## Servlets and Filters

Here's a detailed explanation and code examples for **2a (Servlets)** and **2b (Filters)** with a Spring Framework (6.2.1) setup that doesn't use Spring Boot. The project will be deployable to a Tomcat server using the Maven deploy plugin.

---

### **2a. Servlets**

#### Key Concepts:

- A Servlet processes HTTP requests and generates responses.
- It's part of the core Java EE stack.
- The lifecycle of a Servlet includes `init()`, `service()`, and `destroy()` methods.

#### Example: Basic Servlet in Spring Framework

##### **Directory Structure**

```
src/
├── main/
│   ├── java/
│   │   └── com/example/
│   │       ├── config/
│   │       │   └── AppConfig.java
│   │       ├── servlet/
│   │       │   └── MyServlet.java
│   ├── webapp/
│       ├── WEB-INF/
│       │   ├── web.xml
│       └── index.html
```

##### **1. Servlet Implementation**

```java
package com.example.servlet;

import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

@WebServlet(name = "MyServlet", urlPatterns = {"/hello"})
public class MyServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/plain");
        resp.getWriter().write("Hello from MyServlet!");
    }
}
```

##### **2. Configuration in `web.xml`**

```xml
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>myServlet</servlet-name>
        <servlet-class>com.example.servlet.MyServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>myServlet</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
</web-app>
```

---

### **2b. Filters**

#### Key Concepts:

- Filters intercept requests before they reach Servlets.
- Useful for preprocessing (e.g., logging, security, content compression).

#### Example: Logging Filter

##### **1. Filter Implementation**

```java
package com.example.servlet;

import jakarta.servlet.Filter;
import jakarta.servlet.FilterChain;
import jakarta.servlet.FilterConfig;
import jakarta.servlet.ServletException;
import jakarta.servlet.ServletRequest;
import jakarta.servlet.ServletResponse;
import jakarta.servlet.annotation.WebFilter;

import java.io.IOException;

@WebFilter(urlPatterns = "/*")
public class LoggingFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("LoggingFilter initialized");
    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        System.out.println("Request received: " + request.getRemoteAddr());
        chain.doFilter(request, response); // Continue to the next filter or servlet
    }

    @Override
    public void destroy() {
        System.out.println("LoggingFilter destroyed");
    }
}
```

##### **2. Configuration in `web.xml`**

```xml
<filter>
    <filter-name>authenticationFilter</filter-name>
    <filter-class>io.reactivestax.filter.AuthenticationFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>loggingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

<filter>
    <filter-name>loggingFilter</filter-name>
    <filter-class>io.reactivestax.filter.LoggingFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>loggingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

```

---

### Maven Configuration for Tomcat Deployment

##### **1. Add Maven Plugin for Deployment**

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-war-plugin</artifactId>
            <version>3.3.1</version>
            <configuration>
                <failOnMissingWebXml>false</failOnMissingWebXml>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
                <url>http://localhost:8080/manager/text</url>
                <server>TomcatServer</server>
                <path>/example</path>
            </configuration>
        </plugin>
    </plugins>
</build>
```

##### **2. Add a Server in Maven `.m2/conf/settings.xml`**

```xml
<server>
    <id>TomcatServer</id>
    <username>admin</username>
    <password>password</password>
</server>
```

##### **3. Deploy Using Maven**

Run the following command:

```bash
mvn tomcat7:deploy    (compare this to mvn spring-boot:run)

