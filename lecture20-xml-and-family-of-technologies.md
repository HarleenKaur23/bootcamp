# **XML**

XML (e**Xtensible Markup Language**) is a markup language designed to store and transport data in a **structured, human-readable, and machine-readable format**. It is widely used for data interchange between systems, configuration files, and document storage. **XML** (**eXtensible Markup Language**) was created in **1996** by the **World Wide Web Consortium (W3C)**.

- **Released Date**: XML 1.0 was officially released as a recommendation on **February 10, 1998**.

- **Creators**: XML was developed by a working group led by **Jon Bosak** at W3C. Jon Bosak is often referred to as the "Father of XML."

- **Goal**: The primary purpose of XML was to simplify SGML (**Standard Generalized Markup Language**) and make it more accessible for web-based applications while still retaining its ability to represent structured data.

**Example of XML Document:**

```
<?xml version="1.0" encoding="UTF-8"?>
<book>
    <title>Clean Code</title>
    <author>Robert C. Martin</author>
    <year>2008</year>
    <price>29.99</price>
</book>
```

In this example:

- The root element is `<book>`.
- Elements like `<title>`, `<author>`, `<year>`, and `<price>` contain specific data about the book.

##### **Why Was XML Created?**

XML was created to:

1. **Data Interchange**:  XML was designed to store and exchange data between different systems, applications  (e.g., web services using SOAP) in a standardized way. 
2. **Simplify Data Sharing**: Before XML, data sharing between applications and over the internet was complex due to incompatible formats. How do multiple application, services, exchange data and agree on the common structure of the data.
3. **Provide a Flexible Format**: XML is **extensible**, meaning you can define your own custom tags based on your needs.
4. **Configuration**: Many software systems use XML for configuration files (e.g., Maven `pom.xml`, Hibernate `hibernate*.cfg.xml` ).
5. **Document Storage**: Formats like Microsoft Word and Excel files internally use XML. (Change the microsoft office documents to .zip file and you can open it up, internally it's creates set of xml documents to maintain spreadsheet, ppt , word documents)
6. **Web Development**: SOAP-based web services, Rest Services,  XML is also used for RSS feeds, SVG graphics and it was extensively used to define configuration properties for Spring Frameworks, lo .
7. **Separate Data from Presentation**: XML separates data from how it is displayed, unlike **HTML**, which focuses on presentation.

##### **Key Features of XML:**

1. **Self-descriptive:**

   : XML documents include data along with metadata that describes the data structure, making it easy to understand.

   ```xml
   <person>
       <name>John Doe</name>
       <age>30</age>
   </person>
   ```

2. **Customizable Tags**: Unlike HTML, XML allows you to define your own tags to describe the data.

3. **Platform and Language Independent**: XML can be used across different systems and programming languages.

4. **Hierarchical Structure**: Data is stored in a tree-like structure with nested elements.

5. **Extensible**: You can extend it to fit the needs of specific applications.

6. **Text-based Format**: XML is stored in plain text, making it easily editable and portable.

7. **Unicode Support**: XML supports Unicode, allowing it to handle different languages and characters.

##### **Advantages:**

- **Human and Machine Readable**: Easy for both developers and systems to understand.
- **Structured and Flexible**: Adaptable to various domains and use cases.
- **Wide Adoption**: Many tools and libraries support XML processing.

##### **Limitations:**

- **Verbose**: XML documents can become large due to detailed tags.
- **Complexity**: Parsing and processing XML can require more effort compared to simpler formats like JSON.
- **Performance**: Larger size and complexity can lead to slower performance.

###### Example of an XML Document:

```xml
<bookstore>
   <book>
       <title lang="en">Learning XML</title>
       <author>John Smith</author>
       <price>29.99</price>
   </book>
   <book>
       <title lang="es">Aprendiendo XML</title>
       <author>Juan Pérez</author>
       <price>19.99</price>
   </book>
</bookstore>
```

#### **Here are some of the example how xml was used extensively** 

##### **XML was used extensively used for data exchange and configuration management**

**SOAP (Simple Object Access Protocol) Services** are a type of **web service** that use **XML-based messaging** to exchange information between systems over a network. Here is the sample XML SOAP Request and Response Messages (we don't need to understand the message semantic today, when we cover SOAP Services we will go into the structure of the messages, implementation and full details) 

**SOAP (Simple Object Access Protocol)** was created in **1998** by **Microsoft, IBM, and DevelopMentor** as a standard for exchanging structured information in the implementation of web services. SOAP Schema https://schemas.xmlsoap.org/soap/envelope/

###### **1. SOAP Request Message**

A SOAP request is used to call a web service method, typically with some input parameters.

**Example Request:**

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" 
                  xmlns:web="http://www.example.com/webservice">
   <soapenv:Header/>
   <soapenv:Body>
      <web:GetUserDetails>
         <web:UserId>12345</web:UserId>
      </web:GetUserDetails>
   </soapenv:Body>
</soapenv:Envelope>
```

###### **Explanation**:

- ```
  <soapenv:Envelope>
  ```

  : The root element of the SOAP message.

  - `xmlns:soapenv`: Namespace for the SOAP protocol.
  - `xmlns:web`: Namespace for the web service's operations.

- `<soapenv:Header>`: Contains metadata (optional for this example).

- `<soapenv:Body>`: Contains the actual request.

- `<web:GetUserDetails>`: The operation (method) being invoked.

- `<web:UserId>`: Input parameter for the method.

- See the Root XML Root <soapenv:Envelope, it points to different namepsaces used in the soap envelope

------

###### **2. SOAP Response Message**

A SOAP response returns the result of the web service method invocation.

###### **Example Response:**

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" 
                  xmlns:web="http://www.example.com/webservice">
   <soapenv:Header/>
   <soapenv:Body>
      <web:GetUserDetailsResponse>
         <web:User>
            <web:UserId>12345</web:UserId>
            <web:Name>John Doe</web:Name>
            <web:Email>john.doe@example.com</web:Email>
         </web:User>
      </web:GetUserDetailsResponse>
   </soapenv:Body>
</soapenv:Envelope>
```

###### **Explanation**:

- `<soapenv:Envelope>`: The root element of the SOAP message.
- `<soapenv:Header>`: Typically empty unless there is additional metadata.
- `<soapenv:Body>`: Contains the actual response data.
- `<web:GetUserDetailsResponse>`: The response to the operation.
- `<web:User>`: Contains the data returned by the service, such as user details.
- See the Root XML Root <soapenv:Envelope, it points to different namepsaces used in the soap envelope

------

###### **SOAP Fault Example**

When an error occurs, the response includes a `<Fault>` element.

###### **Example Fault Response:**

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
   <soapenv:Header/>
   <soapenv:Body>
      <soapenv:Fault>
         <faultcode>soapenv:Client</faultcode>
         <faultstring>Invalid UserId</faultstring>
         <detail>
            User ID must be a positive integer.
         </detail>
      </soapenv:Fault>
   </soapenv:Body>
</soapenv:Envelope>
```

**Explanation**:

- `<soapenv:Fault>`: Indicates an error.
- `<faultcode>`: Error type or source (e.g., `Client`, `Server`).
- `<faultstring>`: Human-readable description of the error.
- `<detail>`: Optional additional details about the error.

------

###### **Key Characteristics of SOAP Messages:**

- **Transport Protocol**: SOAP typically uses HTTP/HTTPS, but it can use other protocols like SMTP.
- **Structure**: Every message has an `Envelope`, and optionally a `Header`, with the core data in the `Body`.
- **Namespace**: Namespaces ensure element names do not conflict between different systems.

_________________________

#### Several **Java and others** frameworks utilizes **XML-based configuration** files for defining application behavior, bean wiring, dependency injection, and other settings. Here's a list of popular Java frameworks that extensively support or originally relied on XML-based configuration:

------

##### **1. Spring Framework**

- **Purpose**: Dependency Injection (DI), Aspect-Oriented Programming (AOP), and Enterprise Java applications.

- XML Use

  :

  - Define beans, their dependencies, and configurations.
  - Set up security, database configurations, and web services.

- Example

  :

  ```xml
  <beans xmlns="http://www.springframework.org/schema/beans">
      <bean id="myBean" class="com.example.MyBean">
          <property name="property1" value="value1"/>
      </bean>
  </beans>
  ```

- **Modern Approach**: While XML was the original configuration method, Spring now prefers annotations and Java-based configuration (`@Configuration` and `@Bean`).

------

##### **2. Hibernate**

- **Purpose**: Object-Relational Mapping (ORM).

- XML Use

  :

  - Mapping Java classes to database tables.
  - Configuring relationships between entities.

- Example (Entity Mapping)

  :

  ```xml
  <hibernate-mapping>
      <class name="com.example.Employee" table="EMPLOYEES">
          <id name="id" column="EMP_ID">
              <generator class="native"/>
          </id>
          <property name="name" column="EMP_NAME"/>
      </class>
  </hibernate-mapping>
  ```

- **Modern Approach**: XML is still widely supported, but annotations like `@Entity` and `@Table` are commonly used.

------

##### **3. Apache Struts**

- **Purpose**: Web application framework (Model-View-Controller pattern).

- XML Use

  :

  - Configure actions, result types, and interceptors in the `struts.xml` file.

- Example

  :

  ```xml
  <struts>
      <package name="default" namespace="/" extends="struts-default">
          <action name="login" class="com.example.LoginAction">
              <result name="success">/welcome.jsp</result>
              <result name="error">/login.jsp</result>
          </action>
      </package>
  </struts>
  ```

- **Modern Approach**: Supports annotations (`@Action`, `@Result`) but XML is still prevalent.

------

##### **4. Apache Maven**

- **Purpose**: Build and dependency management tool.

- XML Use

  :

  - Project Object Model (POM) is defined in `pom.xml`.

- Example

  :

  ```xml
  <project xmlns="http://maven.apache.org/POM/4.0.0">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.example</groupId>
      <artifactId>my-app</artifactId>
      <version>1.0-SNAPSHOT</version>
      <dependencies>
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-core</artifactId>
              <version>5.3.10</version>
          </dependency>
      </dependencies>
  </project>
  ```

------

##### **5. Apache Ant**

- **Purpose**: Build automation tool (predecessor to Maven).

- XML Use

  :

  - Define build tasks and targets in `build.xml`.

- Example

  :

  ```xml
  <project name="MyProject" default="compile">
      <target name="compile">
          <javac srcdir="src" destdir="build"/>
      </target>
  </project>
  ```

------

##### **6. JavaServer Faces (JSF)**

- **Purpose**: Web application framework for building UI components.

- XML Use

  :

  - Configure navigation rules and beans in `faces-config.xml`.

- Example

  :

  ```xml
  <navigation-rule>
      <from-view-id>/login.xhtml</from-view-id>
      <navigation-case>
          <from-outcome>success</from-outcome>
          <to-view-id>/home.xhtml</to-view-id>
      </navigation-case>
  </navigation-rule>
  ```

------

##### **7. JAX-WS (Java API for XML Web Services)**

- **Purpose**: Web service development.

- XML Use

  :

  - Define WSDL (Web Services Description Language) for service contracts.

- Example

  :

  ```xml
  <definitions xmlns="http://schemas.xmlsoap.org/wsdl/">
      <service name="MyService">
          <port name="MyPort" binding="tns:MyBinding">
              <soap:address location="http://example.com/MyService"/>
          </port>
      </service>
  </definitions>
  ```

------

##### **8. Log4j (Version 1.x)**

- **Purpose**: Logging framework.

- XML Use

  :

  - Configure loggers, appenders, and log levels in `log4j.xml`.

- Example

  :

  ```xml
  <log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
      <appender name="Console" class="org.apache.log4j.ConsoleAppender">
          <layout class="org.apache.log4j.PatternLayout">
              <param name="ConversionPattern" value="%d [%t] %-5p %c - %m%n"/>
          </layout>
      </appender>
      <root>
          <level value="DEBUG"/>
          <appender-ref ref="Console"/>
      </root>
  </log4j:configuration>
  ```

------

##### **9. Java EE (Jakarta EE)**

- **Purpose**: Enterprise application development.

- XML Use

  :

  - Deployment descriptors (`web.xml`, `application.xml`) for configuring web applications and enterprise archives.

- Example (`web.xml`)

  :

  ```xml
  <web-app>
      <servlet>
          <servlet-name>MyServlet</servlet-name>
          <servlet-class>com.example.MyServlet</servlet-class>
      </servlet>
      <servlet-mapping>
          <servlet-name>MyServlet</servlet-name>
          <url-pattern>/myServlet</url-pattern>
      </servlet-mapping>
  </web-app>
  ```

  ___________________

  

**10. JasperReports**

- **Purpose**: Reporting and visualization framework for generating PDF, Excel, and HTML reports.

- XML Use

  :

  - Internally defines report templates and structures in XML files (`.jrxml`). 

- Example

  :

  ```
  xml
  
  
  Copy code
  <jasperReport>
      <parameter name="ReportTitle" class="java.lang.String"/>
      <queryString>
          <![CDATA[SELECT * FROM employees]]>
      </queryString>
      <field name="EmployeeName" class="java.lang.String"/>
      <detail>
          <band>
              <textField>
                  <textFieldExpression><![CDATA[$F{EmployeeName}]]></textFieldExpression>
              </textField>
          </band>
      </detail>
  </jasperReport>
  ```

- **Modern Approach**: JasperReports continues to rely on XML (`.jrxml`) for defining report layouts.

------

##  **XML Namespaces**

XML Namespaces were introduced in **1999** as part of the W3C Recommendation titled ***"Namespaces in XML"*** to address challenges in XML documents involving **multiple vocabularies** or elements with **identical** names.

------

###### **Why Were XML Namespaces Created?**

XML was designed to be highly flexible, allowing developers to define their own tags. However, this flexibility introduced the possibility of **naming conflicts** when different XML vocabularies were combined in the same document.

For example:

- You might include elements from an **HTML vocabulary** and a **custom inventory vocabulary** in the same document.
- Without a way to differentiate between the two vocabularies, there could be ambiguity if both used tags like `<title>` or `<item>`.

**Namespaces solve this problem** by associating a unique identifier (URI) with each vocabulary, ensuring that element and attribute names are **globally unique**.

------

###### **How Do XML Namespaces Work?**

1. **Namespace Declaration**:
   - A namespace is declared using the `xmlns` attribute (short for "XML namespace").
   - It associates a **prefix** with a **Uniform Resource Identifier (URI)**, which acts as a globally unique identifier.
2. **Prefix Usage**:
   - Elements and attributes from the namespace use the defined prefix.
   - This avoids conflicts, even if other vocabularies use the same tag names.

------

###### **Example Without Namespaces (Conflict-Prone)**

```
<document>
    <title>XML Basics</title> <!-- Is this HTML title or custom title? -->
    <title>Inventory System</title> <!-- Naming conflict -->
</document>
```

###### **Example With Namespaces**

```
<document xmlns:html="http://www.w3.org/TR/html4/" 
          xmlns:inv="http://www.example.com/inventory">
    <html:title>XML Basics</html:title> <!-- Clearly HTML -->
    <inv:title>Inventory System</inv:title> <!-- Clearly Inventory -->
</document>
```

###### **Explanation**:

- `xmlns:html="http://www.w3.org/TR/html4/"`: Declares a namespace for HTML elements.
- `xmlns:inv="http://www.example.com/inventory"`: Declares a namespace for inventory elements.
- `html:title` and `inv:title` make it clear which `title` belongs to which vocabulary.

------

###### **Key Benefits of Namespaces**

1. **Avoid Naming Conflicts**: Enables multiple vocabularies to coexist in the same document.
2. **Scalability**: Allows XML documents to grow and integrate additional vocabularies without breaking existing functionality.
3. **Clarity**: Makes XML documents easier to read and interpret, especially in complex systems.

------

###### **How a Namespace URI Works**

- The URI used in namespaces (e.g., `http://www.w3.org/TR/html4/`) is just a unique identifier and does **not** need to resolve to an **actual web page**.
- The URI’s main purpose is to **uniquely identify the namespace** and distinguish it from others.

------

###### **Namespace Defaulting**

- If most elements in a document belong to the same namespace, a **default namespace** can be declared without a prefix:

```
<document xmlns="http://www.example.com/inventory">
    <title>Inventory System</title> <!-- Uses the default namespace -->
    <item>12345</item>
</document>
```

------

###### **When to Use XML Namespaces**

- When combining XML vocabularies (e.g., XHTML with custom XML elements).
- When developing systems where XML schemas may conflict or evolve separately.
- In XML-based standards like **SOAP**, **RSS**, **SVG**, and **XSLT**, namespaces are essential.

______________________________

## **XML Vocabularies**

An **XML vocabulary** is a set of predefined tags and structures used for a specific purpose. When an XML document uses elements and attributes from **more than one vocabulary**, it is said to involve multiple vocabularies.

This is common in scenarios where an XML document integrates features or data from different systems, domains, or standards. Each vocabulary may serve a specific role in the document. To avoid conflicts between the different vocabularies (e.g., identical tag names with different meanings), **XML namespaces** are used.

------

##### **Examples of Multiple Vocabularies in a Single XML Document**

1. **Integrating SVG (Scalable Vector Graphics) with XHTML**:

   - XHTML is a vocabulary for structuring web documents.
   - SVG is a vocabulary for defining graphics.

   Example:

   ```xml
   <html xmlns="http://www.w3.org/1999/xhtml"
         xmlns:svg="http://www.w3.org/2000/svg">
       <head>
           <title>Embedding SVG</title>
       </head>
       <body>
           <h1>Example</h1>
           <svg:svg width="100" height="100">
               <svg:circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red"/>
           </svg:svg>
       </body>
   </html>
   ```

   **Explanation**:

   - The `xmlns="http://www.w3.org/1999/xhtml"` declares the default XHTML vocabulary.
   - The `xmlns:svg="http://www.w3.org/2000/svg"` declares the SVG vocabulary.
   - The `<svg:svg>` element uses the `svg` prefix to include graphics within an XHTML document.

2. **SOAP Message Using XML Schema Definition (XSD)**:

   - SOAP is a vocabulary for messaging protocols.
   - XSD is a vocabulary for data types and validation.

   Example:

   ```xml
   <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"
                  xmlns:xsd="http://www.w3.org/2001/XMLSchema">
       <soap:Body>
           <Request>
               <xsd:string>Hello, World!</xsd:string>
           </Request>
       </soap:Body>
   </soap:Envelope>
   ```

   **Explanation**:

   - The `soap` namespace defines SOAP-specific elements like `<Envelope>` and `<Body>`.
   - The `xsd` namespace defines a string data type used in the `<xsd:string>` element.

------

##### **Popular XML Vocabularies**

1. **XHTML (Extensible HyperText Markup Language)**

   - Used for structuring and presenting content on the web.

   - Namespace: `http://www.w3.org/1999/xhtml`

   - Example:

     ```xml
     <html xmlns="http://www.w3.org/1999/xhtml">
         <head><title>Example</title></head>
         <body><h1>Welcome!</h1></body>
     </html>
     ```

2. **SVG (Scalable Vector Graphics)**

   - Used for defining vector-based graphics.

   - Namespace: `http://www.w3.org/2000/svg`

   - Example:

     ```xml
     <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100">
         <circle cx="50" cy="50" r="40" fill="blue"/>
     </svg>
     ```

3. **SOAP (Simple Object Access Protocol)**

   - Used for messaging and web service communication.

   - Namespace: `http://schemas.xmlsoap.org/soap/envelope/`

   - Example:

     ```xml
     <soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
         <soap:Body>
             <message>Hello, World!</message>
         </soap:Body>
     </soap:Envelope>
     ```

4. **XSLT (Extensible Stylesheet Language Transformations)**

   - Used for transforming XML documents into other formats like HTML, plain text, or other XML structures.

   - Namespace: `http://www.w3.org/1999/XSL/Transform`

   - Example:

     ```xml
     <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
         <xsl:template match="/">
             <html>
                 <body>
                     <h1>Transformed XML</h1>
                 </body>
             </html>
         </xsl:template>
     </xsl:stylesheet>
     ```

5. **Dublin Core**

   - Used for metadata descriptions of resources (e.g., books, documents).

   - Namespace: `http://purl.org/dc/elements/1.1/`

   - Example:

     ```xml
     <metadata xmlns:dc="http://purl.org/dc/elements/1.1/">
         <dc:title>XML Vocabulary</dc:title>
         <dc:creator>John Doe</dc:creator>
     </metadata>
     ```

------

##### **Why Use Multiple Vocabularies?**

- **Interoperability**: Combine features from different domains (e.g., HTML and SVG for web applications).
- **Reusability**: Use existing, standardized vocabularies instead of reinventing the wheel.
- **Separation of Concerns**: Keep functionality modular, each vocabulary handling a specific aspect of the document.

By utilizing XML namespaces, developers can combine these vocabularies in a single document without worrying about conflicts. This capability makes XML a powerful tool for complex applications.

_____________________

**Financial industry**, including **capital markets** and **banking**, heavily relies on XML-based vocabularies for standardization, interoperability, and efficient data exchange. These XML vocabularies facilitate seamless communication among financial institutions, regulatory bodies, and market participants.

Key XML vocabularies used in the financial industry (Good to know , one needs to be expert , good to have some idea where and how it's getting used):

------

##### **1. FpML (Financial products Markup Language)** (https://www.isda.org/isda-solutions-infohub/fpml)

- **Purpose**: Standardized format for over-the-counter (OTC) derivatives, including interest rate swaps, credit derivatives, and equity derivatives.

- Used In

  :

  - Trade confirmations.
  - Risk analysis.
  - Regulatory reporting.

- **Namespace**: `http://www.fpml.org`

- Example

  :

  ```xml
  <fpml xmlns="http://www.fpml.org/FpML-5/confirmation">
      <trade>
          <tradeHeader>
              <partyId>BankA</partyId>
              <tradeDate>2024-11-27</tradeDate>
          </tradeHeader>
          <product>
              <interestRateSwap>
                  <fixedRate>5.0%</fixedRate>
                  <floatingRate>LIBOR</floatingRate>
              </interestRateSwap>
          </product>
      </trade>
  </fpml>
  ```

------

##### **2. ISO 20022** (https://www.iso20022.org/)

- **Purpose**: A global standard for financial messaging used in payments, securities, trade finance, and foreign exchange.

- Used In

  :

  - Payment transactions (e.g., SWIFT messages like MT to MX migration).
  - Securities settlement and reconciliation.
  - Corporate-to-bank communications.

- **Namespace**: `urn:iso:std:iso:20022:tech:xsd:<messageType>`

- Example (Payment Instruction - pacs.008):

  ```xml
  <Document xmlns="urn:iso:std:iso:20022:tech:xsd:pacs.008.001.02">
      <FIToFICstmrCdtTrf>
          <GrpHdr>
              <MsgId>ABC123</MsgId>
              <CreDtTm>2024-11-27T10:00:00</CreDtTm>
          </GrpHdr>
          <CdtTrfTxInf>
              <PmtId>
                  <InstrId>INSTR123</InstrId>
              </PmtId>
              <Dbtr>
                  <Nm>John Doe</Nm>
              </Dbtr>
              <Cdtr>
                  <Nm>Jane Smith</Nm>
              </Cdtr>
              <IntrBkSttlmAmt Ccy="USD">1000.00</IntrBkSttlmAmt>
          </CdtTrfTxInf>
      </FIToFICstmrCdtTrf>
  </Document>
  ```

------

##### **3. FIXML (Financial Information Exchange Markup Language)**

- **Purpose**: XML-based version of the FIX protocol, used for real-time trade communication, order routing, and execution in capital markets.

- Used In

  :

  - Equity and fixed-income trading.
  - Post-trade processes like allocation and settlement.

- **Namespace**: `http://www.fixprotocol.org/FIXML`

- Example

  :

  ```xml
  <FIXML xmlns="http://www.fixprotocol.org/FIXML-5-0-SP2">
      <Order ID="12345" Side="1" TmInForce="0" Typ="2" Px="100.50" Qty="100">
          <Instrmt Sym="AAPL"/>
      </Order>
  </FIXML>
  ```

------

##### **4. XBRL (eXtensible Business Reporting Language)**

- **Purpose**: Standardized format for business and financial reporting, including tax filings and financial statements.

- Used In

  :

  - Regulatory reporting (e.g., **SEC filing**s in the US).
  - Corporate financial disclosures.

- **Namespace**: `http://www.xbrl.org`

- Example

  :

  ```xml
  <xbrl xmlns="http://www.xbrl.org/2003/instance">
      <context id="current_period">
          <entity>
              <identifier scheme="http://www.sec.gov">123456789</identifier>
          </entity>
          <period>
              <startDate>2024-01-01</startDate>
              <endDate>2024-12-31</endDate>
          </period>
      </context>
      <item name="Revenue" contextRef="current_period" unitRef="USD">1000000</item>
  </xbrl>
  ```

------

##### **5. ACORD XML** (https://www.acord.org/standards-architecture/acord-data-standards)

- **Purpose**: Used in insurance and financial services for data exchange and interoperability.

- Used In

  :

  - Life insurance policies.
  - Annuities and claims processing.
  - Integration between insurers and banks.

- **Namespace**: `http://www.acord.org`

- Example

  :

  ```xml
  <Policy xmlns="http://www.acord.org">
      <PolicyNumber>123456</PolicyNumber>
      <PolicyHolder>
          <Name>John Doe</Name>
      </PolicyHolder>
      <Premium>500.00</Premium>
  </Policy>
  ```

------

##### **6. SWIFT MX (https://www.swift.com/**) 

- **Purpose**: XML-based messaging standard by SWIFT for global financial transactions.

- Used In

  :

  - Payment instructions and confirmations.
  - Securities settlement.

- **Namespace**: `urn:swift:xsd:<messageType>`

- Example (SWIFT MX Message - Payment Initiation):

  ```xml
  <Document xmlns="urn:swift:xsd:pain.001.001.03">
      <CstmrCdtTrfInitn>
          <GrpHdr>
              <MsgId>Message123</MsgId>
              <CreDtTm>2024-11-27T10:00:00</CreDtTm>
          </GrpHdr>
          <PmtInf>
              <Dbtr>
                  <Nm>John Doe</Nm>
              </Dbtr>
              <Cdtr>
                  <Nm>Jane Smith</Nm>
              </Cdtr>
              <Amt Ccy="EUR">1500.00</Amt>
          </PmtInf>
      </CstmrCdtTrfInitn>
  </Document>
  ```

------

##### **7. DTCC XML (https://www.dtcc.com/**)

- **Purpose**: Used by the Depository Trust & Clearing Corporation (DTCC) for trade processing, settlement, and corporate actions in the US securities market.

- Used In

  :

  - Trade matching and reporting.
  - Corporate actions processing.

- **Namespace**: `http://www.dtcc.com/xml`

- Example

  :

  ```xml
  <Trade xmlns="http://www.dtcc.com/xml">
      <TradeID>78910</TradeID>
      <Security>
          <Symbol>MSFT</Symbol>
          <ISIN>US5949181045</ISIN>
      </Security>
      <Quantity>1000</Quantity>
      <Price>250.00</Price>
  </Trade>
  ```

------

- ```xml
  <Document xmlns="urn:iso:std:iso:20022:tech:xsd:pain.001.001.03">
      <CstmrCdtTrfInitn>
          <PmtInf>
              <Cdtr>
                  <Nm>John Doe</Nm>
              </Cdtr>
              <CdtrAcct>
                  <Id>
                      <IBAN>DE89370400440532013000</IBAN>
                  </Id>
              </CdtrAcct>
              <Amt>
                  <InstdAmt Ccy="EUR">100.00</InstdAmt>
              </Amt>
          </PmtInf>
      </CstmrCdtTrfInitn>
  </Document>
  ```

------

#### **Summary**

| **Vocabulary** | **Purpose**                      | **Primary Domain**                                           |
| -------------- | -------------------------------- | ------------------------------------------------------------ |
| **FpML**       | OTC derivatives                  | Capital Markets                                              |
| **ISO 20022**  | Financial messaging              | Banking and Securities                                       |
| **FIXML**      | Trade communication              | Trading and Execution  (https://en.wikipedia.org/wiki/Financial_Information_eXchange) |
| **XBRL**       | Business and financial reporting | Regulatory Reporting                                         |
| **ACORD**      | Insurance and financial services | Insurance and Banking                                        |
| **SWIFT MX**   | Global financial transactions    | Payments and Securities                                      |
| **DTCC XML**   | US securities trade processing   | Post-Trade Processing                                        |
|                |                                  |                                                              |

## **XML Document Validation**

Validating an XML document ensures that it conforms to a predefined structure and rules, defined by a schema or a document type definition (DTD). Validation can be done using:

1. XML Schema Definition (XSD)
   - A powerful way to define the structure, content, and data types of XML documents.
2. Document Type Definition (DTD)
   - An older and simpler method for defining the structure and legal elements/attributes.
3. Relax NG
   - A simpler and more readable alternative to XSD for certain use cases.

------

##### **Steps to Validate an XML Document**

###### **1. Using XML Schema Definition (XSD)**

**Sample XML Document (`example.xml`):**

```
<bookstore xmlns="http://example.com/books" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://example.com/books bookstore.xsd">
    <book>
        <title>XML Basics</title>
        <author>John Doe</author>
        <price>29.99</price>
    </book>
</bookstore>
```

The XML document  contains three important attributes on the `<bookstore>` element: **`xmlns`**, **`xmlns:xsi`**, and **`xsi:schemaLocation`**. Each of these attributes plays a role in defining the XML's namespace information and linking the XML document to an associated schema for validation. Let's break down each one:

1. **`xmlns="http://example.com/books"`** (Default Namespace):

   - **`xmlns`** stands for **XML Namespace** and is used to declare the **default namespace** for the elements in the XML document.
   - **`xmlns="http://example.com/books"`** declares that all elements within the `<bookstore>` document are associated with the namespace `http://example.com/books`.
   - This means that `<bookstore>`, `<book>`, `<title>`, `<author>`, and `<price>` all belong to this namespace.
   - Declaring a default namespace allows you to use these elements without a prefix, which makes the XML easier to read and write.
   - The default namespace ensures that the elements are uniquely identified, avoiding conflicts if the XML document includes elements from different vocabularies.

2. **`xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`** (XML Schema Instance Namespace):

   - **`xmlns:xsi`** defines a **namespace prefix** called `xsi`, which refers to the XML Schema Instance vocabulary.
   - **`"http://www.w3.org/2001/XMLSchema-instance"`** is a standard namespace URI that provides a set of attributes used in XML Schema validation.
   - The `xsi` prefix is commonly used to declare attributes such as `schemaLocation` and `noNamespaceSchemaLocation`, which are essential for specifying the schema to be used for validation.
   - This namespace does not change the content of the XML, but rather provides metadata to indicate how the XML should be validated.

3. **`xsi:schemaLocation="http://example.com/books bookstore.xsd"`** (Schema Location):

   - **`xsi:schemaLocation`** is an attribute used to specify the **location of the XML Schema** that should be used to validate this XML document.

   - The value of 

     ```
     xsi:schemaLocation
     ```

      contains 

     two parts

     :

     1. **Namespace URI** (`http://example.com/books`): This is the namespace that the XML elements are associated with.
     2. **Schema File Location** (`bookstore.xsd`): This specifies the location of the schema file that defines the structure and rules for elements in the namespace. In this case, the schema is called `bookstore.xsd`.

   - The **schemaLocation** attribute tells the XML parser that elements in the namespace `http://example.com/books` should be validated against the rules defined in `bookstore.xsd`.

   - This allows the parser to validate the structure, data types, and constraints of the XML elements as defined in the schema file.

###### How the Attributes Work Together:

- **`xmlns`** sets the default namespace for the XML document, meaning that all elements belong to the `http://example.com/books` namespace.
- **`xmlns:xsi`** introduces the XML Schema Instance namespace, which provides the mechanism to specify schema-related attributes.
- **`xsi:schemaLocation`** links the elements in the `http://example.com/books` namespace to the schema file (`bookstore.xsd`) for validation.

###### Example Summary:

- The **default namespace** (`xmlns="http://example.com/books"`) applies to all elements in the document, meaning `<bookstore>`, `<book>`, `<title>`, etc., belong to this namespace.
- The **XML Schema Instance** namespace (`xmlns:xsi`) provides attributes that are used to reference a schema.
- The **`xsi:schemaLocation`** attribute tells the XML processor where to find the schema (`bookstore.xsd`) that defines the structure and rules for the elements belonging to the `http://example.com/books` namespace.

**Sample XSD File (`bookstore.xsd`):**

```
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" targetNamespace="http://example.com/books" xmlns="http://example.com/books" elementFormDefault="qualified">
    <xs:element name="bookstore">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="book" maxOccurs="unbounded">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="title" type="xs:string"/>
                            <xs:element name="author" type="xs:string"/>
                            <xs:element name="price" type="xs:decimal"/>
                        </xs:sequence>
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

**Steps**:

1. Include the `xsi:schemaLocation` attribute in the XML document to point to the XSD file.
2. Use a parser or validation tool to validate the XML against the XSD.

------

##### **2. Using Document Type Definition (DTD)**

**Sample XML Document (`example.xml`):**

```
<?xml version="1.0"?>
<!DOCTYPE bookstore SYSTEM "bookstore.dtd">
<bookstore>
    <book>
        <title>XML Basics</title>
        <author>John Doe</author>
        <price>29.99</price>
    </book>
</bookstore>
```

**Sample DTD File (`bookstore.dtd`):**

```
<!ELEMENT bookstore (book+)>
<!ELEMENT book (title, author, price)>
<!ELEMENT title (#PCDATA)>
<!ELEMENT author (#PCDATA)>
<!ELEMENT price (#PCDATA)>
```

**Steps**:

1. Declare the DTD using the `DOCTYPE` declaration.
2. Validate the XML document against the DTD using an XML parser or tool.

# **DTD**

##### What is DTD (Document Type Definition)?

**DTD** stands for **Document Type Definition**, and it is used to define the structure and the rules of an XML document. DTD specifies: 

1. **Elements** that can appear in the document.
2. **Attributes** for the elements.
3. The **order** and **nesting** of the elements.
4. Whether elements are optional or required.
5. Here is the DTD for the XHTML - https://www.w3.org/TR/xhtml1/dtds.html (Define all the elements that can be used in HTML) 

**Example Use Case**: Imagine you are creating an XML document to store information about books. To ensure that every XML document has the correct structure (e.g., each book has a title, author, and publication year), you can define a DTD.

##### Two Types of DTD:

1. **Internal DTD**: Defined within the XML document itself.
2. **External DTD**: Defined in a separate file and referenced from the XML document.

##### Example of Internal DTD

```xml
<?xml version="1.0"?>
<!DOCTYPE books [
    <!ELEMENT books (book+)>
    <!ELEMENT book (title, author, year)>
    <!ELEMENT title (#PCDATA)>
    <!ELEMENT author (#PCDATA)>
    <!ELEMENT year (#PCDATA)>
]>
<books>
    <book>
        <title>Clean Code</title>
        <author>Robert C. Martin</author>
        <year>2008</year>
    </book>
    <book>
        <title>Introduction to Algorithms</title>
        <author>Thomas H. Cormen</author>
        <year>2009</year>
    </book>
</books>
```

**Explanation**:

- `<!DOCTYPE books [...]>`: Declares the DTD for the XML document.
- `<!ELEMENT books (book+)>`: Defines that the `books` element must contain one or more `book` elements.
- `<!ELEMENT book (title, author, year)>`: Defines that a `book` element must have `title`, `author`, and `year` elements in that order.
- `<!ELEMENT title (#PCDATA)>`: Defines that `title` contains parsed character data (text content).

##### Example of External DTD

**books.dtd**:

```xml
<!ELEMENT books (book+)>
<!ELEMENT book (title, author, year)>
<!ELEMENT title (#PCDATA)>
<!ELEMENT author (#PCDATA)>
<!ELEMENT year (#PCDATA)>
```

**XML Document**:

```xml
<?xml version="1.0"?>
<!DOCTYPE books SYSTEM "books.dtd">
<books>
    <book>
        <title><![CDATA[The Pragmatic Programmer! One of the must read books for all software engineers]]</title>
        <author>Andrew Hunt</author>
        <year>1999</year>
    </book>
</books>
```

```xml
<?xml version="1.0"?>
<!DOCTYPE books SYSTEM "books.dtd">
<books>
    <book>
        <title>The Pragmatic Programmer</title>
        <author>Andrew Hunt</author>
        <year>1999</year>
    </book>
</books>
```

**Explanation**:

- The XML document references an external DTD file (`books.dtd`).
- This approach is useful if you want to use the same DTD for multiple XML documents.
- There ate two separate XML documents one is using CDATA section in the title element even it's specified to with #PCDATA element

In **DTD (Document Type Definition)**, you cannot define explicit data types like integers, floats, or dates as you can in XML Schema (XSD). DTD only supports a limited set of content types for elements, which are more about structure and character data rather than specific data types.

###### Types of Data in DTD

1. **Element Content Types** DTD defines the content type of an element based on the kind of data it can contain:

   | Content Type | Description                                                  | Example                            |
   | ------------ | ------------------------------------------------------------ | ---------------------------------- |
   | `#PCDATA`    | Parsed character data (text content).                        | `<title>Clean Code</title>`        |
   | `CDATA`      | Unparsed character data (raw text, less common).             | `<code><![CDATA[<html>]]></code>`  |
   | EMPTY        | Element contains no content (self-closing).                  | `<lineBreak/>`                     |
   | ANY          | Element can contain any content, including child elements, text, or a combination of both. | `<content>Anything here</content>` |

2. **Attribute Data Types** For attributes, DTD offers some basic attribute types:

   | Attribute Type | Description                                                  | Example                                                 |
   | -------------- | ------------------------------------------------------------ | ------------------------------------------------------- |
   | `CDATA`        | Character data (default for attributes).                     | `<book title="Clean Code"/>`                            |
   | `ID`           | Unique identifier for an element within the document.        | `<book id="B001"/>`                                     |
   | `IDREF`        | Reference to another element's ID.                           | `<author id="A001"/><book author="A001"/>`              |
   | `IDREFS`       | Multiple references to IDs (space-separated).                | `<book authors="A001 A002"/>`                           |
   | `ENTITY`       | Reference to an external entity.                             | `<doc system="systemID"/>`                              |
   | `ENTITIES`     | Multiple ENTITY references.                                  | `<images src="img1 img2 img3"/>`                        |
   | `NMTOKEN`      | A single token (alphanumeric string with no spaces).         | `<book genre="fiction"/>`                               |
   | `NMTOKENS`     | Multiple tokens (space-separated).                           | `<book keywords="technology programming development"/>` |
   | `NOTATION`     | Refers to a predefined notation type, often for multimedia or file format references. | `<media type="video/mp4"/>`                             |

3. **Element Content Models** DTD uses **content models** to describe the **structure and hierarchy** of elements.

   | Content Model      | Description                                              | Example                                        |
   | ------------------ | -------------------------------------------------------- | ---------------------------------------------- |
   | `(child1, child2)` | Specifies an exact sequence of child elements.           | `<book><title/><author/></book>`               |
   | `(child1           | child2)`                                                 | Specifies a choice between child elements.     |
   | `(child1*)`        | Specifies zero or more occurrences of the child element. | `<authors><author/><author/>...</authors>`     |
   | `(child1?)`        | Specifies zero or one occurrence of the child element.   | `<publisher><address/></publisher>`            |
   | `(child1+)`        | Specifies one or more occurrences of the child element.  | `<chapters><chapter/><chapter/>...</chapters>` |

   Based on the content models provided in your description, I'll create sample XML payloads and corresponding DTD schemas for each content model type. Each example below demonstrates the use of a specific content model in both the XML payload and DTD.

   ###### 1. Content Model: `(child1, child2)`

   **Description**: Specifies an exact sequence of child elements.

   ###### XML Payload

   ```xml
   <book>
       <title>XML Fundamentals</title>
       <author>Jane Doe</author>
   </book>
   ```

   ###### DTD Schema

   ```xml
   <!ELEMENT book (title, author)>
   <!ELEMENT title (#PCDATA)>
   <!ELEMENT author (#PCDATA)>
   ```

   ###### 2. Content Model: `(child1 | child2)`

   **Description**: Specifies a choice between child elements.

   ###### XML Payload - Example 1

   ```xml
   <item>
       <magazine>Tech Today</magazine>
   </item>
   ```

   ###### XML Payload - Example 2

   ```xml
   <item>
       <book>Learning XML</book>
   </item>
   ```

   ###### DTD Schema

   ```xml
   <!ELEMENT item (book | magazine)>
   <!ELEMENT book (#PCDATA)>
   <!ELEMENT magazine (#PCDATA)>
   ```

   ###### 3. Content Model: `(child1*)`

   **Description**: Specifies zero or more occurrences of the child element.

   ###### XML Payload

   ```xml
   <authors>
       <author>John Doe</author>
       <author>Jane Smith</author>
       <author>Emily Johnson</author>
   </authors>
   ```

   ###### DTD Schema

   ```xml
   <!ELEMENT authors (author*)>
   <!ELEMENT author (#PCDATA)>
   ```

   ###### 4. Content Model: `(child1?)`

   **Description**: Specifies zero or one occurrence of the child element.

   ###### XML Payload - Example 1 (with child element)

   ```xml
   <publisher>
       <address>123 Publisher Lane, Booktown</address>
   </publisher>
   ```

   ###### XML Payload - Example 2 (without child element)

   ```xml
   <publisher>
   </publisher>
   ```

   ###### DTD Schema

   ```xml
   <!ELEMENT publisher (address?)>
   <!ELEMENT address (#PCDATA)>
   ```

   ###### 5. Content Model: `(child1+)`

   **Description**: Specifies one or more occurrences of the child element.

   ###### XML Payload

   ```xml
   <chapters>
       <chapter>Introduction to XML</chapter>
       <chapter>DTD Basics</chapter>
       <chapter>Advanced XML Techniques</chapter>
   </chapters>
   ```

   ###### DTD Schema

   ```xml
   <!ELEMENT chapters (chapter+)>
   <!ELEMENT chapter (#PCDATA)>
   ```

   ##### Summary

   - **`(child1, child2)`**: Use when elements should appear in a specific sequence.
   - **`(child1 | child2)`**: Use when there is a choice between elements.
   - **`(child1*)`**: Use when an element can occur zero or more times.
   - **`(child1?)`**: Use when an element is optional and can occur zero or one time.
   - **`(child1+)`**: Use when an element should appear one or more times.

###### Example of DTD with Content and Attributes

**DTD:**

```xml
<!ELEMENT book (title, author, price)>
<!ELEMENT title (#PCDATA)>
<!ELEMENT author (#PCDATA)>
<!ELEMENT price (#PCDATA)>

<!ATTLIST book
    id ID #REQUIRED
    genre CDATA #IMPLIED>
```

**`<!ATTLIST book ...>`**: This is used to define attributes that are allowed for the `book` element.

**`id ID #REQUIRED`**: The attribute `id` is of type `ID` and is required, meaning every `<book>` element must have a unique `id` attribute.

**`genre CDATA #IMPLIED`**:

- **`genre`**: The attribute name.
- **`CDATA`**: The type of the attribute, which stands for character data. It means that the value can be any character data, essentially a string.
- **`#IMPLIED`**: This means that the `genre` attribute is **optional**. If it is omitted in the XML document, the document will still be considered valid. The XML parser does not require a value for `genre`, and there is no default value assigned to it.

**XML Document Validated by the Above DTD:**

```xml
<book id="B001" genre="programming">
    <title>Clean Code</title>
    <author>Robert C. Martin</author>
    <price>29.99</price>
</book>
```



One can use `CDATA` for elements in XML, but not directly in a DTD definition. In XML documents, you can use a **CDATA section** to contain literal text that should not be parsed by the XML parser, such as special characters (`<`, `>`, `&`), without needing to escape them.

Here’s a summary of how CDATA works:

- In **XML**, you can use a **CDATA section** within an element to include character data that you don't want the parser to interpret.
- In a **DTD**, however, you cannot define an element as directly of type `CDATA`. Instead, you define an element that contains **parsed character data** (`#PCDATA`), which means the element can hold text, including CDATA sections.

###### Example of Using CDATA in XML:

Let’s look at how CDATA sections are used in an XML document to store text that should not be parsed.

###### XML Example

```xml
<book>
    <title>Learning XML</title>
    <author>Jane Doe</author>
    <description><![CDATA[This book provides an in-depth guide to XML. Use < or > symbols freely here!]]></description>
</book>
```

- **`<![CDATA[ ... ]]>`**: This is a CDATA section. The XML parser will treat everything inside as literal text without trying to interpret or parse any XML tags or special characters.
- The `<description>` element contains a CDATA section to prevent the parser from interpreting special characters like `<` and `>`.

###### Corresponding DTD Schema:

In the DTD, you define such elements using `#PCDATA` to indicate that the element can contain character data.

###### DTD Example

```xml
<!ELEMENT book (title, author, description)>
<!ELEMENT title (#PCDATA)>
<!ELEMENT author (#PCDATA)>
<!ELEMENT description (#PCDATA)>
```

In this DTD:

- **`#PCDATA`** stands for **parsed character data**, which means the element can contain text, including characters and data from CDATA sections.

###### Summary:

- **CDATA Section in XML**: You use `<![CDATA[ ... ]]>` inside an element to include text that should not be interpreted by the XML parser.
- **DTD Definition**: You cannot directly declare an element as `CDATA` in a DTD. Instead, you use `#PCDATA` to indicate that an element can contain character data, which can include CDATA sections.

**Example Usage:**

- If you want to store unparsed text (including special characters) in an XML element, use a **CDATA section** in the XML.
- In the **DTD**, declare that element as containing `#PCDATA`.

This approach allows you to have flexibility in storing text data, including special symbols, in the XML document.

###### Limitations of DTD Data Types:

- No support for **numeric data types** like integer, float, etc.
- No support for complex data types (e.g., date, boolean).
- No validation for the content of `#PCDATA`—all text is allowed without type checking.
- Does not support namespaces.

For more robust data type definitions, **XML Schema (XSD)** is preferred. Would you like a comparison of DTD and XSD, or more examples of specific DTD definitions?

###### Why Use DTD?

- **Validation**: Ensures the XML document follows a specific structure, making it easier to parse and understand.
- **Consistency**: Helps maintain uniformity across multiple XML documents.

###### Limitations of DTD:

- DTD only supports basic data types (like text).
- It doesn't support namespaces, making it less useful for more complex XML documents.
- XML Schema (XSD) is often preferred for more advanced validation.

------

##### **Steps to Validate XML Against a DTD:**

1. Create a **DTD** file that defines the structure of the XML.
2. Create an **XML document** that conforms to the DTD.
3. Write a **Java program** to validate the XML against the DTD using the `javax.xml.validation` API.

------

##### 1. **Sample DTD File (employee.dtd)**:

```xml
<!ELEMENT employee (name, age, position)>
<!ELEMENT name (#PCDATA)>
<!ELEMENT age (#PCDATA)>
<!ELEMENT position (#PCDATA)>
<!ATTLIST employee id ID #REQUIRED>
```

This DTD:

- Defines an `employee` element with `name`, `age`, and `position` as child elements.
- Specifies that `employee` must have an `id` attribute of type `ID`.

------

##### 2. **Sample XML File (employee-using-dtd.xml)**:

```xml
<?xml version="1.0"?>
<!DOCTYPE employee SYSTEM "employee.dtd">
<employee id="E101">
    <name>John Doe</name>
    <age>30</age>
    <position>Software Engineer</position>
</employee>
```

This XML:

- References the DTD (`employee.dtd`) using the `SYSTEM` keyword.
- Contains data about an employee that conforms to the DTD.

------

##### 3. **Java Code to Validate XML Against DTD**:

```java
// We shouldn't be using system out to log messages 

import org.xml.sax.ErrorHandler;
import org.xml.sax.SAXException;
import org.xml.sax.SAXParseException;

public class DocumentErrorHandler implements ErrorHandler {

    private boolean isValid = true;

    public void warning(SAXParseException exception) throws SAXException {
        System.out.println("Warning: " + exception.getMessage());
    }

    @Override
    public void error(SAXParseException exception) throws SAXException {
        System.out.println("Error: " + exception.getMessage());
        isValid = false;
    }

    @Override
    public void fatalError(SAXParseException exception) throws SAXException {
        System.out.println("Fatal error: " + exception.getMessage());
        isValid = false;
    }

    public boolean isValid() {
        return isValid;
    }
}


import org.w3c.dom.Document;
import org.xml.sax.SAXException;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import java.io.File;

public class XMLValidatorWithDTD {
    public static void main(String[] args) {

        try {
            // 1. Create a DocumentBuilderFactory
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();

            // 2. Enable validation and DTD processing
            factory.setValidating(true);
            factory.setNamespaceAware(false); // DTD doesn't use namespaces

            // 3. Create a DocumentBuilder
            DocumentBuilder builder = factory.newDocumentBuilder();


            // 4. Set an ErrorHandler to capture validation errors
            DocumentErrorHandler errorHandler = new DocumentErrorHandler();

            builder.setErrorHandler(errorHandler);

            // project home 
            File projectHome = new File(System.getProperty("user.dir"));

            // 5. Parse the XML file (employee.xml)
            File xmlFile = new File(projectHome.getAbsolutePath()+"/src/main/resources/employee-using-dtd.xml");
            Document doc = builder.parse(xmlFile);

            if (!errorHandler.isValid()) {
                System.out.println("Error validating XML");
            }

            // If no exception, XML is valid
        } catch (SAXException e) {
            System.out.println("Validation failed: " + e.getMessage());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

------

##### 4. **How It Works**:

1. **DocumentBuilderFactory**:
   - Creates a parser that understands DTD validation.
2. **Validation Enabled**:
   - `factory.setValidating(true)` ensures the XML is validated against the referenced DTD.
3. **Error Handling**:
   - Custom `ErrorHandler` captures warnings, errors, and fatal errors during validation.
4. **Parse and Validate**:
   - If the XML conforms to the DTD, the program prints: `"The XML file is valid."`
   - Otherwise, it prints validation errors.

------

##### 5. **Example Output**:

###### Valid XML:

If `employee.xml` matches `employee.dtd`, the output is:

```
The XML file is valid.
```

###### Invalid XML:

If the XML is invalid (e.g., missing the `id` attribute), the output might be:

```
Error: Attribute "id" must be declared for element type "employee".
```

------

## **XML Schema**

In **XML Schema Definition (XSD)**, there is a rich set of **built-in data types** to validate and enforce constraints on XML document content. These types are divided into:

1. **Primitive Data Types**: Basic types like strings, numbers, and dates.
2. **Derived Data Types**: More specific types based on primitive types.

###### 1. **Primitive Data Types**

These are the basic, predefined data types in XSD.

| Data Type         | Description                                      | Example                 |
| ----------------- | ------------------------------------------------ | ----------------------- |
| `xs:string`       | Represents text content                          | `"Hello World"`         |
| `xs:boolean`      | Represents `true` or `false` values              | `true`, `false`         |
| `xs:decimal`      | Represents decimal numbers                       | `123.45`, `-456.78`     |
| `xs:integer`      | Represents whole numbers (positive/negative)     | `42`, `-99`             |
| `xs:float`        | Represents floating-point numbers                | `3.14`, `-0.001`        |
| `xs:double`       | Represents double-precision numbers              | `1.23456789E10`         |
| `xs:date`         | Represents a calendar date (YYYY-MM-DD)          | `2024-11-17`            |
| `xs:time`         | Represents a time (HH:MM:SS)                     | `14:30:00`              |
| `xs:dateTime`     | Represents a date and time (YYYY-MM-DDTHH:MM:SS) | `2024-11-17T14:30:00`   |
| `xs:duration`     | Represents a time duration                       | `P1Y2M3DT4H5M6S`        |
| `xs:base64Binary` | Represents binary data in Base64 encoding        | `"SGVsbG8="`            |
| `xs:anyURI`       | Represents a URI                                 | `"https://example.com"` |

###### 2. **Derived Data Types**

Derived types are based on the primitive types but have additional constraints.

| Data Type               | Description                                             | Example                |
| ----------------------- | ------------------------------------------------------- | ---------------------- |
| `xs:byte`               | 8-bit signed integer (-128 to 127)                      | `-128`, `127`          |
| `xs:short`              | 16-bit signed integer (-32,768 to 32,767)               | `-32768`, `32767`      |
| `xs:int`                | 32-bit signed integer (-2,147,483,648 to 2,147,483,647) | `12345`                |
| `xs:long`               | 64-bit signed integer                                   | `1234567890123`        |
| `xs:unsignedByte`       | 8-bit unsigned integer (0 to 255)                       | `255`                  |
| `xs:unsignedShort`      | 16-bit unsigned integer (0 to 65,535)                   | `65535`                |
| `xs:unsignedInt`        | 32-bit unsigned integer                                 | `4294967295`           |
| `xs:unsignedLong`       | 64-bit unsigned integer                                 | `18446744073709551615` |
| `xs:positiveInteger`    | Positive integer (greater than 0)                       | `1`, `100`             |
| `xs:negativeInteger`    | Negative integer (less than 0)                          | `-1`, `-100`           |
| `xs:nonPositiveInteger` | Integer less than or equal to 0                         | `0`, `-50`             |
| `xs:nonNegativeInteger` | Integer greater than or equal to 0                      | `0`, `50`              |

###### 3. **Example XML with XSD Schema Using Different Data Types**

###### **XSD Schema (example.xsd):**

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="person">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="name" type="xs:string"/>
                <xs:element name="age" type="xs:positiveInteger"/>
                <xs:element name="salary" type="xs:decimal"/>
                <xs:element name="isMarried" type="xs:boolean"/>
                <xs:element name="birthDate" type="xs:date"/>
                <xs:element name="website" type="xs:anyURI"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

###### **XML Document (example.xml):**

```xml
<person>
    <name>John Doe</name>
    <age>30</age>
    <salary>75000.50</salary>
    <isMarried>true</isMarried>
    <birthDate>1994-06-15</birthDate>
    <website>https://johndoe.com</website>
</person>
```

###### **Explanation**:

- `name` is a string.
- `age` must be a positive integer.
- `salary` is a decimal number.
- `isMarried` is a boolean (`true` or `false`).
- `birthDate` must follow the `YYYY-MM-DD` format.
- `website` must be a valid URI.

##### **Why Use XSD Data Types?**

- **Validation**: Ensures that the data in XML documents is of the correct type.
- **Consistency**: Helps maintain consistent data across different XML files.
- **Readability**: Makes it clear what kind of data each element or attribute should contain.

###### **XML Schema Using Derived Data Types**

Let’s create an **XML Schema (XSD)** using various **derived data types** such as `xs:byte`, `xs:positiveInteger`, `xs:unsignedShort`, and others. We will then create an XML document that conforms to this schema.

###### **XML Schema (schema.xsd)**

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

    <!-- Root element: employee -->
    <xs:element name="employee">
        <xs:complexType>
            <xs:sequence>
                <!-- Derived Data Types -->
                <xs:element name="id" type="xs:unsignedInt"/>
                <xs:element name="name" type="xs:string"/>
                <xs:element name="age" type="xs:byte"/> <!-- Range: -128 to 127 -->
                <xs:element name="experience" type="xs:positiveInteger"/> <!-- Must be greater than 0 -->
                <xs:element name="salary" type="xs:decimal"/>
                <xs:element name="rating" type="xs:unsignedByte"/> <!-- Range: 0 to 255 -->
                <xs:element name="bonusPercentage" type="xs:unsignedShort"/> <!-- Range: 0 to 65535 -->
                <xs:element name="employmentStatus" type="xs:boolean"/>
                <xs:element name="joiningDate" type="xs:date"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>

</xs:schema>
```

###### **XML Document (employee.xml)**

This XML document conforms to the above schema.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<employee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:noNamespaceSchemaLocation="schema.xsd">
    <id>1024</id>
    <name>Jane Doe</name>
    <age>28</age>
    <experience>5</experience>
    <salary>85000.75</salary>
    <rating>120</rating>
    <bonusPercentage>10</bonusPercentage>
    <employmentStatus>true</employmentStatus>
    <joiningDate>2019-07-15</joiningDate>
</employee>
```

###### **Explanation:**

1. **id (`xs:unsignedInt`)**: An unsigned 32-bit integer, so it cannot be negative. Example value: `1024`.
2. **name (`xs:string`)**: A text value representing the employee's name.
3. **age (`xs:byte`)**: An 8-bit signed integer. Valid range: `-128` to `127`. Example value: `28`.
4. **experience (`xs:positiveInteger`)**: A positive integer (greater than 0). Example value: `5`.
5. **salary (`xs:decimal`)**: A decimal value. Example value: `85000.75`.
6. **rating (`xs:unsignedByte`)**: An 8-bit unsigned integer. Valid range: `0` to `255`. Example value: `120`.
7. **bonusPercentage (`xs:unsignedShort`)**: A 16-bit unsigned integer. Valid range: `0` to `65535`. Example value: `10`.
8. **employmentStatus (`xs:boolean`)**: A boolean value (`true` or `false`). Example value: `true`.
9. **joiningDate (`xs:date`)**: A date value in the format `YYYY-MM-DD`. Example value: `2019-07-15`.

###### **How to Validate:**

To check if the XML document conforms to the schema:

- Use an XML editor with schema validation support (e.g., XMLSpy, Visual Studio Code with an XML plugin).

- Run a command-line tool like (should be available on macOS)

  ```
  xmllint
  ```

   if you have it installed:

  ```bash
  xmllint --noout --schema schema.xsd employee.xml
  ```

###### **Steps to Validate XML Against an XSD:**

1. Create an **XSD** file that defines the structure of the XML.
2. Create an **XML document** that conforms to the XSD.
3. Write a **Java program** to validate the XML against the XSD using the `javax.xml.validation` API.

------

###### 1. **Sample XML Schema (employee.xsd)**:

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           elementFormDefault="qualified">

    <!-- Root element: employee -->
    <xs:element name="employee">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="name" type="xs:string"/>
                <xs:element name="age" type="xs:integer"/>
                <xs:element name="position" type="xs:string"/>
            </xs:sequence>
            <xs:attribute name="id" type="xs:ID" use="required"/>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

This schema:

- Defines an 

  ```
  employee
  ```

   element with child elements:

  - `name` (string),
  - `age` (integer), and
  - `position` (string).

- Requires the `employee` element to have an `id` attribute of type `ID`.

- The attribute `type="xs:ID"` is used to define the **type** of the attribute named `id` as an **ID**. 

  - **`xs:ID`**: This is a **built-in data type** in XML Schema (XSD) that represents a **unique identifier** within the XML document.
  
  - **Uniqueness**: The value assigned to an attribute of type `xs:ID` must be unique across the entire XML document. This means that no two elements can have the same `ID` value.
  
  - **Validation**: The `xs:ID` type is used for validation, ensuring that the value of the attribute conforms to the rules for an ID and is unique within the document.
  
  - In the example **`name="id"`**: Defines the attribute name, which is `"id"`. **`type="xs:ID"`**: Specifies that the `id` attribute is of type `xs:ID`, meaning its value must be unique across all elements in the XML document. This serves as a unique identifier for each `<employee>` element. **`use="required"`**: Indicates that the `id` attribute is **mandatory** for the `<employee>` element. Each `<employee>` must have an `id` attribute
  
    
  
    ***First line of XML Schema Definition (XSD) and contains several important attributes that define the structure and behavior of the schema. Let’s break down each part of the line:***
  
  - **`xs:schema`**:
  
    - This is the root element of the XSD document.
    - The prefix `xs` is commonly used to indicate elements and types defined by the XML Schema namespace.
    - The root element `<xs:schema>` contains all the elements, attributes, and type definitions for the schema.
  
  - **`xmlns:xs="http://www.w3.org/2001/XMLSchema"`**:
  
    - This attribute declares the **namespace** for the XML Schema Definition.
    - **`xmlns`** is a standard attribute used in XML to declare a namespace.
    - **`xs`** is a **namespace prefix** used throughout the schema to refer to the XML Schema elements.
    - **`http://www.w3.org/2001/XMLSchema`** is the **namespace URI** that uniquely identifies the XML Schema vocabulary. This URI tells the parser that the elements prefixed with `xs` are part of the XML Schema Definition language.
    - The prefix `xs` could technically be anything (e.g., `xsd`), but it is conventionally `xs` to make it easier to understand and maintain.
  
  - **`elementFormDefault="qualified"`**:
  
    - This attribute specifies the **qualification requirements** for the elements defined in the schema.
  
    - `elementFormDefault`
  
       can take one of two possible values:
  
      - **`qualified`**: This means that all the elements defined in the schema must be **namespace-qualified** in the XML documents. In other words, they must include the namespace prefix when used in an XML instance document.
      - **`unqualified`**: This means that elements defined in the schema do **not need to be namespace-qualified** when used in an XML instance document (they can be used without a prefix).
  
    - In this case, `elementFormDefault="qualified"` means that **all child elements** of the root element must be **qualified with the namespace**. This ensures that the elements are explicitly associated with the namespace declared in the schema.
  
    - ###### Example: Usage of `elementFormDefault="qualified"`
  
      Consider the following XML instance that uses an XSD schema with `elementFormDefault="qualified"`.
  
      ###### XML Instance Document:
  
      ```
      <bookstore xmlns="http://example.com/bookstore">
          <book>
              <title>XML Fundamentals</title>
              <author>Jane Doe</author>
          </book>
      </bookstore>
      ```
  
      - In the above example, **all elements** (`<bookstore>`, `<book>`, `<title>`, `<author>`) are qualified because they belong to the namespace `http://example.com/bookstore`.
      - This is required because of `elementFormDefault="qualified"` in the schema, meaning that these elements must explicitly belong to the declared namespace.
  
      ##### **Why Declare `xmlns="http://example.com/bookstore"` in the XSD?**
  
      1. ###### **Namespace Consistency**:
  
         - By declaring the default namespace (`xmlns="http://example.com/bookstore"`) in the XSD, you ensure that all elements defined within the schema automatically belong to the specified target namespace (`http://example.com/bookstore`).
         - This is crucial for XML instance documents that must comply with this schema, as it enforces **consistency** between the schema and the XML document.
  
      2. ###### **Simplified XML Instance Document**:
  
         - Without the default namespace declaration in the XSD (`xmlns="http://example.com/bookstore"`), you would need to use **qualified names** (prefixes) in both the XML Schema and the XML instance document.
         - Declaring the default namespace allows the XML document to be written without using prefixes, making it **simpler** and **easier to read**.
  
         For example, without the default namespace, the XML instance might look like this:
  
         ```
         <bookstore xmlns:bs="http://example.com/bookstore">
             <bs:book>
                 <bs:title>XML Fundamentals</bs:title>
                 <bs:author>Jane Doe</bs:author>
             </bs:book>
         </bookstore>
         ```
  
         - Using prefixes (`bs:`) adds complexity, which can be avoided by using a default namespace.
  
      3. **`elementFormDefault="qualified"`** and Default Namespace**:
  
         - Since `elementFormDefault="qualified"` is used, all child elements of the root must be **qualified** with a namespace.
         - By setting the default namespace to `http://example.com/bookstore`, you ensure that all elements in the XML document are automatically qualified, complying with the schema.
  
      ###### **Summary:**
  
      - **`xmlns="http://example.com/bookstore"`** declares the **default namespace** for the schema.
      - It ensures that all elements defined in the XSD and the XML instance document belong to the `http://example.com/bookstore` namespace.
      - It **simplifies the XML instance document** by removing the need for prefixes, while also ensuring consistency between the XML document and the schema.
      - Combined with `targetNamespace`, it allows all the elements defined by the XSD to be associated with the correct namespace and ensures that the XML documents are valid according to the schema's rules.
  
      ###### Corresponding XSD Schema:
  
      ```
      <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
                 targetNamespace="http://example.com/bookstore"
                 xmlns="http://example.com/bookstore"
                 elementFormDefault="qualified">
      
          <xs:element name="bookstore">
              <xs:complexType>
                  <xs:sequence>
                      <xs:element name="book" maxOccurs="unbounded">
                          <xs:complexType>
                              <xs:sequence>
                                  <xs:element name="title" type="xs:string"/>
                                  <xs:element name="author" type="xs:string"/>
                              </xs:sequence>
                          </xs:complexType>
                      </xs:element>
                  </xs:sequence>
              </xs:complexType>
          </xs:element>
      
      </xs:schema>
      ```
  
      - **`xmlns:xs="http://www.w3.org/2001/XMLSchema"`**: Declares the namespace for the XML Schema (`xs` is a prefix that refers to elements defined by XML Schema language).
      - **`targetNamespace="http://example.com/bookstore"`**:  Specifies the **namespace** that this schema is describing. It essentially means that all elements defined in this schema are part of the `http://example.com/bookstore` namespace. When an XML document wants to use this schema, the elements in that document must belong to this namespace.
      - **`xmlns="http://example.com/bookstore"`**: This declares the **default namespace** for the elements defined in the schema itself. By specifying this, the elements defined in the schema are automatically placed in the `http://example.com/bookstore` namespace **without requiring a prefix**. This allows the XML instance document to be simpler, without prefixes, since all elements within the document will belong to this namespace by default.
      - **`elementFormDefault="qualified"`**: Requires that all elements are qualified by the namespace when used in an XML instance.
  
      ###### Summary:
  
      - **`<xs:schema>`**: Defines the root element for an XSD document.
      - **`xmlns:xs="http://www.w3.org/2001/XMLSchema"`**: Declares the XML Schema namespace so that all elements prefixed with `xs` are recognized as part of XML Schema.
      - **`elementFormDefault="qualified"`**: Indicates that all child elements in the XML document must be qualified by a namespace. This ensures that the XML elements are explicitly associated with the declared schema's namespace.
  
      Using `elementFormDefault="qualified"` helps to **avoid conflicts** when elements from different schemas are used in the same XML document by requiring elements to be explicitly tied to their namespaces.
  
  


------

###### 2. **Sample XML File (employee-using-xsd.xml)**:

```xml
<?xml version="1.0"?>
<employee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:noNamespaceSchemaLocation="employee.xsd"
          id="E101">
    <name>John Doe</name>
    <age>30</age>
    <position>Software Engineer</position>
</employee>
```

- **`id="E101"`**: The `id` attribute is of type `xs:ID`, so it must be unique throughout the XML document. If there are multiple `<employee>` elements, each one must have a unique `id` value

  ###### Why Use `xs:ID`?

  1. **Uniqueness**: The `xs:ID` type guarantees that every `id` value is unique within the document. This is useful for identifying elements uniquely, which can help in linking, referencing, or for ensuring data consistency.

  2. **Reference Mechanism**: In XML, IDs can be used in combination with another type called **`xs:IDREF`**. The `xs:IDREF` type allows you to reference an element by its `xs:ID`. This forms a relationship similar to foreign keys in databases, allowing you to link different parts of the XML document.

     ###### Example of `xs:ID` and `xs:IDREF`

​	Consider the use of `xs:ID` along with `xs:IDREF` to establish relationships between elements:

```
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           targetNamespace="http://company.com/department"
           xmlns="http://company.com/department"
           elementFormDefault="qualified">

<xs:element name="department">
    <xs:complexType>
        <xs:sequence>
            <xs:element name="employeeRef" type="xs:IDREF"/>
        </xs:sequence>
        <xs:attribute name="deptId" type="xs:ID" use="required"/>
    </xs:complexType>
</xs:element>

</xs:schema>
```

- Here, `deptId` is an `xs:ID` and must be unique.
- `employeeRef` is an `xs:IDREF` and must refer to an existing `id` of an `employee`.

This mechanism allows you to define **relationships** between different elements in the XML, similar to referencing in a relational database.

the `type="xs:ID"` in an XML Schema (XSD) **cannot** be a number only. In fact, the value of an attribute of type `xs:ID` must follow the rules for **XML names**, which means:

1. **Starts with a Letter or Underscore**: The value must start with a letter (either uppercase or lowercase) or an underscore (`_`). It **cannot start with a digit**.
2. **Contains Letters, Digits, Hyphens, Periods, or Underscores**: After the first character, the value can contain letters, digits, hyphens (`-`), periods (`.`), or underscores (`_`).
3. **No Spaces**: The value cannot contain spaces.

Here are some examples of valid and invalid values for an attribute of type `xs:ID`:

###### Examples of Valid Values for `xs:ID`:

- `"E101"` (Starts with a letter and contains digits)
- `"emp_123"` (Starts with a letter and contains an underscore and digits)
- `"_myId"` (Starts with an underscore and contains letters)
- `"id-001"` (Starts with a letter and contains a hyphen and digits)

###### Examples of Invalid Values for `xs:ID`:

- `"1234"` (**Invalid**: Starts with a digit)
- `"my id"` (**Invalid**: Contains a space)
- `"-emp01"` (**Invalid**: Starts with a hyphen)

###### Summary:

- **`xs:ID`** cannot be a **number only** or **start with a digit**.
- **`xs:ID`** is a data type that represents a **unique identifier
- It must follow the rules of XML naming conventions, which means it should start with a **letter or underscore**, and can include **letters, digits, hyphens, periods, or underscores**.

- It ensures the **uniqueness** of an attribute value across the entire XML document.
- It’s typically used for uniquely identifying elements, enabling linking and referencing, much like a primary key.

This XML:

- References the `employee.xsd` schema using `xsi:noNamespaceSchemaLocation`.

------

###### 3. **Java Code to Validate XML Against XSD**:



```java
import java.io.File;
import javax.xml.XMLConstants;
import javax.xml.validation.Schema;
import javax.xml.validation.SchemaFactory;
import javax.xml.validation.Validator;
import org.xml.sax.SAXException;

public class XMLValidatorWithXSD {
    public static void main(String[] args) {
        try {
            File projectHome = new File(System.getProperty("user.dir"));

            // 1. Load the XML Schema (employee.xsd)
            File schemaFile = new File(projectHome.getAbsolutePath()+"/src/main/resources/employee.xsd");
            SchemaFactory schemaFactory = SchemaFactory.newInstance(XMLConstants.W3C_XML_SCHEMA_NS_URI);
            Schema schema = schemaFactory.newSchema(schemaFile);

            // 2. Create a Validator
            Validator validator = schema.newValidator();

            // 3. Validate the XML file (employee.xml)
            File xmlFile = new File(projectHome.getAbsolutePath()+"/src/main/resources/employee-using-xsd.xml");
            validator.validate(new javax.xml.transform.stream.StreamSource(xmlFile));

            // If no exception, XML is valid
            System.out.println("The XML file is valid.");

        } catch (SAXException e) {
            // Validation failed
            System.out.println("Validation failed: " + e.getMessage());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```



###### **How It Works**:

1. **Load Schema**:
   - Use `SchemaFactory` to create a `Schema` object from the `employee.xsd` file.
   - `XMLConstants.W3C_XML_SCHEMA_NS_URI` specifies that the schema is XSD-based.
2. **Create Validator**:
   - A `Validator` object is created from the `Schema`.
3. **Validate XML**:
   - The `validator.validate()` method checks the `employee.xml` file against the `employee.xsd` schema.
4. **Error Handling**:
   - If validation fails, a `SAXException` is thrown with details of the error.

------

###### 5. **Example Output**:

###### Valid XML:

If `employee.xml` conforms to `employee.xsd`, the output is:

```
The XML file is valid.
```

###### Invalid XML:

If the XML is invalid (e.g., missing the `id` attribute), the output might be:

```
Validation failed: cvc-complex-type.4: Attribute 'id' must appear on element 'employee'.
```

------

## **XML Parsing**

XML parsing refers to the process of reading and extracting data from an XML document. This can be done using a variety of methods and tools depending on the programming language.

#### **Types of XML Parsers:**

1. **DOM (Document Object Model) Parser**:
   - Loads the entire XML document into memory as a tree structure.
   - Provides flexibility to navigate and modify the XML.
   - Suitable for small to medium-sized XML files.
2. **SAX (Simple API for XML) Parser**:
   - Parses XML sequentially, one element at a time.
   - Does not load the entire document into memory.
   - Suitable for large XML files but does not allow backward navigation.
3. **StAX (Streaming API for XML)**:
   - Combines features of DOM and SAX.
   - Allows both reading and writing of XML sequentially.
   - Efficient for large XML documents.
4. **JAXB (Java Architecture for XML Binding)**:
   - Binds XML to Java objects and vice versa (object serialization).
   - Simplifies XML processing by using annotations to map Java classes to XML schema.
   - Efficient for large XML documents.

------

##### **1. DOM (Document Object Model) Parser**

###### **Explanation**

- **How it works**: Loads the entire XML document into memory and creates a tree-like structure.
- **Use case**: Suitable for **small to medium XML files** where you need **random access** to the document.
- **Pros**: Easy to traverse and modify the document.
- **Cons**: Not memory-efficient for large files.

###### **Sample XML (books.xml)**

```xml
<books>
    <book id="1">
        <title>Clean Code</title>
        <author>Robert C. Martin</author>
        <price>29.99</price>
    </book>
    <book id="2">
        <title>Effective Java</title>
        <author>Joshua Bloch</author>
        <price>39.99</price>
    </book>
</books>
```

###### **Java Code Using DOM**

```java

import org.w3c.dom.Document;
import org.w3c.dom.Element;
import org.w3c.dom.Node;
import org.w3c.dom.NodeList;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import java.io.File;

public class DOMParserExample {
    public static void main(String[] args) {
        try {
            File projectHome = new File(System.getProperty("user.dir"));

            // 1. Load the XML Schema (employee.xsd)
            // Load the XML file
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
            DocumentBuilder builder = factory.newDocumentBuilder();
            Document document = builder.parse(projectHome.getAbsolutePath()+"/src/main/resources/books.xml");

            // Normalize the document (optional but recommended)
            document.getDocumentElement().normalize();

            // Get the root element
            Element root = document.getDocumentElement();
            System.out.println("Root Element: " + root.getNodeName());

            // Get all <book> elements
            NodeList bookList = document.getElementsByTagName("book");

            for (int i = 0; i < bookList.getLength(); i++) {
                Node bookNode = bookList.item(i);

                if (bookNode.getNodeType() == Node.ELEMENT_NODE) {
                    Element bookElement = (Element) bookNode;

                    // Access attributes and child elements
                    String id = bookElement.getAttribute("id");
                    String title = bookElement.getElementsByTagName("title").item(0).getTextContent();
                    String author = bookElement.getElementsByTagName("author").item(0).getTextContent();
                    String price = bookElement.getElementsByTagName("price").item(0).getTextContent();

                    System.out.println("Book ID: " + id);
                    System.out.println("Title: " + title);
                    System.out.println("Author: " + author);
                    System.out.println("Price: $" + price);
                    System.out.println("---------------");
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

###### **Output**

```
Root Element: books
Book ID: 1
Title: Clean Code
Author: Robert C. Martin
Price: $29.99
---------------
Book ID: 2
Title: Effective Java
Author: Joshua Bloch
Price: $39.99
---------------
```

------

##### **2. SAX (Simple API for XML) Parser**

###### **Explanation**

- **How it works**: Reads the XML document **sequentially** and triggers events (e.g., start of an element, end of an element).
- **Use case**: Suitable for **large XML files** when memory usage is a concern.
- **Pros**: Memory-efficient as it doesn’t load the entire document.
- **Cons**: No random access to elements, and you must handle events manually.

###### **Java Code Using SAX**

```java
import org.xml.sax.*;
import org.xml.sax.helpers.*;
import javax.xml.parsers.SAXParser;
import javax.xml.parsers.SAXParserFactory;
import java.io.File;

public class SAXParserExample extends DefaultHandler {

    public static void main(String[] args) {
        try {
            // Create a SAX parser
            SAXParserFactory factory = SAXParserFactory.newInstance();
            SAXParser saxParser = factory.newSAXParser();
            File projectHome = new File(System.getProperty("user.dir"));

            // Parse the XML file
            saxParser.parse(projectHome.getAbsolutePath()+"/src/main/resources/books.xml", new SAXParserExample());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // Triggered at the start of an element
    public void startElement(String uri, String localName, String qName, Attributes attributes) {
        if (qName.equals("book")) {
            String id = attributes.getValue("id");
            System.out.println("Book ID: " + id);
        } else if (qName.equals("title") || qName.equals("author") || qName.equals("price")) {
            System.out.print(qName + ": ");
        }
    }

    // Triggered when character data is encountered
    public void characters(char[] ch, int start, int length) {
        System.out.println(new String(ch, start, length));
    }

    // Triggered at the end of an element
    public void endElement(String uri, String localName, String qName) {
        if (qName.equals("book")) {
            System.out.println("---------------");
        }
    }
}



```

###### **Output**

```
Book ID: 1
title: Clean Code
author: Robert C. Martin
price: 29.99
---------------
Book ID: 2
title: Effective Java
author: Joshua Bloch
price: 39.99
---------------
```

------



##### **3. StAX (Streaming API for XML) Parser**

###### **Explanation**

- **How it works**: Reads XML data sequentially using a **cursor-like approach**.
- **Use case**: Suitable for **streaming large XML files** with more control than SAX.
- **Pros**: Combines the benefits of DOM (easy to use) and SAX (memory-efficient).
- **Cons**: Less intuitive than DOM for small XML documents.

###### **Java Code Using StAX**

```java
import javax.xml.stream.*;
import java.io.File;
import java.io.FileReader;

public class StAXParserExample {
    public static void main(String[] args) {
        try {
            File projectHome = new File(System.getProperty("user.dir"));

            // Create a StAX parser
            XMLInputFactory factory = XMLInputFactory.newInstance();

            XMLStreamReader reader = factory.createXMLStreamReader(new FileReader(projectHome.getAbsolutePath()+"/src/main/resources/books.xml"));

            while (reader.hasNext()) {
                int event = reader.next();

                if (event == XMLStreamReader.START_ELEMENT) {
                    String elementName = reader.getLocalName();

                    if (elementName.equals("book")) {
                        String id = reader.getAttributeValue(null, "id");
                        System.out.println("Book ID: " + id);
                    } else if (elementName.equals("title") || elementName.equals("author") || elementName.equals("price")) {
                        System.out.print(elementName + ": ");
                    }
                } else if (event == XMLStreamReader.CHARACTERS) {
                    if (!reader.isWhiteSpace()) {
                        System.out.println(reader.getText());
                    }
                } else if (event == XMLStreamReader.END_ELEMENT) {
                    if (reader.getLocalName().equals("book")) {
                        System.out.println("---------------");
                    }
                }
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

###### **Output**

```
Book ID: 1
title: Clean Code
author: Robert C. Martin
price: 29.99
---------------
Book ID: 2
title: Effective Java
author: Joshua Bloch
price: 39.99
---------------
```

##### **4. JAXB (Java Architecture for XML Binding)**

###### **Explanation**

- **How it works**: JAXB maps Java objects to XML (marshalling) and XML to Java objects (unmarshalling) using annotations or XML schemas.

- **Use case**: Ideal for scenarios requiring **data binding** between Java objects and XML, such as web services and configuration files.

- Pros

  :

  - Simplifies XML parsing by removing the need to handle XML structure directly.
  - Supports automatic generation of Java classes from XML schemas and vice versa.
  - Easily integrates with frameworks like JAX-WS for web services.

- Cons

  :

  - Less flexible for manipulating XML documents without a predefined schema.
  - Requires extra memory when marshalling/unmarshalling large XML files.

------

##### **Key Features**

1. ###### **Annotations**:

   - Use `@XmlRootElement`, `@XmlElement`, and others to define how Java objects map to XML elements.

   - Example:

     ```java
     import javax.xml.bind.annotation.XmlElement;
     import javax.xml.bind.annotation.XmlRootElement;
     import java.util.List;
     
     @XmlRootElement
     public class Bookstore {
         @XmlElement
         private String name;
     
         @XmlElement
         private List<Book> books;
     
         // Getters and Setters
     }
     
     class Book {
         @XmlElement
         private String title;
     
         @XmlElement
         private String author;
     
         @XmlElement
         private double price;
     
         // Getters and Setters
     }
     ```

2. ###### **Marshalling** (Java object to XML):

   ```java
   import javax.xml.bind.JAXBContext;
   import javax.xml.bind.Marshaller;
   import java.util.Arrays;
   
   public class MarshallingExample {
       public static void main(String[] args) throws Exception {
           Bookstore bookstore = new Bookstore();
           bookstore.setName("The Book Haven");
   
           Book book1 = new Book();
           book1.setTitle("Java Programming");
           book1.setAuthor("John Doe");
           book1.setPrice(45.99);
   
           Book book2 = new Book();
           book2.setTitle("XML Made Simple");
           book2.setAuthor("Jane Smith");
           book2.setPrice(30.50);
   
           bookstore.setBooks(Arrays.asList(book1, book2));
   
           JAXBContext context = JAXBContext.newInstance(Bookstore.class);
           Marshaller marshaller = context.createMarshaller();
           marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
           marshaller.marshal(bookstore, System.out); // Output to console
       }
   }
   ```

   **Sample XML Output**:

   ```
   <bookstore>
       <name>The Book Haven</name>
       <books>
           <book>
               <title>Java Programming</title>
               <author>John Doe</author>
               <price>45.99</price>
           </book>
           <book>
               <title>XML Made Simple</title>
               <author>Jane Smith</author>
               <price>30.5</price>
           </book>
       </books>
   </bookstore>
   ```

3. ###### **Unmarshalling** (XML to Java object):

   ```java
   import javax.xml.bind.JAXBContext;
   import javax.xml.bind.Unmarshaller;
   import java.io.File;
   
   public class UnmarshallingExample {
       public static void main(String[] args) throws Exception {
           JAXBContext context = JAXBContext.newInstance(Bookstore.class);
           Unmarshaller unmarshaller = context.createUnmarshaller();
   
           Bookstore bookstore = (Bookstore) unmarshaller.unmarshal(new File("bookstore.xml"));
           System.out.println("Bookstore: " + bookstore.getName());
           bookstore.getBooks().forEach(book -> {
               System.out.println("Title: " + book.getTitle());
               System.out.println("Author: " + book.getAuthor());
               System.out.println("Price: $" + book.getPrice());
           });
       }
   }
   ```

   **Sample XML File (`bookstore.xml`)**:

   ```
   <bookstore>
       <name>The Book Haven</name>
       <books>
           <book>
               <title>Java Programming</title>
               <author>John Doe</author>
               <price>45.99</price>
           </book>
           <book>
               <title>XML Made Simple</title>
               <author>Jane Smith</author>
               <price>30.5</price>
           </book>
       </books>
   </bookstore>
   ```

4. ###### **Schema Validation**: Supports validation against XML schemas during unmarshalling.

------

###### **When to Use JAXB**

- Best for

  :

  - Applications where XML serves as a data exchange format.
  - Scenarios needing automatic Java class generation from XML schema (or vice versa).
  - Web services (JAX-WS uses JAXB for XML processing).

- Avoid if

  :

  - You need high-performance parsing for very large XML files (use SAX or StAX instead).
  - Complex XML structures need heavy manipulation without predefined schema.

------

###### **Comparison with Other Parsers**:

- **Simpler than DOM/SAX/StAX**: No need to manually traverse or parse XML elements.
- **Less flexible**: Tight coupling between XML schema and Java object structure. For highly dynamic XML, DOM or StAX may be better.

------

#### **Summary of Parsing Techniques**

| Feature           | DOM                    | SAX                       | StAX                      |
| ----------------- | ---------------------- | ------------------------- | ------------------------- |
| **Memory Usage**  | High (entire document) | Low (event-based)         | Low (cursor-based)        |
| **Random Access** | Yes                    | No                        | No                        |
| **Traversal**     | Tree-like              | Sequential (forward-only) | Sequential (forward-only) |
| **Modification**  | Possible               | Not possible              | Not possible              |
| **Use Case**      | Small/Medium files     | Large files               | Streaming large files     |





### **Other XML Related Technologies**

## **XPath**





##### Brief Tutorial on XPath

XPath (XML Path Language) is a query language used to navigate and retrieve information from an XML document. It provides a way to locate nodes in the document using expressions.

------

###### **Core Concepts of XPath**

1. **Nodes in XML**
   - XML documents consist of nodes:
     - **Element nodes**: `<tag>`
     - **Attribute nodes**: `attribute="value"`
     - **Text nodes**: Content within elements
     - **Root node**: The top-most node in an XML document
2. **XPath Syntax** XPath expressions define paths to navigate through the nodes.

------

###### **Basic Syntax and Examples**

1. **Absolute Path**

   - Specifies the path from the root node:

     ```xml
     /root/child/grandchild
     ```

     Example:

     ```xml
     <bookstore>
       <book>
         <title>Learn XPath</title>
       </book>
     </bookstore>
     ```

     XPath: 

     ```
     /bookstore/book/title
     ```

     Result: 

     ```
     <title>Learn XPath</title>
     ```

2. **Relative Path**

   - Starts from the current context node:

     ```xml
     book/title
     ```

3. **Selecting All Nodes (`//`)**

   - ```
     //
     ```

      selects nodes anywhere in the document:

     ```xml
     //title
     ```

     Matches all 

     ```
     <title>
     ```

      elements regardless of location.

4. **Attributes (`@`)**

   - Access attributes with 

     ```
     @
     ```

     :

     ```xml
     /bookstore/book/@category
     ```

5. **Wildcards**

   - `*`: Matches any element node.

   - ```
     @*
     ```

     : Matches any attribute node.

     ```xml
     /bookstore/book/*  → All child elements of <book>
     ```

------

###### **Operators**

1. **Predicate (`[]`)**

   - Filters nodes based on conditions:

     ```xml
     /bookstore/book[1] → First <book> element
     /bookstore/book[@category='fiction'] → Books with a category attribute 'fiction'
     ```

2. **Functions**

   - XPath includes built-in functions for advanced queries:

     - `text()` → Retrieves text content.
     - `contains()` → Checks for substring matches.
     - `last()` → Selects the last node. Example:

     ```xml
     /bookstore/book[last()] → Last <book> element
     ```

------

###### **Example XML**

```xml
<bookstore>
    <book category="fiction">
        <title lang="en">Harry Potter</title>
        <author>J.K. Rowling</author>
        <year>1997</year>
        <price>29.99</price>
    </book>
    <book category="programming">
        <title lang="en">Learn XPath</title>
        <author>Jane Doe</author>
        <year>2024</year>
        <price>39.99</price>
    </book>
    <book category="fiction">
        <title lang="en">Fantastic Beasts</title>
        <author>J.K. Rowling</author>
        <year>2016</year>
        <price>19.99</price>
    </book>
    <book category="science">
        <title lang="fr">Introduction to Physics</title>
        <author>Albert Einstein</author>
        <year>1950</year>
        <price>49.99</price>
    </book>
</bookstore>
```

 **Download the Bookstore File** [Download the XML File](./assets/bookstore_shortlisted_books.xml)

###### **Practical XPath Queries**

1. ##### **Basic Queries**

   1. **Get all book titles**:

      ```
      //title
      ```

   2. **Get the language of the title in the first book**:

      ```
      /bookstore/book[1]/title/@lang
      ```

   3. **Find books priced above $30**:

      ```
      /bookstore/book[price > 30]
      ```

   4. **Find the author of the book with the title "Harry Potter"**:

      ```
      //book[title='Harry Potter']/author
      ```

   5. **Select all attributes of `<title>` elements**:

      ```
      //title/@*
      ```

   ------

   ##### **Intermediate Queries**

   1. **Select Books Published After a Certain Year**:

      ```
      
      //book[year > 2000]/title
      ```

   2. **Select Books Where Price is Less Than or Equal to $30**:

      ```
      //book[price <= 30]/title
      ```

   3. **Select Books with Specific Authors and Titles**:

      ```
      //book[author='J.K. Rowling' and title='Harry Potter']
      ```

   4. **Select All Authors of Fiction Books**:

      ```
      //book[@category='fiction']/author
      ```

   5. **Find Books with Specific Language Attribute**:

      ```
      //book/title[@lang='en']
      ```

   ------

   ##### **Advanced Queries**

   1. ###### **Count the Number of Books**:

      ```
      count(//book)
      ```

   2. ###### **Select the First Book in the XML**:

      ```
      //book[1]
      ```

   3. **Select the Last Book in the XML**:

      ```
      //book[last()]
      ```

   4. **Find Titles Containing a Specific Word**:

      ```
      //title[contains(., 'Learn')]
      ```

   5. **Select Books with Prices in a Specific Range**:

      ```
      //book[price > 20 and price < 40]/title
      ```

   6. **Retrieve Attribute Values**:

      ```
      //@lang
      ```

   7. **Select Books with Missing Price or Year**:

      ```
      //book[not(price) or not(year)]
      ```

   8. **Select Sibling Nodes**:

      ```
      //book[title='Harry Potter']/following-sibling::book
      ```

   9. **Group by Parent and Count Children**:

      ```
      count(/bookstore/book)
      ```

   10. **Use Wildcards for Flexible Queries**:

       ```
       /bookstore/book/*[contains(local-name(), 'author')]
       ```

   11. **Combine Multiple Conditions**:

       ```
       //book[author='J.K. Rowling' and year < 2010 and price > 20]
       ```

   12. **Select Text Only (Ignore Tags)**:

       ```
       //book/title/text()
       ```

   ------

   ##### **Complex Queries**

   1. **Find All Titles of Books by "J.K. Rowling"**:

      ```
      //book[author='J.K. Rowling']/title
      ```

   2. **Find All Titles of Programming Books**:

      ```
      //book[@category='programming']/title
      ```

   3. **Find Books That Are Not Fiction**:

      ```
      //book[not(@category='fiction')]
      ```

   4. **Select Titles and Prices of Books Priced Over $30**:

      ```
      //book[price > 30]/(title | price)
      ```

   5. **Find the Second Book by an Author**:

      ```
      //book[author='J.K. Rowling'][2]
      ```

   6. **Retrieve All Text Nodes Under the Root Node**:

      ```
      //bookstore//text()
      ```

   7. **Find All Books with an Attribute**:

      ```
      //book[@*]
      ```

   8. **Select Titles of Books Published in English or French**:

      ```
      //title[@lang='en' or @lang='fr']
      ```

   ------

   ###### **Utility and Aggregation**

   1. **Count the Number of Fiction Books**:

      ```
      count(//book[@category='fiction'])
      ```

   2. **Find All Books Without a Category Attribute**:

      ```
      //book[not(@category)]
      ```

   3. **Retrieve All Unique Authors**:

      ```
      distinct-values(//author)
      ```

------

###### **Use Cases of XPath**

- **Parsing XML in Applications**: Extracting specific data for processing.
- **Web Scraping**: Navigating XML or XHTML content in web pages.
- **XSLT**: XPath is integral to XSLT for transforming XML documents.

**Java Code** 

```

import org.w3c.dom.Document;
import org.w3c.dom.NodeList;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.xpath.XPath;
import javax.xml.xpath.XPathConstants;
import javax.xml.xpath.XPathFactory;
import java.io.File;

public class XPathBookSelector {

    public static void main(String[] args) {
        try {

            File projectHome = new File(System.getProperty("user.dir"));

            // Load the XML file
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
            DocumentBuilder builder = factory.newDocumentBuilder();
            Document document = builder.parse(projectHome m ZgetAbsolutePath()+"/src/main/resources/books.xml"); // Ensure the XML file is in the same directory

            // Create XPath object
            XPathFactory xPathFactory = XPathFactory.newInstance();
            XPath xPath = xPathFactory.newXPath();

            // XPath expression to find books by the author "J.K. Rowling"
            String author = "J.K. Rowling"; // You can change this to any author
            String expression = String.format("//book[author='%s']/title", author);

            // Evaluate the XPath expression
            NodeList nodeList = (NodeList) xPath.evaluate(expression, document, XPathConstants.NODESET);

            // Print the results
            System.out.println("Books by " + author + ", Count "+nodeList.getLength() );
            for (int i = 0; i < nodeList.getLength(); i++) {
                System.out.println(nodeList.item(i).getTextContent());
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}.   asas

```

## **XSLT**

**XSLT** (eXtensible Stylesheet Language Transformations) is a language designed for transforming XML documents into other formats such as HTML, plain text, or other XML structures. It allows you to define rules and templates to manipulate and present XML data in various ways.

------

##### **Core Concepts**

1. **Transformation Process**
   - XSLT transforms an input XML document into an output document using a set of templates defined in an XSLT stylesheet.
2. **XSLT Stylesheet**
   - An XML document that defines how to transform the input XML. It uses XSLT elements and XPath expressions to match and manipulate nodes.
3. **Templates**
   - `<xsl:template>` elements define rules for matching nodes in the input XML and specify how they should be processed.

------

##### **Basic Structure of an XSLT Stylesheet**

An XSLT stylesheet typically includes:

- **Root Element**: `<xsl:stylesheet>` or `<xsl:transform>`
- **Namespace Declaration**: `xmlns:xsl="http://www.w3.org/1999/XSL/Transform"`
- **Version Attribute**: Specifies the XSLT version (e.g., `version="1.0"`)

###### **Example:**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <!-- Template definitions go here -->
</xsl:stylesheet>
```

------

###### **Common XSLT Elements**

1. **`<xsl:template>`**
   - Defines a template that matches specific nodes.
2. **`<xsl:value-of>`**
   - Extracts and outputs the value of a node.
3. **`<xsl:apply-templates>`**
   - Applies templates to selected nodes.
4. **`<xsl:for-each>`**
   - Iterates over a set of nodes.
5. **`<xsl:if>` and `<xsl:choose>`**
   - Provides conditional processing capabilities.
6. **`<xsl:variable>`**
   - Declares a variable.
7. **`<xsl:output>`**
   - Specifies the output format (e.g., HTML, XML, text).

------

##### **Example: Transforming XML to HTML**

###### **Input XML (`books.xml`):**

```xml
<bookstore>
  <book category="fiction">
    <title lang="en">Harry Potter and the Sorcerer's Stone</title>
    <author>J.K. Rowling</author>
    <year>1997</year>
    <price>29.99</price>
  </book>
  <!-- More book elements, use the sample books xml file attached -->
</bookstore>
```

###### **Default XSLT Stylesheet (`books.xsl`):**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">

  <!-- Output Method -->
  <xsl:output method="html" encoding="UTF-8"/>

  <!-- Root Template -->
  <xsl:template match="/bookstore">
    <html>
      <head>
        <title>Bookstore</title>
      </head>
      <body>
        <h1>Available Books</h1>
        <table border="1">
          <tr bgcolor="#9acd32">
            <th>Title</th>
            <th>Author</th>
            <th>Year</th>
            <th>Price</th>
          </tr>
          <xsl:apply-templates select="book"/>
        </table>
      </body>
    </html>
  </xsl:template>

  <!-- Template for Book Elements -->
  <xsl:template match="book">
    <tr>
      <td><xsl:value-of select="title"/></td>
      <td><xsl:value-of select="author"/></td>
      <td><xsl:value-of select="year"/></td>
      <td><xsl:value-of select="price"/></td>
    </tr>
  </xsl:template>

</xsl:stylesheet>
```

###### **XSLT Stylesheet using for each loop (`books-for-each.xsl`):**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:output method="html" encoding="UTF-8" indent="yes"/>

  <!-- Root Template -->
  <xsl:template match="/">
    <html>
      <head>
        <title>Bookstore</title>
      </head>
      <body>
        <h1>Available Books</h1>
        <table border="1">
          <tr>
            <th>Title</th>
            <th>Author</th>
            <th>Year</th>
            <th>Price</th>
          </tr>
          <!-- Iterate through all <book> elements -->
          <xsl:for-each select="bookstore/book">
            <tr>
              <!-- Extract data for each column -->
              <td><xsl:value-of select="title"/></td>
              <td><xsl:value-of select="author"/></td>
              <td><xsl:value-of select="year"/></td>
              <td><xsl:value-of select="price"/></td>
            </tr>
          </xsl:for-each>
        </table>
      </body>
    </html>
  </xsl:template>
</xsl:stylesheet>>
```



###### **XSLT Stylesheet (`books-sort-by-author.xsl`):**

```
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:output method="html" encoding="UTF-8" indent="yes"/>

  <!-- Root Template -->
  <xsl:template match="/">
    <html>
      <head>
        <title>Bookstore</title>
      </head>
      <body>
        <h1>Available Books (Sorted by Author)</h1>
        <table border="1">
          <tr>
            <th>Author</th>
            <th>Title</th>
            <th>Year</th>
            <th>Price</th>
          </tr>
          <!-- Iterate through all <book> elements and sort by author -->
          <xsl:for-each select="bookstore/book">
            <!-- Sort by the <author> child element -->
            <xsl:sort select="author" order="ascending"/>
            <tr>
              <td><xsl:value-of select="author"/></td>
              <td><xsl:value-of select="title"/></td>
              <td><xsl:value-of select="year"/></td>
              <td><xsl:value-of select="price"/></td>
            </tr>
          </xsl:for-each>
        </table>
      </body>
    </html>
  </xsl:template>
</xsl:stylesheet>
```



###### **Explanation:**

- **`<xsl:template match="/bookstore">`**

  - Matches the root `<bookstore>` element and defines the structure of the output HTML.

- **`<xsl:apply-templates select="book"/>`**

  - Applies templates to each `<book>` element under `<bookstore>`.

- **`<xsl:template match="book">`**

  - Defines how each `<book>` element is transformed into an HTML table row.

- **`<xsl:value-of select="element-name"/>`**

  - Extracts the text content of the specified child element.

- **`<xsl:sort select="bookstore/book"/>`**

  - Sorting the book name

- **`<xsl:sort select="price" data-type="number" order="descending"/>`**

  - Sorting the book price and we are specify the data type so it's sorting based on the number value

- **`<xsl:sort select="year" order="ascending"/>`**

  - Sorting the book year

- Now using multiple sorting criteria (please add the two lines to full xsl)

  ```
  <xsl:sort select="author" order="ascending"/>
  <xsl:sort select="title" order="ascending"/>
  ```

------

###### **Processing the Transformation**

To apply the XSLT stylesheet to the XML document, we can use various methods:

1. ###### **Using a Web Browser**

   - Modern browsers can apply XSLT stylesheets to XML files directly if you add a processing instruction at the top of the XML file.

     ```xml
     <?xml-stylesheet type="text/xsl" href="books.xsl"?>
     ```

2. ###### **Using Command-Line Tools**

   - Tools like `xsltproc` can be used to process the transformation (install using homebrew **brew install libxslt**, make sure you add the path to your zsh configuration file (see the output of brew comman)

     ```bash
     xsltproc books.xsl books.xml -o output.html
     ```

3. ###### **XSLT Processing in Java**

   ```python
   import javax.xml.transform.*;
   import javax.xml.transform.stream.StreamResult;
   import javax.xml.transform.stream.StreamSource;
   import java.io.File;
   
   public class XSLTProcessor {
       public static void main(String[] args) {
           try {
   
               File projectHome = new File(System.getProperty("user.dir"));
               File tempDir = new File(System.getProperty("java.io.tmpdir"));
               // Paths to the XML and XSLT files
               File xmlFile = new File(projectHome+"/src/main/resources/books.xml"); // Input XML file
               File xsltFile = new File(projectHome+"/src/main/resources/books.xsl"); // XSLT stylesheet
               File outputFile = new File(tempDir+"/output.html"); // Output HTML file
   
               // Create a TransformerFactory
               TransformerFactory factory = TransformerFactory.newInstance();
   
               // Load the XSLT stylesheet
               Source xslt = new StreamSource(xsltFile);
   
               // Create a Transformer object
               Transformer transformer = factory.newTransformer(xslt);
   
               // Set optional output properties (like encoding and indentation)
               transformer.setOutputProperty(OutputKeys.INDENT, "yes");
               transformer.setOutputProperty(OutputKeys.METHOD, "html");
               transformer.setOutputProperty(OutputKeys.ENCODING, "UTF-8");
   
               // Load the input XML
               Source xml = new StreamSource(xmlFile);
   
               // Define the output file
               Result output = new StreamResult(outputFile);
   
               // Perform the transformation
               transformer.transform(xml, output);
   
               System.out.println("Transformation complete. Output written to: " + outputFile.getAbsolutePath());
           } catch (Exception e) {
               e.printStackTrace();
           }
       }
   }
   ```

------

### **XQuery** 

- XQuery is a functional query language which is built on XPath expressions.
- We will not discussing or covering XQuery here



 
