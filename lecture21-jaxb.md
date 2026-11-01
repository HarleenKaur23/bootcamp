## **JAXB **

#### 							                                                   **(Java Architecture for XML Binding)**

- XML Parsing - An XML parser is the piece of software that reads XML files and makes the information from those files available to applications and programming languages

- Why use JAXB 

  - Defines an API for reading and writing Java objects to and from XML documents.

  - Don't need to be aware of XML parsing techniques

  - No extra dependency needed (its provided by JDK)

  - Used as a standard in many cases


![image-20241204120016631](/Users/brijeshkumar/Library/Application Support/typora-user-images/xml-jaxb-java.png)

#### **Two main JAXB components** 

- Binding Compiler - The binding compiler binds a given XML Schema to set of generated Java ckasses

- Binding Runtime Framework - Runtime framework provides unmarshalling , marshalling and validation functionalities

  

**JAXB binding compiler:**

- The JAXB binding compiler (also known as **xjc**) lets you generate Java classes from a given XML Schema.
- It transforms XML Schemas into a collection of Java classes that match the structure defined in the XML Schema.
- These classes are annotated with special JAXB annotations.
- JAXB provides the runtime framework with the mappings it needs to process corresponding XML documents.
- 

**Binding runtime framework**:

- The binding runtime framework provides an efficient and easy-to-use mechanism for unmarshalling (or reading) and marshalling (or writing) XML documents
- Transform an XML document into a hierarchy of Java objects (unmarshalling) or, inversely, transform a Java object hierarchy into XML format (marshalling)

**Basic Annotations**

- JAXB uses annotations to indicate the central elements.
  - **@XmlRootElement(namespace = "namespace")** - Define the root element for an XML tree
  - **@XmlType(propOrder = { "field2", "field1",.. })** - Allows to define the order in which the fields are written in the XML file
  - **@XmlElement** - Define the XML element which will be used.
  - **@XmlAttribute**- Define the attribute of an element

##### **JAXB - Operations**

![image-20241204144716249](/Users/brijeshkumar/Library/Application Support/typora-user-images/jaxb-marshaller-unmarshaller.png)

###### **XSD (`bookstore.xsd`)**

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified">
    <xs:element name="bookstore">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="book" maxOccurs="unbounded">
                    <xs:complexType>
                        <xs:sequence>
                            <xs:element name="title" type="xs:string" />
                            <xs:element name="author" type="xs:string" />
                            <xs:element name="price" type="xs:decimal" />
                        </xs:sequence>
                    </xs:complexType>
                </xs:element>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>

```

To generate we use the **XJC tool** (XML to Java Compiler or JAXB binding compiler) is a command-line utility provided as part of the **Java Architecture for XML Binding (JAXB)** framework. It generates Java classes from an XML Schema Definition (XSD) file. These classes can then be used for **data binding** to marshal (convert) Java objects to XML and unmarshal (convert) XML back to Java objects.

- run the following command to generate the classes

  ```bash
  xjc -d src -p com.example.bookstore bookstore.xsd
  ```

------

##### **Key Features of XJC**

1. ###### **Generates Java Classes**:

   - Automatically creates Java classes with appropriate fields, getters, setters, and annotations based on the structure defined in the XSD file.

2. ###### **Supports Customization**:

   - Allows customization of generated code using JAXB binding files (`.xjb`) to control package names, class names, and more.

3. ###### **Enforces XML Schema**:

   - Ensures that the generated classes strictly adhere to the provided XSD.

4. ###### **Output Ready for JAXB**:

   - The generated classes can be directly used for JAXB marshalling and unmarshalling.

------

##### **When to Use XJC**

- **Data Binding**: When you need to interact with XML documents using Java objects.
- **Schema Validation**: To ensure XML documents conform to a specific XSD schema.
- **Web Services**: To process XML-based messages in SOAP or RESTful web services.

###### 3. **Generated Java Classes**

- A `Bookstore` class with a list of `Book` objects.
- The `Book` class will have fields for `title`, `author`, and `price`.

------

##### **Customization with Binding Files**

You can use `.xjb` binding files to customize the generated code. For example, you might want to:

- Change a package name.
- Rename a generated class.

###### Example Binding File (`bindings.xjb`):

```xml
<jaxb:bindings xmlns:jaxb="http://java.sun.com/xml/ns/jaxb"
               xmlns:xs="http://www.w3.org/2001/XMLSchema"
               jaxb:version="2.1">
    <jaxb:bindings schemaLocation="bookstore.xsd">
        <jaxb:bindings node="//xs:element[@name='book']">
            <jaxb:class name="CustomBook" />
        </jaxb:bindings>
    </jaxb:bindings>