this guy just copies the .war file to tomcat/webapps folder
```

---

### Summary

- **Servlets** are used for request processing, while **Filters** provide preprocessing.
- Configuration is done using `web.xml` or annotations like `@WebServlet` and `@WebFilter`.
- Deployment is simplified with Maven's `maven-war-plugin` and `tomcat7-maven-plugin`.



## Servlet lifecycle methods 

The **`service()`** method and the **`doGet()`**, **`doPost()`**, **`doPut()`**, etc., methods in a servlet serve different purposes but are closely related. Here’s a breakdown of the differences:

---

### **1. The `service()` Method**

#### **Purpose**:

- The `service()` method is the core of the servlet that handles all incoming HTTP requests.
- It determines the HTTP method (e.g., GET, POST, PUT, DELETE) of the request and dispatches it to the appropriate `doXXX()` method (`doGet()`, `doPost()`, etc.).

#### **Default Implementation**:

- In the `HttpServlet` class, `service()` is already implemented to delegate to `doGet()`, `doPost()`, and other methods based on the request type.
- You rarely need to override `service()` unless you want to handle all request types in one method.

#### **Flow**:

1. Servlet container calls `service()` for every incoming request.
2. `service()` inspects the request's HTTP method (e.g., GET, POST).
3. Based on the HTTP method:
   - `GET` → `doGet()`
   - `POST` → `doPost()`
   - `PUT` → `doPut()`
   - `DELETE` → `doDelete()`
   - etc.

#### **When to Use**:

- You override `service()` if you need to handle all HTTP methods in a custom way or need custom routing logic that doesn't rely on `doXXX()` methods.

#### **Example**:

```java
@Override
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String method = req.getMethod(); // Determine the HTTP method
    resp.getWriter().write("Handled by service() method. HTTP Method: " + method);
}
```

---

### **2. The `doXXX()` Methods (e.g., `doGet()`, `doPost()`)**

#### **Purpose**:

- The `doXXX()` methods are specialized handlers for specific HTTP methods.
- These methods are called by `service()` when a request with the corresponding HTTP method is received.

#### **Specialization**:

- Each `doXXX()` method is tailored to handle a specific HTTP method:
  - `doGet()`: Handles GET requests.
  - `doPost()`: Handles POST requests.
  - `doPut()`: Handles PUT requests.
  - `doDelete()`: Handles DELETE requests.
  - `doHead()`: Handles HEAD requests.
  - `doOptions()`: Handles OPTIONS requests.

#### **When to Use**:

- Override these methods to handle specific HTTP methods without worrying about routing logic (already handled by `service()`).

#### **Example**:

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    resp.getWriter().write("Handled by doGet() method.");
}

@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    resp.getWriter().write("Handled by doPost() method.");
}
```

---

### **3. Key Differences Between `service()` and `doXXX()`**

| **Aspect**           | **`service()`**                                              | **`doXXX()` (e.g., `doGet()`, `doPost()`)**          |
| -------------------- | ------------------------------------------------------------ | ---------------------------------------------------- |
| **Purpose**          | Handles all HTTP methods and dispatches to `doXXX()` methods. | Handles specific HTTP methods (e.g., GET, POST).     |
| **Default Behavior** | Implemented in `HttpServlet` to call the appropriate `doXXX()`. | Empty in `HttpServlet`; you need to override them.   |
| **When Called**      | Called by the servlet container for every HTTP request.      | Called by `service()` based on the HTTP method.      |
| **Use Case**         | Override to handle all methods together or customize routing. | Override to handle specific HTTP methods separately. |
| **Level of Control** | Provides lower-level control over request handling.          | Focused on specific HTTP operations.                 |

---

### **4. Relationship Between `service()` and `doXXX()`**

- **Default Workflow**:
  - Servlet container calls `service()` for every request.
  - `service()` inspects the HTTP method (`GET`, `POST`, etc.).
  - `service()` delegates the request to the corresponding `doXXX()` method.

- **Customizing Behavior**:
  - If you override `service()`, it takes full control and does not call `doXXX()` methods unless you explicitly invoke them.
  - If you override `doXXX()` methods, the `service()` method's default routing logic remains intact.

---

### **Examples of Overriding**

#### **Overriding `doGet()` and `doPost()` Separately**:

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    resp.getWriter().write("This is a GET request.");
}

