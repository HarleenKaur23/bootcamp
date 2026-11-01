### Java Maven Build System: Basic Tutorial

Maven is a powerful build automation tool used primarily for Java projects. It simplifies the build process, dependency management, and project configuration. Here's a step-by-step guide to understanding and using Maven for a Java project.

### 1. **Installing Maven**

Before using Maven, you need to install it on your machine.

#### Steps:
1. **Download Maven**: Go to [Maven's download page](https://maven.apache.org/download.cgi) and download the latest version.
2. **Extract Maven**: Extract the downloaded archive to a directory of your choice.
3. **Configure Environment Variables**: 
   
   - Add the `bin` folder from Maven to your system's PATH environment variable.
   - Set the `M2_HOME` environment variable to the location where Maven was extracted.
4. **Verify Installation**: Open a terminal and type:
   ```bash
   mvn -version
   (Maven version 3.5 onwards there were some important changes about pulling the dependencies from the http endpoints)
   
   Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
   Maven home: /opt/homebrew/Cellar/maven/3.9.9/libexec
   Java version: 17.0.12, vendor: Eclipse Adoptium, runtime: /Users/robinbajaj/.sdkman/candidates/java/17.0.12-tem
   Default locale: en_CA, platform encoding: UTF-8
   OS name: "mac os x", version: "15.0", arch: "aarch64", family: "mac"
   ```
   This should show the installed version of Maven.

you have to know which Java distribution your maven is working with (`/Users/<user-name>/.sdkman/candidates/java/17.0.12-tem`)

you may need to configure `$JAVA_HOME/lib/security/cacerts` for outbound maven access from your employer organization.

`brew install keystore-explorer` for opening the cacerts file (default password is `changeit`)

### 2. **Creating a Maven Project**

You can create a Maven project either manually or using Maven's built-in archetypes (templates).

#### 2.1. **Creating a Maven Project from Command Line**

Run the following command to create a simple Maven project using the **Quickstart archetype**:

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

This command does the following:
- **`groupId`**: A unique identifier for your project, typically the domain name of the organization (e.g., `com.example`).
- **`artifactId`**: The name of your project (e.g., `my-app`).
- **`archetypeArtifactId`**: The type of project template (archetype) used for creating the project (e.g., `maven-archetype-quickstart`).
- **`interactiveMode`**: Set to `false` to avoid prompts and auto-generate the project.

This command will generate a directory structure like this:

```
my-app
│
├── pom.xml
└── src
    ├── main
    │   └── java
    │       └── com
    │           └── example
    │               └── App.java
    └── test
        └── java
            └── com
                └── example
                    └── AppTest.java
```

#### 2.2. **Project Structure Explained**

- **`src/main/java`**: Contains your source code.
- **`src/main/resources`**: Contains your source code (related) resources (anything non-java like application.properties, trades.csv, etc).
- **`src/test/java`**: Contains your test code.
- **`src/test/resources`**: Contains your test code (related) resources (any sample test-trades.csv).
- **`pom.xml`**: The Project Object Model (POM) file that holds the project's configuration, dependencies, and build instructions.

### 3. **Understanding the `pom.xml` File**

The **`pom.xml`** is the core of a Maven project. It contains all the configuration details, such as dependencies, plugins, and project metadata.

Here is a basic `pom.xml`:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- JUnit dependency for testing -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```

All things proxy server, repositories related is configured in `$M2_HOME/conf/settings.xml`

### Key Sections:

1. **`groupId`**: Identifies the project's group, usually based on the reverse domain name.
2. **`artifactId`**: The name of the project or module.
3. **`version`**: Specifies the current version of the project (e.g., `1.0-SNAPSHOT`).
4. **`properties`**: Defines project-specific properties like the Java version (`1.8` in this case).
5. **`dependencies`**: Lists all the libraries required by the project. For example, the JUnit library for testing.

### 4. **Adding Dependencies**

Maven automatically manages dependencies, fetching them from a central repository.

To add a dependency, find the Maven coordinates (groupId, artifactId, version) from [Maven Central](https://search.maven.org/) or another source, and add it to your `pom.xml`.

Example of adding a `log4j` dependency:

```xml
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

### 5. **Maven Build Lifecycle**

Maven's build lifecycle consists of multiple phases. The main phases are:

1. **`validate`**: Validate the project and ensure that all required information is available.
2. **`compile`**: Compile the source code of the project.
3. **`test`**: Run the tests using a suitable testing framework (e.g., JUnit).
4. **`package`**: Package the compiled code into a distributable format (e.g., JAR, WAR).
5. **`verify`**: Run checks to verify the package is valid and meets quality criteria.
6. **`install`**: Install the package into the local Maven repository.
7. **`deploy`**: Copy the package to a remote repository for sharing with other developers.

You can invoke these phases by running:

```bash
mvn compile         # Compiles the source code
mvn test            # Runs tests
mvn package         # Packages the project (e.g., generates a JAR)
mvn install         # Installs the package in your local Maven repository
```

### 6. **Running the Project**

If you're building a simple project with a `main` method, you can use the `exec-maven-plugin` to run the application.

Add the following plugin to your `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>3.0.0</version>
            <configuration>
                <mainClass>com.example.App</mainClass> <!-- Main class to run -->
            </configuration>
        </plugin>
    </plugins>
</build>
```

Run the application with:

```bash
mvn exec:java
```

### 7. **Testing with Maven**

Maven integrates well with testing frameworks like JUnit. The example `pom.xml` already includes JUnit as a dependency.

To run tests, simply run:

```bash
mvn test
```

Maven will automatically compile and run all tests located in `src/test/java`.

### 8. **Maven Goals and Plugins**

Maven uses **plugins** to perform different tasks. Each plugin can have multiple goals. For example, the `maven-compiler-plugin` compiles Java source files, and the `maven-surefire-plugin` runs unit tests.

Example of specifying a compiler plugin:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

You can also specify plugins for code coverage (e.g., Jacoco), packaging, and deploying.

### 9. **Common Maven Commands**

Here’s a list of commonly used Maven commands:

```bash
mvn clean           # Cleans the /target directory
mvn compile         # Compiles the source code
mvn test            # Runs the test cases
mvn package         # Packages the project into a JAR/WAR
mvn install         # Installs the package into the local repository
mvn deploy          # Deploys the package to a remote repository
```

### 10. **Maven Repository Structure**

Maven downloads dependencies from a central repository and stores them locally.

- **Local Repository**: Located on your local machine (`~/.m2/repository`).
- **Central Repository**: A global repository provided by Maven (default).

You can define additional repositories in your `pom.xml`:

```xml
<repositories>
    <repository>
        <id>my-repo</id>
        <url>http://my-company-repo.com/repo</url>
    </repository>
</repositories>
```

### 11. **Maven Profiles**

Maven profiles allow you to customize build configurations for different environments (e.g., production, development).

Example of defining a profile:

```xml
<profiles>
    <profile>
        <id>dev</id>
        <properties>
           

 <env>development</env>
        </properties>
    </profile>
    
    <profile>
        <id>prod</id>
        <properties>
            <env>production</env>
        </properties>
    </profile>
</profiles>
```

Run Maven with a specific profile:

```bash
mvn package -Pprod
```

### Summary

- **Maven** simplifies Java project management by providing dependency management and build automation.
- **POM File**: The `pom.xml` defines project metadata, dependencies, and build instructions.
- **Dependencies**: Maven automatically downloads and manages external libraries.
- **Build Lifecycle**: Maven uses phases like `compile`, `test`, and `package` to automate the build process.
- **Plugins**: Use plugins to add functionality such as running tests, packaging the project, or running the app.

Maven is a powerful tool, and this basic tutorial should give you a solid foundation to start building and managing Java projects effectively.







The Maven **Shade Plugin** is used to create a **fat JAR** (also known as an uber JAR), which packages your project along with all of its dependencies into a single JAR file. This is particularly useful for running standalone Java applications where you want to bundle everything into one executable JAR.

### Steps to Use Maven Shade Plugin for Creating a Fat JAR

1. **Add the Maven Shade Plugin to your `pom.xml`**.
2. **Configure the plugin to package all dependencies**.
3. **Run the Maven `package` command** to generate the fat JAR.

### 1. **Add Maven Shade Plugin to `pom.xml`**

Here’s an example `pom.xml` configuration with the Maven Shade Plugin.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Example dependencies -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
        <!-- Add other dependencies you need -->
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.2.4</version>
                <executions>
                    <execution>
                        <phase>package</phase> <!-- Runs during the package phase -->
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <!-- You can define the main class to be included in the manifest -->
                            <transformers>
                                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <mainClass>com.example.App</mainClass>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

</project>
```

### Key Sections:
1. **`dependencies`**: Define your project’s dependencies here.
2. **`maven-shade-plugin`**: This plugin is configured to create a fat JAR.
3. **`execution`**: The `shade` goal is bound to the `package` phase, so when you run `mvn package`, the plugin will create the fat JAR.
4. **`ManifestResourceTransformer`**: Defines the `Main-Class` in the manifest, which is required to make the JAR executable.

### 2. **Configure the Main Class**

The `ManifestResourceTransformer` in the `shade` plugin specifies the main class in the manifest file of the JAR, so when you run the JAR, it knows which class contains the `main()` method. In the example, it points to `com.example.App`.

```java
package com.example;

public class App {
    public static void main(String[] args) {
        System.out.println("Hello, Maven Shade Plugin!");
    }
}
```

### 3. **Build the Project to Generate the Fat JAR**

Once you have added the configuration, you can build the project to create the fat JAR using the following command:

```bash
mvn clean package
```

This command will:
- Clean any previous builds.
- Package your project and its dependencies into a fat JAR using the Shade plugin.

### 4. **Locate the Fat JAR**

After running the `mvn package` command, you can find the generated fat JAR in the `target` directory:

```
target/my-app-1.0-SNAPSHOT-shaded.jar
```

The `shaded.jar` file contains:
- Your compiled classes.
- All dependencies required to run the application.

### 5. **Run the Fat JAR**

You can now run the fat JAR using the `java -jar` command:

```bash
java -jar target/my-app-1.0-SNAPSHOT-shaded.jar
```

If everything is set up correctly, you should see the output from the `main()` method:

```
Hello, Maven Shade Plugin!
```

### Summary of Steps:
1. **Add the `maven-shade-plugin` to your `pom.xml`**.
2. **Specify the main class in the manifest** using the `ManifestResourceTransformer`.
3. **Run `mvn clean package`** to generate the fat JAR.
4. **Run the fat JAR** with `java -jar <your-fat-jar>.jar`.

This method creates a self-contained executable JAR, bundling all the dependencies and making it easy to distribute and run your application.

---

To set up a multi-module Maven project with a parent module `trade-processor` and two sub-modules, `trade-reader-processor-app` and `trade-analytics-app`, follow these steps:

### 1. Create the Parent Module: `trade-processor`

This is the top-level module that will manage the two sub-modules. The `pom.xml` file in the root project (`trade-processor`) will act as the parent for both sub-modules.

#### Directory Structure:
```
trade-processor
|-- pom.xml
|-- trade-reader-processor-app
|   |-- pom.xml
|-- trade-analytics-app
    |-- pom.xml
```

#### Parent `pom.xml` (for `trade-processor`):
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    
    <groupId>com.example</groupId>
    <artifactId>trade-processor</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>pom</packaging> <!-- Parent packaging should be POM -->

    <modules>
        <module>trade-reader-processor-app</module>
        <module>trade-analytics-app</module>
    </modules>

    <!-- Add any shared dependencies here -->
    <dependencyManagement>
        <dependencies>
            <!-- Common dependencies like logging, Spring, etc. -->
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <!-- Plugin management (e.g., for compilation, testing) -->
        </plugins>
    </build>
</project>
```

### 2. Sub-Module: `trade-reader-processor-app`

#### `pom.xml` (for `trade-reader-processor-app`):
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    
    <parent>
        <groupId>com.example</groupId>
        <artifactId>trade-processor</artifactId>
        <version>1.0-SNAPSHOT</version>
        <relativePath>../pom.xml</relativePath> <!-- Path to parent pom -->
    </parent>
    
    <groupId>com.example</groupId>
    <artifactId>trade-reader-processor-app</artifactId>
    <version>1.0-SNAPSHOT</version>
    
    <dependencies>
        <!-- Add module-specific dependencies here -->
    </dependencies>
    
    <build>
        <plugins>
            <!-- Any module-specific build configurations -->
        </plugins>
    </build>
</project>
```

### 3. Sub-Module: `trade-analytics-app`

#### `pom.xml` (for `trade-analytics-app`):
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    
    <parent>
        <groupId>com.example</groupId>
        <artifactId>trade-processor</artifactId>
        <version>1.0-SNAPSHOT</version>
        <relativePath>../pom.xml</relativePath> <!-- Path to parent pom -->
    </parent>
    
    <groupId>com.example</groupId>
    <artifactId>trade-analytics-app</artifactId>
    <version>1.0-SNAPSHOT</version>
    
    <dependencies>
        <!-- Add module-specific dependencies here -->
    </dependencies>
    
    <build>
        <plugins>
            <!-- Any module-specific build configurations -->
        </plugins>
    </build>
</project>
```

### 4. Building the Multi-Module Project

To build the entire multi-module project, run the following command from the `trade-processor` directory:

```bash
mvn clean install
```

This will build both sub-modules (`trade-reader-processor-app` and `trade-analytics-app`), ensuring that any shared dependencies are managed by the parent `pom.xml`.

With this setup, you can manage the two sub-modules under a common parent module, and they will share any common configurations or dependencies defined in the parent module.

----

There isn't a built-in Maven archetype specifically for a multi-module setup, but you can create a multi-module Maven project using a custom archetype or by using existing Maven commands to quickly scaffold a project structure.

Here’s how you can create a multi-module setup using the standard Maven commands:

### 1. Create the Parent Module (top-level project)

You can create the parent module using the Maven archetype for a basic project (with `pom` packaging), which will serve as the aggregator for sub-modules:

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=trade-processor -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

Once created, navigate to the `trade-processor` directory:

```bash
cd trade-processor
```

Modify the `pom.xml` to act as a parent by changing the `<packaging>` to `pom`.

#### Updated `pom.xml` for Parent Module:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    
    <groupId>com.example</groupId>
    <artifactId>trade-processor</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>pom</packaging>

    <modules>
        <module>trade-reader-processor-app</module>
        <module>trade-analytics-app</module>
    </modules>

    <!-- Add any shared dependencies or build configuration here -->

</project>
```

### 2. Create Sub-Modules

Next, create the sub-modules as part of the parent project.

#### Create Sub-Module `trade-reader-processor-app`:

From within the `trade-processor` directory, run:

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=trade-reader-processor-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

This will create a `trade-reader-processor-app` sub-module directory with a basic Maven structure.

#### Create Sub-Module `trade-analytics-app`:

Similarly, create the `trade-analytics-app` sub-module by running:

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=trade-analytics-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

This will create the `trade-analytics-app` sub-module.

### 3. Add Sub-Modules to Parent `pom.xml`

Ensure that your parent `pom.xml` (in `trade-processor`) references both sub-modules in the `<modules>` section:

```xml
<modules>
    <module>trade-reader-processor-app</module>
    <module>trade-analytics-app</module>
</modules>
```

### 4. Build the Multi-Module Project

Now, from the root of the `trade-processor` project, you can build the entire multi-module project using:

```bash
mvn clean install
```