</jaxb:bindings>
```

###### Run XJC with Binding File:

```bash
xjc -d src -p com.example.bookstore -b bindings.xjb bookstore.xsd
```

------

###### **XJC Options**

- **`-d <directory>`**: Specify the output directory for generated files.
- **`-p <package>`**: Specify the package name for generated classes.
- **`-b <file>`**: Use a binding customization file.
- **`-npa`**: Suppress generation of `package-info.java`.
- **`-nv`**: Disable strict schema validation.

------

###### **Uses**

1. **XML Configuration**:
   - Define an XSD for application configuration and use JAXB to load it as Java objects.
2. **Web Services**:
   - SOAP-based services often require classes generated from WSDL (uses XSD internally).
3. **Data Interchange**:
   - Use XSD to define data formats exchanged between systems and generate Java classes for handling those formats.

------

##### **Notes**

- In JDK 9 and later JAXB (and XJC) is no longer bundled with the JDK. You need to use the standalone JAXB libraries.

  - We need to add the Maven Dependency in pom.xml

    ```xml
    <dependency>
        <groupId>com.sun.xml.bind</groupId>
        <artifactId>jaxb-xjc</artifactId>
        <version>2.3.2</version>
    </dependency>
    ```

- ###### In earlier versions (JDK 8 and before), XJC is available in the `bin` directory of the JDK.

JAXB (Java Architecture for XML Binding) provides several annotations to map Java objects to XML elements and vice versa. These annotations are defined in the `javax.xml.bind.annotation` package and are used to customize the XML structure generated during marshalling or the mapping behavior during unmarshalling.

Here is a comprehensive list of JAXB annotations:

------

##### **1. `@XmlRootElement`**

- **Description**: Specifies the root element of an XML document.

- **Usage**: Applied to a class.

- Attributes

  :

  - `name`: The name of the XML root element (default is the class name).
  - `namespace`: The XML namespace.

- Example

  :

  ```java
  @XmlRootElement(name = "bookstore")
  public class Bookstore {
  }
  ```

------

##### **2. `@XmlType`**

- **Description**: Defines the order of XML elements in a class.

- **Usage**: Applied to a class.

- Attributes

  :

  - `propOrder`: Specifies the order of the XML elements.
  - `name`: The name of the XML type (optional).
  - `namespace`: The namespace (optional).

- Example

  :

  ```java
  @XmlType(propOrder = { "title", "author", "price" })
  public class Book {
  }
  ```

------

##### **3. `@XmlElement`**

- **Description**: Maps a Java property to an XML element.

- **Usage**: Applied to a field, method, or parameter.

- Attributes

  :

  - `name`: Specifies the name of the XML element.
  - `nillable`: Allows `xsi:nil` representation for null values.
  - `required`: Specifies if the element is required (default is `false`).
  - `namespace`: The namespace.

- Example

  :

  ```java
  @XmlElement(name = "bookTitle", required = true)
  private String title;
  ```

------

##### **4. `@XmlAttribute`**

- **Description**: Maps a Java property to an XML attribute.

- **Usage**: Applied to a field or method.

- Attributes

  :

  - `name`: Specifies the name of the XML attribute.
  - `required`: Specifies if the attribute is required (default is `false`).
  - `namespace`: The namespace.

- Example

  :

  ```java
  @XmlAttribute(name = "id", required = true)
  private int bookId;
  ```

------

##### **5. `@XmlValue`**

- **Description**: Maps a property to the text content of an XML element.

- **Usage**: Applied to a single field or method in a class.

- Example

  :

  ```java
  public class Price {
      @XmlValue
      private double amount;
  }
  ```

------

##### **6. `@XmlElementWrapper`**

- **Description**: Wraps a collection of XML elements in an enclosing element.

- **Usage**: Applied to a field or method.

- Attributes

  :

  - `name`: Specifies the wrapper element name.
  - `namespace`: The namespace.

- Example

  :

  ```java
  @XmlElementWrapper(name = "books")
  @XmlElement(name = "book")
  private List<Book> bookList;
  ```

------

##### **7. `@XmlTransient`**

- **Description**: Prevents a field or method from being mapped to XML.

- **Usage**: Applied to a field or method.

- Example

  :

  ```java
  @XmlTransient
  private String internalCode;
  ```

------

##### **8. `@XmlAccessorType`**

- **Description**: Defines how JAXB accesses fields and properties.

- **Usage**: Applied to a class.

- Values

  :

  - `XmlAccessType.FIELD`: JAXB maps all non-static, non-transient fields.
  - `XmlAccessType.PROPERTY`: JAXB maps all public getters/setters.
  - `XmlAccessType.PUBLIC_MEMBER`: JAXB maps all public fields and properties.
  - `XmlAccessType.NONE`: JAXB maps nothing unless explicitly annotated.

- Example

  :

  ```java
  @XmlAccessorType(XmlAccessType.FIELD)
  public class Book {
  }
  ```

------

##### **9. `@XmlAccessorOrder`**

- **Description**: Controls the ordering of fields and properties.

- **Usage**: Applied to a class.

- Values

  :

  - `XmlAccessOrder.ALPHABETICAL`: Orders alphabetically.
  - `XmlAccessOrder.UNDEFINED`: No specific order.

- Example

  :

  ```java
  @XmlAccessorOrder(XmlAccessOrder.ALPHABETICAL)
  public class Book {
  }
  ```

------

##### **10. `@XmlSchema`**

- **Description**: Maps the XML namespace and schema.

- **Usage**: Applied at the package level using `package-info.java`.

- Attributes

  :

  - `namespace`: The namespace.
  - `elementFormDefault`: Specifies whether elements are qualified (`qualified`) or not (`unqualified`).

- Example

   (in 

  ```
  package-info.java
  ```

  ):

  ```java
  @XmlSchema(namespace = "http://example.com/books", elementFormDefault = XmlNsForm.QUALIFIED)
  package com.example.books;
  ```

------

##### **11. `@XmlSeeAlso`**

- **Description**: Informs JAXB of related classes for polymorphic marshalling/unmarshalling.

- **Usage**: Applied to a class.

- Example

  :

  ```java
  @XmlSeeAlso({ Ebook.class, PrintedBook.class })
  public class Book {
  }
  ```

------

##### **12. `@XmlEnum`**

- **Description**: Maps an enum type to an XML representation.

- **Usage**: Applied to an enum class.

- Example

  :

  ```java
  @XmlEnum(String.class)
  public enum Genre {
      @XmlEnumValue("Fiction") FICTION,
      @XmlEnumValue("Non-Fiction") NON_FICTION
  }
  ```

------

##### **13. `@XmlEnumValue`**

- **Description**: Specifies the XML value for an enum constant.

- **Usage**: Applied to enum constants.

- Example

  :

  ```java
  @XmlEnumValue("Fiction")
  FICTION
  ```

------

##### **14. `@XmlElements`**

- **Description**: Specifies multiple possible XML element types for a property.

- **Usage**: Applied to a field or method.

- Example

  :

  ```java
  @XmlElements({
      @XmlElement(name = "ebook", type = Ebook.class),
      @XmlElement(name = "printedBook", type = PrintedBook.class)
  })
  private Book book;
  ```

------

##### **15. `@XmlAnyElement`**

- **Description**: Captures elements not bound to a specific property.

- **Usage**: Applied to a field or method.

- Example

  :

  ```java
  @XmlAnyElement
  private List<Object> otherElements;
  ```

------

##### **16. `@XmlAnyAttribute`**

- **Description**: Captures attributes not explicitly bound to a property.

- **Usage**: Applied to a `Map<QName, String>` field or method.

- Example

  :

  ```java
  @XmlAnyAttribute
  private Map<QName, String> otherAttributes;
  ```

------

These annotations provide powerful ways to map and customize how Java classes are bound to XML structures.

## **Java Libraries and tools for XML Processing**

Java offers a variety of libraries to deal with XML, each suited for different use cases like parsing, transformation, validation, or data binding. Here’s a categorized list of key XML libraries in Java:

------

#### **1. Core JDK XML Libraries**

These libraries are bundled with the JDK and cover most common XML processing needs.

##### a. **SAX (Simple API for XML)**

- **Description**: Event-driven parser that reads XML sequentially.
- **Class**: `javax.xml.parsers.SAXParser`
- **Use Case**: Efficiently processing large XML files in a memory-friendly way.
- **JAR Requirement**: Included in the JDK.

##### b. **DOM (Document Object Model)**

- **Description**: Loads the entire XML document into memory as a tree structure.
- **Class**: `javax.xml.parsers.DocumentBuilder`
- **Use Case**: Random access to XML nodes and modification of the document.
- **JAR Requirement**: Included in the JDK.

###### c. **StAX (Streaming API for XML)**

- **Description**: A pull-based streaming API for XML parsing.
- **Classes**: `javax.xml.stream.XMLStreamReader`, `javax.xml.stream.XMLStreamWriter`
- **Use Case**: Allows developers to control the parsing process, suitable for large XML files.
- **JAR Requirement**: Included in the JDK.

##### d. **XSLT Transformation (Java API for XML Processing - JAXP)**

- **Description**: Transforms XML using XSLT stylesheets.
- **Class**: `javax.xml.transform.Transformer`
- **Use Case**: Transforming XML to different formats like HTML or other XML.
- **JAR Requirement**: Included in the JDK.

##### e. **JAXB (Java Architecture for XML Binding)**

- **Description**: Converts Java objects to XML (marshalling) and XML to Java objects (unmarshalling).
- **Classes**: `javax.xml.bind.JAXBContext`, `javax.xml.bind.Marshaller`, `javax.xml.bind.Unmarshaller`
- **Use Case**: Data binding for XML documents.
- **JAR Requirement**: Included in JDK 9 and earlier; external library for newer versions.

------

#### **2. Third-Party Libraries**

For more advanced use cases, the following third-party libraries provide additional functionality or performance improvements:

##### a. **Apache Xerces**

- **Description**: A high-performance parser that supports SAX, DOM, and JAXP.
- **Use Case**: Validation of XML documents against DTD or XML Schema.
- **JAR**: `xercesImpl.jar`

##### b. **Apache XMLBeans**

- **Description**: Provides XML binding by allowing Java objects to be used as XML elements.
- **Use Case**: Handling XML documents with dynamic schemas.
- **JAR**: `xmlbeans.jar`

##### c. **JDOM**

- **Description**: A lightweight library for XML processing.
- **Use Case**: Provides a simpler API for reading, writing, and manipulating XML than the DOM API.
- **JAR**: `jdom.jar`

##### d. **DOM4J**

- **Description**: A flexible library for XML parsing and manipulation.
- **Use Case**: Integrates easily with XPath and XSLT.
- **JAR**: `dom4j.jar`

##### e. **XOM (XML Object Model)**

- **Description**: A robust and simple library for XML processing with an emphasis on correctness.
- **Use Case**: Handling XML documents with strong guarantees on well-formedness.
- **JAR**: `xom.jar`

##### f.  **ThoughtWorks XStream**

- **Description**: A simple and flexible library for serializing Java objects to XML and deserializing XML to Java objects.

- **Use Case**: Ideal for object persistence, configuration files, and logging.

- **JAR**: `xstream.jar`

- Key Features

  :

  - Minimal setup: Automatically maps Java objects to XML.
  - Customizable: Supports annotations (`@XStreamAlias`, etc.) and custom converters.
  - JSON support: Converts between Java objects, XML, and JSON.

------

#### **3. Other Specialized Libraries**

These libraries address niche XML processing requirements.

##### a. **Woodstox**

- **Description**: A high-performance StAX-compliant XML parser.
- **Use Case**: For performance-critical streaming applications.
- **JAR**: `woodstox-core.jar`

##### b. **Saxon**

- **Description**: An XSLT and XQuery processor.
- **Use Case**: Advanced transformations and querying of XML documents.
- **JAR**: `saxon.jar`

##### c. **XMLUnit**

- **Description**: A library for comparing XML documents.
- **Use Case**: Unit testing XML output, comparing expected vs. actual XML.
- **JAR**: `xmlunit-core.jar`

------

#### **4. JSON-XML Conversion Libraries**

When XML needs to be converted to JSON or vice versa.

##### a. **Jackson XML Module**

- **Description**: Adds XML support to Jackson's JSON processing library.
- **Use Case**: Convert between XML and JSON with POJO mapping.
- **JAR**: `jackson-dataformat-xml.jar`

##### b. **org.json (XML API)**

- **Description**: Provides utilities to convert XML to JSON and vice versa.
- **Use Case**: Simplified XML-JSON transformations.
- **JAR**: `json.jar`

------

#### **Comparison Chart**

| **Library**   | **Type**              | **Use Case**                                | **Bundled with JDK?** |
| ------------- | --------------------- | ------------------------------------------- | --------------------- |
| SAX           | Event-driven Parser   | Streaming large XML files                   | Yes                   |
| DOM           | Tree-based Parser     | Random access or modification of XML        | Yes                   |
| StAX          | Pull-based Parser     | Efficient streaming with developer control  | Yes                   |
| JAXB          | Data Binding          | Converting between XML and Java objects     | JDK 9 and earlier     |
| Apache Xerces | Validation            | High-performance parsing and validation     | No                    |
| JDOM          | Simplified API        | Easy manipulation of XML                    | No                    |
| DOM4J         | Advanced Manipulation | XPath and XSLT integration                  | No                    |
| XMLBeans      | XML Binding           | Dynamic XML schema handling                 | No                    |
| XOM           | Simple API            | Guaranteed well-formed XML documents        | No                    |
| Woodstox      | High-performance StAX | Performance-critical streaming applications | No                    |
| Saxon         | XSLT/XQuery Processor | Advanced XML transformations                | No                    |
| XMLUnit       | Comparison            | Unit testing XML documents                  | No                    |

------

We need choose the library based on the **size of the XML**, **performance needs**, and **complexity of operations**!

_____________