@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    resp.getWriter().write("This is a POST request.");
}
```

#### **Overriding `service()` to Handle All Requests**:

```java
@Override
protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String method = req.getMethod();
    resp.getWriter().write("Request handled by service() method. HTTP Method: " + method);

    // Custom routing logic
    if ("GET".equalsIgnoreCase(method)) {
        resp.getWriter().write(" - Special GET handling.");
    } else if ("POST".equalsIgnoreCase(method)) {
        resp.getWriter().write(" - Special POST handling.");
    }
}
```

---

### **When to Use Which**

- **Use `doGet()`, `doPost()`, etc.**:
  - When your servlet has distinct behavior for different HTTP methods.
  - Common for web applications where forms use POST and pages use GET.

- **Use `service()`**:
  - When you need to handle all HTTP methods in a unified manner.
  - Useful for building custom routing mechanisms or handling non-standard HTTP methods.



## **Chained Filters That Eventually Hit a Servlet**

Filters in Java Servlets are used to preprocess or post-process requests and responses. They are executed in a chain, one after another, in the order specified in the deployment descriptor (`web.xml`) or annotations. Filters only execute **before** and optionally **after** the servlet processes the request; they cannot run exclusively after the servlet.

---

### **Filter Lifecycle**

1. **Request Processing**:
   - Filters are executed **before the servlet**.
   - Each filter in the chain can perform processing and then pass control to the next filter or the servlet.

2. **Response Processing**:
   - Filters can process the response as it is passed back through the chain.

---

### **Code Example: Chained Filters**

#### **1. Servlet**

```java
package com.example.servlet;

import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

@WebServlet(name = "MyServlet", urlPatterns = {"/my-servlet"})
public class MyServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.getWriter().write("Response from MyServlet");
    }
}
```

---

#### **2. Filter 1: Logging Filter**

```java
package com.example.filter;

import jakarta.servlet.Filter;
import jakarta.servlet.FilterChain;
import jakarta.servlet.FilterConfig;
import jakarta.servlet.ServletException;
import jakarta.servlet.ServletRequest;
import jakarta.servlet.ServletResponse;
import jakarta.servlet.annotation.WebFilter;

import java.io.IOException;

@WebFilter(filterName = "LoggingFilter", urlPatterns = "/*")
public class LoggingFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("LoggingFilter initialized");
    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        System.out.println("LoggingFilter: Before servlet");
        chain.doFilter(request, response); // Pass request to next filter or servlet
        System.out.println("LoggingFilter: After servlet");
    }

    @Override
    public void destroy() {
        System.out.println("LoggingFilter destroyed");
    }
}
```

---

#### **3. Filter 2: Authentication Filter**

```java
package com.example.filter;

import jakarta.servlet.Filter;
import jakarta.servlet.FilterChain;
import jakarta.servlet.FilterConfig;
import jakarta.servlet.ServletException;
import jakarta.servlet.ServletRequest;
import jakarta.servlet.ServletResponse;
import jakarta.servlet.annotation.WebFilter;

import java.io.IOException;

@WebFilter(filterName = "AuthenticationFilter", urlPatterns = "/*")
public class AuthenticationFilter implements Filter {

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("AuthenticationFilter initialized");
    }

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        System.out.println("AuthenticationFilter: Checking authentication");
        // Perform authentication checks here (example logic omitted)
        chain.doFilter(request, response); // Pass request to next filter or servlet
        System.out.println("AuthenticationFilter: After servlet processing");
    }

    @Override
    public void destroy() {
        System.out.println("AuthenticationFilter destroyed");
    }
}
```

---

#### **4. Deployment Configuration (web.xml)**

The order of filters in `web.xml` defines the chaining order.

```xml
<filter>
    <filter-name>LoggingFilter</filter-name>
    <filter-class>com.example.filter.LoggingFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>LoggingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

<filter>
    <filter-name>AuthenticationFilter</filter-name>
    <filter-class>com.example.filter.AuthenticationFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>AuthenticationFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

<servlet>
    <servlet-name>MyServlet</servlet-name>
    <servlet-class>com.example.servlet.MyServlet</servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name>MyServlet</servlet-name>
    <url-pattern>/my-servlet</url-pattern>
