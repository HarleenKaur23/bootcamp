#  **Framework and Library**

They are often use it interchangeably, but they have different meanings in software development:

##### 1. **Library**

- **Definition**: A library is a collection of pre-written code that you can call when needed. It provides specific functionality, but **you control the flow** of the application. As a software engineer are in charge of deciding when and where to use functions from the library.
- Example
  - **HikariCP** : Manages database connections efficiently, reducing the overhead of opening and closing connections.
  - **Log4j / SLF4J (Logging Libraries)**:  help you manage logging in your Java application (recording information, errors, warnings).
  - **React** (often called a framework but is technically a library): You call React functions like `useState()` or `ReactDOM.render()`.
  - **Lodash**: A utility library for JavaScript that offers various helper functions like `_.map()`, `_.filter()`.

- **Analogy**: It’s like having a toolbox. You pick the tool you need and use it.

##### 2. **Framework**

- **Definition**: A framework is a collection of libraries and rules that dictate the structure of your application. It provides a predefined structure and **controls the flow** of the application. As a software engineer write code that fits into the framework’s structure, but the framework decides when and how your code is executed.

- Example

  - **Hibernate**: Maps Java objects to database tables (Object-Relational Mapping), simplifying database interactions..
  - **Spring Boot** (Java): It handles the flow of your application, like managing requests and setting up the server.
  - **Angular**: It provides a complete structure for building applications, handling things like routing, data binding, and state management.

- **Analogy**: It’s like building a house using a prefabricated kit. You follow the framework’s instructions and put things where they are expected.

##### **Key Differences:**

| Feature         | Library                        | Framework                       |
| --------------- | ------------------------------ | ------------------------------- |
| **Control**     | You call the library functions | Framework calls your code       |
| **Flexibility** | More flexible                  | Less flexible, more opinionated |
| **Use Case**    | Specific functions or tasks    | Provides a complete solution    |
| **Examples**    | React, Lodash, jQuery          | Angular, Spring Boot, Django    |

##### **Inversion of Control**:

- The main difference is **inversion of control**. In a library, **you are in control**. In a framework, **the framework is in control** and calls your code when needed.

If you're building a React app, you decide when to use hooks like `useEffect()`. If you're using Angular, it dictates the flow, handling components, services, and routing automatically.