</servlet-mapping>
```

---

### **Flow of Execution**

1. A request to `/my-servlet` hits the `LoggingFilter` first.
2. The `LoggingFilter` processes the request and passes it to the `AuthenticationFilter`.
3. The `AuthenticationFilter` processes the request and passes it to the servlet.
4. The servlet processes the request and generates a response.
5. The response is passed back through the filters in reverse order:
   - `AuthenticationFilter`
   - `LoggingFilter`
6. The client receives the final response.

---

### **Logs Example**

For a request to `/my-servlet`, the logs might look like this:

```
LoggingFilter initialized
AuthenticationFilter initialized
LoggingFilter: Before servlet
AuthenticationFilter: Checking authentication
Response from MyServlet
AuthenticationFilter: After servlet processing
LoggingFilter: After servlet
```

---

### **Can Filters Execute After the Servlet Alone?**

No, filters cannot execute **only after** the servlet. Filters are designed to:

1. Process **before** the servlet (request preprocessing).
2. Optionally process **after** the servlet (response post-processing).

This dual capability ensures filters can act as interceptors for both the request and response.

---

### **Summary**

- Filters form a chain and always execute **before and/or after** the servlet.
- The order of execution is defined by the order of mapping in `web.xml` or annotations.
- Filters cannot run exclusively after the servlet.



In the **`web.xml`**, the order in which filters are declared and mapped signals the execution order of the filter chain. Specifically:

### **How Filter Order Is Determined**

1. **Order in `web.xml`:**

   - Filters are executed **in the order of their `<filter-mapping>` elements** in the `web.xml` file.
   - The first `<filter-mapping>` element corresponds to the first filter in the chain, the second `<filter-mapping>` corresponds to the second filter, and so on.

2. **Mapping in the Provided Example:**

   ```xml
   <filter>
       <filter-name>LoggingFilter</filter-name>
       <filter-class>com.example.filter.LoggingFilter</filter-class>
   </filter>
   <filter-mapping>
       <filter-name>LoggingFilter</filter-name>
       <url-pattern>/*</url-pattern>
   </filter-mapping>
   
   <filter>
       <filter-name>AuthenticationFilter</filter-name>
       <filter-class>com.example.filter.AuthenticationFilter</filter-class>
   </filter>
   <filter-mapping>
       <filter-name>AuthenticationFilter</filter-name>
       <url-pattern>/*</url-pattern>
   </filter-mapping>
   ```

   - `LoggingFilter` is declared and mapped first, so it is executed **before** `AuthenticationFilter`.

---

### **Execution Flow in the Example**

1. **Request Processing**:
   - The request first enters the `LoggingFilter` because its `<filter-mapping>` appears first.
   - The `LoggingFilter` calls `chain.doFilter(request, response)`, which passes control to the next filter in the chain.
   - The next filter (`AuthenticationFilter`) is executed.

2. **Response Processing**:
   - After the servlet processes the request and generates a response, the filters process the response in **reverse order**.
   - The `AuthenticationFilter` processes the response first.
   - The `LoggingFilter` processes the response last.

---

### **Changing the Filter Execution Order**

To make `AuthenticationFilter` execute **before** `LoggingFilter`, simply swap the order of the `<filter-mapping>` elements in `web.xml`:

```xml
<filter>
    <filter-name>AuthenticationFilter</filter-name>
    <filter-class>com.example.filter.AuthenticationFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>AuthenticationFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>

<filter>
    <filter-name>LoggingFilter</filter-name>
    <filter-class>com.example.filter.LoggingFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>LoggingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

Now, the execution order will be:

1. `AuthenticationFilter` → request preprocessing.
2. `LoggingFilter` → request preprocessing.
3. Servlet processes the request.
4. `LoggingFilter` → response postprocessing.
5. `AuthenticationFilter` → response postprocessing.

---

### **Using Annotations**

If you use annotations (`@WebFilter`) instead of `web.xml`, the execution order is determined by the **string sorting of the class names** of the filters. To control the order explicitly, use the `@WebFilter` `filterName` attribute to name the filters alphabetically or add dependencies programmatically in your configuration.

---

When using `@WebFilter` annotations, the order of execution is not explicitly controlled by the annotations themselves. Instead, the servlet container determines the order based on how it discovers and loads the filters. This can depend on factors like the alphabetical order of class names or the order in which the annotations are processed internally.

To explicitly define the filter order when using `@WebFilter`, you need to:

### **1. Use a Filter Registration Programmatically**

By registering filters in a specific order programmatically in the `ServletContext`, you can control the execution order.

#### **Example: Define Order Programmatically**

```java
package com.example.config;

import com.example.filter.AuthenticationFilter;
import com.example.filter.LoggingFilter;

import jakarta.servlet.Filter;
import jakarta.servlet.FilterRegistration;
import jakarta.servlet.ServletContext;
import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebListener;

@WebListener
public class FilterRegistrationListener implements jakarta.servlet.ServletContextListener {
    @Override
    public void contextInitialized(ServletContext servletContext) {
        // Register LoggingFilter first
        Filter loggingFilter = new LoggingFilter();
        FilterRegistration.Dynamic loggingFilterRegistration = servletContext.addFilter("LoggingFilter", loggingFilter);
        loggingFilterRegistration.addMappingForUrlPatterns(null, false, "/*");

        // Register AuthenticationFilter second
        Filter authenticationFilter = new AuthenticationFilter();
        FilterRegistration.Dynamic authFilterRegistration = servletContext.addFilter("AuthenticationFilter", authenticationFilter);
        authFilterRegistration.addMappingForUrlPatterns(null, false, "/*");
    }

    @Override
    public void contextDestroyed(ServletContext servletContext) {
        // No cleanup needed
    }
}
```

In this example:

- `LoggingFilter` is registered first, so it will execute before `AuthenticationFilter`.

---

### **2. Alternative: Use a Framework-Specific Mechanism**

If you're using a framework like **Spring**, you can define the filter order explicitly using the `@Order` annotation or the `FilterRegistrationBean`.

#### **Example in Spring Boot (for Reference)**:

```java
@Configuration
public class FilterConfig {
    @Bean
    @Order(1) // LoggingFilter executes first
    public FilterRegistrationBean<LoggingFilter> loggingFilter() {
        FilterRegistrationBean<LoggingFilter> registrationBean = new FilterRegistrationBean<>();
        registrationBean.setFilter(new LoggingFilter());
        registrationBean.addUrlPatterns("/*");
        return registrationBean;
    }

    @Bean
    @Order(2) // AuthenticationFilter executes second
    public FilterRegistrationBean<AuthenticationFilter> authenticationFilter() {
        FilterRegistrationBean<AuthenticationFilter> registrationBean = new FilterRegistrationBean<>();
        registrationBean.setFilter(new AuthenticationFilter());
        registrationBean.addUrlPatterns("/*");
        return registrationBean;
    }
}
```

---

### **3. Why You Cannot Control Order Using `@WebFilter` Alone**

The `@WebFilter` annotation does not provide a mechanism for explicitly defining the order. Filters declared with `@WebFilter` are processed in an unspecified order, often based on:

- Alphabetical order of class names.
- The order of discovery during servlet container initialization.

#### Example of Ambiguous Order:

```java
@WebFilter(filterName = "LoggingFilter", urlPatterns = "/*")
public class LoggingFilter implements Filter { /*...*/ }

@WebFilter(filterName = "AuthenticationFilter", urlPatterns = "/*")
public class AuthenticationFilter implements Filter { /*...*/ }
```

The container might execute filters in alphabetical order (`AuthenticationFilter` before `LoggingFilter`) or based on other internal factors.

---

### **Summary**

- **For Explicit Order**: Use programmatic registration (`ServletContext#addFilter`) to define the order.
- **For Frameworks**: Use mechanisms like `@Order` or filter registration beans provided by the framework.
- **With `@WebFilter` Alone**: The order is not guaranteed and depends on the servlet container's implementation.

---------



## HttpRequest methods

In Servlets, both `request.getParameter` and `request.getAttribute` are used to retrieve data from an HTTP request, but they serve different purposes and are used in different scenarios.

---

### **Key Differences**

| **Aspect**        | **`request.getParameter`**                                   | **`request.getAttribute`**                                   |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Purpose**       | Retrieves data sent as part of the HTTP request (query string, form fields). | Retrieves attributes set in the request scope by the server or application. |
| **Data Source**   | Parameters are part of the **request payload** (e.g., form data, URL query string). | Attributes are part of the **request object**, added programmatically. |
| **Usage Context** | Used for retrieving **user input** from forms or query strings. | Used for passing **server-side data** between components (e.g., servlets, JSPs). |
| **Data Format**   | Always returns data as a `String` (or `null` if not present). | Can store and retrieve objects of any type (`Object`).       |
| **Scope**         | Request parameters are **read-only**.                        | Request attributes are **mutable** (can be added, modified, removed). |
| **Availability**  | Automatically available in the request when the client sends it. | Must be explicitly set in the request by server-side code.   |

---

### **Examples**

#### **`request.getParameter`**

Used to retrieve user input sent via form data or query string.

- **Scenario**: The user submits a form with `POST` or `GET` method.

- **Example HTML Form**:

  ```html
  <form action="/exampleServlet" method="POST">
      <input type="text" name="username" value="JohnDoe">
      <button type="submit">Submit</button>
  </form>
  ```

- **Servlet Code**:

  ```java
  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
      String username = req.getParameter("username");
      resp.getWriter().write("Hello, " + username);
  }
  ```

- **Output**:

  ```
  Hello, JohnDoe
  ```

#### **`request.getAttribute`**

Used to share data between server-side components (e.g., passing data from a servlet to a JSP).

- **Scenario**: A servlet processes some logic and forwards data to a JSP.

- **Servlet Code**:

  ```java
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
      req.setAttribute("greeting", "Welcome to the Servlet World!");
      req.getRequestDispatcher("/example.jsp").forward(req, resp);
  }
  ```

- **JSP Code**:

  ```jsp
  <h1>${greeting}</h1>
  ```

- **Output**:

  ```
  Welcome to the Servlet World!
  ```

---

### **Comparison in Use Cases**

| **Use Case**                                | **Use `getParameter`**                            | **Use `getAttribute`**                        |
| ------------------------------------------- | ------------------------------------------------- | --------------------------------------------- |
| Retrieving form data                        | `String username = req.getParameter("username");` | Not applicable.                               |
| Passing data between server-side components | Not applicable.                                   | `req.setAttribute("key", value);`             |
| Query string values                         | `String id = req.getParameter("id");`             | Not applicable.                               |
| Sharing objects between servlet and JSP     | Not applicable.                                   | `req.setAttribute("user", new User("John"));` |

---

### **When to Use Which**

- Use **`request.getParameter`** when retrieving input sent by the **client** (via forms or query strings).
- Use **`request.getAttribute`** when sharing data between **server-side components** like servlets, filters, or JSPs.

-------

In Servlets, **request headers** and **HTTP sessions** are key components for managing client-server communication and maintaining state. Here's how they are handled:

---

### **1. Managing Request Headers in Servlets**

#### **Accessing Request Headers**

The `HttpServletRequest` object provides methods to access HTTP headers sent by the client.

- **Common Methods**:
  - `request.getHeader(String name)`: Retrieves the value of a specific header.
  - `request.getHeaders(String name)`: Retrieves all values of a header (useful for multi-valued headers like `Set-Cookie`).
  - `request.getHeaderNames()`: Retrieves an enumeration of all header names.

#### **Example: Reading Headers**

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // Access a specific header
    String userAgent = req.getHeader("User-Agent");
    String host = req.getHeader("Host");

    // Print headers to response
    resp.setContentType("text/plain");
    resp.getWriter().write("User-Agent: " + userAgent + "\n");
    resp.getWriter().write("Host: " + host + "\n");

    // Print all headers
    resp.getWriter().write("All Headers:\n");
    Enumeration<String> headerNames = req.getHeaderNames();
    while (headerNames.hasMoreElements()) {
        String headerName = headerNames.nextElement();
        resp.getWriter().write(headerName + ": " + req.getHeader(headerName) + "\n");
    }
}
```

#### **Setting Response Headers**

The `HttpServletResponse` object allows you to add or modify response headers.

- **Common Methods**:
  - `response.setHeader(String name, String value)`: Sets a response header.
  - `response.addHeader(String name, String value)`: Adds a header without replacing existing values.

#### **Example: Setting Headers**

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // Set headers
    resp.setHeader("Content-Type", "application/json");
    resp.setHeader("Custom-Header", "MyValue");

    // Write response
    resp.getWriter().write("{\"message\": \"Hello, World!\"}");
}
```

---

### **2. Handling HTTP Sessions in Servlets**

#### **What is an HTTP Session?**

- HTTP is a stateless protocol; sessions allow you to maintain state across multiple requests.
- `HttpSession` provides a way to associate client data with a unique session ID.

#### **Creating and Accessing a Session**

The `HttpServletRequest` object provides the `getSession()` method to retrieve or create a session.

- **Common Methods**:
  - `request.getSession()`: Returns the current session or creates a new one if it doesn’t exist.
  - `request.getSession(boolean create)`: Returns the current session; if `create` is `false`, it won’t create a new session.
  - `session.setAttribute(String name, Object value)`: Stores an attribute in the session.
  - `session.getAttribute(String name)`: Retrieves an attribute from the session.
  - `session.removeAttribute(String name)`: Removes an attribute.
  - `session.invalidate()`: Invalidates the session, removing all attributes.

#### **Example: Managing Sessions**

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    HttpSession session = req.getSession(); // Get or create session

    // Set session attribute
    session.setAttribute("username", "JohnDoe");

    // Get session attribute
    String username = (String) session.getAttribute("username");

    // Write session info
    resp.setContentType("text/plain");
    resp.getWriter().write("Username: " + username + "\n");
    resp.getWriter().write("Session ID: " + session.getId() + "\n");
    resp.getWriter().write("Is New Session: " + session.isNew() + "\n");
}
```

#### **Session Lifecycle**

- Sessions are automatically created on the first `getSession()` call.

- Sessions expire after a period of inactivity (default: 30 minutes).

- You can configure session timeout in `web.xml`:

  ```xml
  <session-config>
      <session-timeout>15</session-timeout>
  </session-config>
  ```

#### **Invalidating a Session**

```java
HttpSession session = req.getSession(false);
if (session != null) {
    session.invalidate(); // Remove session and all attributes
}
```

#### **Storing Complex Objects in Sessions**

You can store objects in a session. The object must implement `Serializable` if session data is persisted or distributed.

```java
session.setAttribute("cart", new ShoppingCart());
ShoppingCart cart = (ShoppingCart) session.getAttribute("cart");
```

---

### **3. Combining Headers and Sessions**

A common use case is storing user authentication tokens in headers and associating user-specific data with the session.

#### **Example**

```java
@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // Read headers
    String authToken = req.getHeader("Authorization");

    // Manage session
    HttpSession session = req.getSession();
    if (authToken != null && authToken.equals("valid-token")) {
        session.setAttribute("authenticated", true);
        resp.getWriter().write("User authenticated!");
    } else {
        session.invalidate();
        resp.getWriter().write("Invalid token. Session terminated.");
    }
}
```

---

### **Best Practices**

- **For Headers**:
  - Avoid overusing custom headers; use standard ones wherever possible.
  - Validate header values to prevent injection attacks.

- **For Sessions**:
  - Store only essential data to minimize memory usage.
  - Use `invalidate()` to end sessions after logout or when no longer needed.
  - Set session timeout to a reasonable duration to reduce resource consumption.