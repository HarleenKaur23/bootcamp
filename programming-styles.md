Sure! Let's imagine you're learning to cook, and each programming style is like a different way of learning to make your favorite meal. Here’s how they compare:

### Imperative Programming
Imagine you have a cookbook with step-by-step instructions to make spaghetti. You follow each step exactly, one after another:

1. Boil water.
2. Add pasta.
3. Cook for 10 minutes.
4. Drain water.
5. Add sauce.

In imperative programming, you tell the computer exactly what to do, step by step, just like following a recipe.

### Procedural Programming
This is like imperative programming but with a little more organization. Imagine you have multiple recipes, and each recipe is a "procedure" or a set of instructions for a specific part of the meal:

- Recipe for boiling pasta
- Recipe for making sauce

Each recipe can be used whenever you need that specific part. You can say, "Follow the recipe to boil pasta," then "Follow the recipe to make sauce," and finally combine them.

### Functional Programming
Imagine you're making a sandwich with pre-made ingredients. You have a function to get bread, a function to get peanut butter, and a function to get jelly. You don't care about the steps inside these functions, just the final result:

- `getBread()`
- `getPeanutButter()`
- `getJelly()`
- `combineIngredients(bread, peanutButter, jelly)`

In functional programming, you use functions to get the result you want, without worrying about the step-by-step process inside those functions.

### Object-Oriented Programming
This is like organizing your kitchen into sections, with each section being an object that has everything needed to make different parts of a meal. For example:

- A "PastaPot" object knows how to boil pasta.
- A "SaucePan" object knows how to make sauce.
- A "Dish" object knows how to serve the meal.

Each object has its own instructions (methods) and ingredients (data). When you want to cook, you just tell each object what to do, and they take care of their part of the meal:

- `PastaPot.boilPasta()`
- `SaucePan.makeSauce()`
- `Dish.serveMeal(pasta, sauce)`

In object-oriented programming, you create objects that know how to do things and tell them to do those things when you need them.

### Summary
- **Imperative:** Step-by-step instructions like a detailed recipe.
- **Procedural:** Organized recipes for different parts of a meal.
- **Functional:** Using functions to get results without worrying about steps.
- **Object-Oriented:** Objects that know how to do specific tasks and work together.

Think of each style as a different way to organize your cooking. Each has its own way to make things easier and more understandable, just like in programming!

### Imperative Programming
In imperative programming, you write code that explicitly tells the computer what to do, step by step. This style is straightforward and mirrors how the machine operates internally. It focuses on how to achieve the desired results.

**Python Example:**
```python
total = 0
for i in range(1, 11):
    total += i
print(total)
```

**Java Example:**
```java
int total = 0;
for (int i = 1; i <= 10; i++) {
    total += i;
}
System.out.println(total);
```
In both examples, you specify the exact sequence of operations to sum numbers from 1 to 10.

### Procedural Programming
Procedural programming is a subset of imperative programming. It structures code into procedures, also known as functions or subroutines, to make it more modular and reusable. This style encourages breaking down tasks into smaller, manageable functions.

**Python Example:**
```python
def sum_numbers(n):
    total = 0
    for i in range(1, n + 1):
        total += i
    return total

print(sum_numbers(10))
```

**Java Example:**
```java
public class Main {
    public static void main(String[] args) {
        System.out.println(sumNumbers(10));
    }

    public static int sumNumbers(int n) {
        int total = 0;
        for (int i = 1; i <= n; i++) {
            total += i;
        }
        return total;
    }
}
```
Here, the task of summing numbers is encapsulated in a procedure (`sum_numbers` or `sumNumbers`), which can be reused.

### Functional Programming
Functional programming treats computation as the evaluation of mathematical functions and avoids changing state and mutable data. It emphasizes the use of pure functions, higher-order functions, and immutability.

**Python Example:**
```python
from functools import reduce

numbers = range(1, 11)
total = reduce(lambda x, y: x + y, numbers)
print(total)
```

**Java Example (using Java Streams):**
```java
import java.util.stream.IntStream;

public class Main {
    public static void main(String[] args) {
        int total = IntStream.rangeClosed(1, 10).reduce(0, Integer::sum);
        System.out.println(total);
    }
}
```
In these examples, you avoid explicit loops and state changes, focusing on applying functions to achieve the result.

### Object-Oriented Programming
Object-oriented programming (OOP) organizes code into objects, which combine data (attributes) and behavior (methods). It emphasizes principles like encapsulation, inheritance, and polymorphism.

**Python Example:**
```python
class Summation:
    def __init__(self, n):
        self.n = n

    def sum_numbers(self):
        total = 0
        for i in range(1, self.n + 1):
            total += i
        return total

sum_obj = Summation(10)
print(sum_obj.sum_numbers())
```

**Java Example:**
```java
public class Summation {
    private int n;

    public Summation(int n) {
        this.n = n;
    }

    public int sumNumbers() {
        int total = 0;
        for (int i = 1; i <= n; i++) {
            total += i;
        }
        return total;
    }

    public static void main(String[] args) {
        Summation sumObj = new Summation(10);
        System.out.println(sumObj.sumNumbers());
    }
}
```
In these examples, the summing logic is encapsulated within a `Summation` class, which has both data (`n`) and behavior (`sum_numbers` or `sumNumbers`).

### Summary
- **Imperative:** Directly instructs the computer with explicit commands.
- **Procedural:** Organizes code into reusable procedures/functions.
- **Functional:** Emphasizes pure functions, immutability, and higher-order functions.
- **Object-Oriented:** Structures code around objects that contain both data and behavior, promoting encapsulation and modularity.

Understanding these styles helps you choose the right approach for different problems and makes your code more robust, maintainable, and scalable.

Certainly! Here’s a more technical explanation of these programming styles tailored for 17-year-old computer science students who are learning Python and Java:

### Imperative Programming
In imperative programming, you write code that explicitly tells the computer what to do, step by step. This style is straightforward and mirrors how the machine operates internally. It focuses on how to achieve the desired results.

**Python Example:**
```python
total = 0
for i in range(1, 11):
    total += i
print(total)
```

**Java Example:**
```java
int total = 0;
for (int i = 1; i <= 10; i++) {
    total += i;
}
System.out.println(total);
```
In both examples, you specify the exact sequence of operations to sum numbers from 1 to 10.

### Procedural Programming
Procedural programming is a subset of imperative programming. It structures code into procedures, also known as functions or subroutines, to make it more modular and reusable. This style encourages breaking down tasks into smaller, manageable functions.

**Python Example:**
```python
def sum_numbers(n):
    total = 0
    for i in range(1, n + 1):
        total += i
    return total

print(sum_numbers(10))
```

**Java Example:**
```java
public class Main {
    public static void main(String[] args) {
        System.out.println(sumNumbers(10));
    }

    public static int sumNumbers(int n) {
        int total = 0;
        for (int i = 1; i <= n; i++) {
            total += i;
        }
        return total;
    }
}
```
Here, the task of summing numbers is encapsulated in a procedure (`sum_numbers` or `sumNumbers`), which can be reused.

### Functional Programming
Functional programming treats computation as the evaluation of mathematical functions and avoids changing state and mutable data. It emphasizes the use of pure functions, higher-order functions, and immutability.

**Python Example:**
```python
from functools import reduce

numbers = range(1, 11)
total = reduce(lambda x, y: x + y, numbers)
print(total)
```

**Java Example (using Java Streams):**
```java
import java.util.stream.IntStream;

public class Main {
    public static void main(String[] args) {
        int total = IntStream.rangeClosed(1, 10).reduce(0, Integer::sum);
        System.out.println(total);
    }
}
```
In these examples, you avoid explicit loops and state changes, focusing on applying functions to achieve the result.

### Object-Oriented Programming
Object-oriented programming (OOP) organizes code into objects, which combine data (attributes) and behavior (methods). It emphasizes principles like encapsulation, inheritance, and polymorphism.

**Python Example:**
```python
class Summation:
    def __init__(self, n):
        self.n = n

    def sum_numbers(self):
        total = 0
        for i in range(1, self.n + 1):
            total += i
        return total

sum_obj = Summation(10)
print(sum_obj.sum_numbers())
```

**Java Example:**
```java
public class Summation {
    private int n;

    public Summation(int n) {
        this.n = n;
    }

    public int sumNumbers() {
        int total = 0;
        for (int i = 1; i <= n; i++) {
            total += i;
        }
        return total;
    }

    public static void main(String[] args) {
        Summation sumObj = new Summation(10);
        System.out.println(sumObj.sumNumbers());
    }
}
```
In these examples, the summing logic is encapsulated within a `Summation` class, which has both data (`n`) and behavior (`sum_numbers` or `sumNumbers`).

### Summary
- **Imperative:** Directly instructs the computer with explicit commands.
- **Procedural:** Organizes code into reusable procedures/functions.
- **Functional:** Emphasizes pure functions, immutability, and higher-order functions.
- **Object-Oriented:** Structures code around objects that contain both data and behavior, promoting encapsulation and modularity.

Understanding these styles helps you choose the right approach for different problems and makes your code more robust, maintainable, and scalable.









## School program written in Imperative Style 



The version I provided, though it simplifies the structure by merging the `DatabaseHelper` and `SchoolCLI` classes into the `School` class, is not necessarily more "imperative" in terms of programming style than the previous one. The imperative style focuses on explicitly detailing each step of the process, and the previous version already did this. The current version still uses structured exception handling, and key abstractions like JDBC resource management are handled similarly to the original.

To make this code more explicitly imperative in style, you could further reduce abstractions by eliminating features like `try-with-resources` and directly managing every aspect of the resource handling, while also avoiding abstractions that streamline processes. Here's an even more imperative-focused version:

### More Imperative Version:

1. Avoid abstraction of utility methods (such as using helper methods for resource handling).
2. More explicit control over resource management, like manual `Connection`, `PreparedStatement`, and `ResultSet` closing.

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.Scanner;

public class School {
    private static final String URL = "jdbc:mysql://localhost:3306/bootcamp";
    private static final String USER = "root";
    private static final String PASSWORD = "password123";

    // Add course
    public void addCourse(String courseName) {
        Connection conn = null;
        PreparedStatement stmt = null;

        try {
            // Step 1: Open connection
            conn = DriverManager.getConnection(URL, USER, PASSWORD);

            // Step 2: Prepare SQL query
            String query = "INSERT INTO Courses (course_name) VALUES (?)";
            stmt = conn.prepareStatement(query);
            stmt.setString(1, courseName);

            // Step 3: Execute query
            stmt.executeUpdate();
            System.out.println("Course '" + courseName + "' added.");
        } catch (SQLException e) {
            System.out.println("Error adding course: " + e.getMessage());
        } finally {
            // Step 4: Close resources
            if (stmt != null) {
                try {
                    stmt.close();
                } catch (SQLException e) {
                    System.out.println("Error closing statement: " + e.getMessage());
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    System.out.println("Error closing connection: " + e.getMessage());
                }
            }
        }
    }

    // Enroll student
    public void enrollStudent(int studentId, String studentName, String courseName) {
        Connection conn = null;
        PreparedStatement courseStmt = null;
        PreparedStatement studentStmt = null;
        PreparedStatement addStudentStmt = null;
        PreparedStatement enrollStmt = null;
        ResultSet courseRs = null;
        ResultSet studentRs = null;

        try {
            // Step 1: Open connection
            conn = DriverManager.getConnection(URL, USER, PASSWORD);

            // Step 2: Prepare and execute course query
            String courseQuery = "SELECT course_id FROM Courses WHERE course_name = ?";
            courseStmt = conn.prepareStatement(courseQuery);
            courseStmt.setString(1, courseName);
            courseRs = courseStmt.executeQuery();

            if (!courseRs.next()) {
                System.out.println("Error: Course '" + courseName + "' does not exist.");
                return;
            }
            int courseId = courseRs.getInt("course_id");

            // Step 3: Check if student exists
            String studentQuery = "SELECT student_id FROM Students WHERE student_id = ?";
            studentStmt = conn.prepareStatement(studentQuery);
            studentStmt.setInt(1, studentId);
            studentRs = studentStmt.executeQuery();

            if (!studentRs.next()) {
                // Step 4: Add student if not exists
                String addStudentQuery = "INSERT INTO Students (student_id, student_name) VALUES (?, ?)";
                addStudentStmt = conn.prepareStatement(addStudentQuery);
                addStudentStmt.setInt(1, studentId);
                addStudentStmt.setString(2, studentName);
                addStudentStmt.executeUpdate();
                System.out.println("Student '" + studentName + "' (ID: " + studentId + ") added.");
            }

            // Step 5: Enroll student in course
            String enrollQuery = "INSERT INTO Enrollments (course_id, student_id) VALUES (?, ?)";
            enrollStmt = conn.prepareStatement(enrollQuery);
            enrollStmt.setInt(1, courseId);
            enrollStmt.setInt(2, studentId);
            enrollStmt.executeUpdate();
            System.out.println("Student '" + studentId + "' enrolled in course '" + courseName + "'.");

        } catch (SQLException e) {
            System.out.println("Error enrolling student: " + e.getMessage());
        } finally {
            // Step 6: Close all resources
            try {
                if (courseRs != null) courseRs.close();
                if (studentRs != null) studentRs.close();
                if (courseStmt != null) courseStmt.close();
                if (studentStmt != null) studentStmt.close();
                if (addStudentStmt != null) addStudentStmt.close();
                if (enrollStmt != null) enrollStmt.close();
                if (conn != null) conn.close();
            } catch (SQLException e) {
                System.out.println("Error closing resources: " + e.getMessage());
            }
        }
    }

    // Assign grade
    public void assignGrade(int studentId, String courseName, double grade) {
        Connection conn = null;
        PreparedStatement courseStmt = null;
        PreparedStatement gradeStmt = null;
        ResultSet courseRs = null;

        try {
            // Step 1: Open connection
            conn = DriverManager.getConnection(URL, USER, PASSWORD);

            // Step 2: Prepare and execute course query
            String courseQuery = "SELECT course_id FROM Courses WHERE course_name = ?";
            courseStmt = conn.prepareStatement(courseQuery);
            courseStmt.setString(1, courseName);
            courseRs = courseStmt.executeQuery();

            if (courseRs.next()) {
                int courseId = courseRs.getInt("course_id");

                // Step 3: Prepare and execute grade insertion
                String gradeQuery = "INSERT INTO Grades (course_id, student_id, grade) VALUES (?, ?, ?)";
                gradeStmt = conn.prepareStatement(gradeQuery);
                gradeStmt.setInt(1, courseId);
                gradeStmt.setInt(2, studentId);
                gradeStmt.setDouble(3, grade);
                gradeStmt.executeUpdate();
                System.out.println("Grade '" + grade + "' assigned to student '" + studentId + "' in course '" + courseName + "'.");
            } else {
                System.out.println("Error: Course '" + courseName + "' does not exist.");
            }
        } catch (SQLException e) {
            System.out.println("Error assigning grade: " + e.getMessage());
        } finally {
            // Step 4: Close all resources
            try {
                if (courseRs != null) courseRs.close();
                if (courseStmt != null) courseStmt.close();
                if (gradeStmt != null) gradeStmt.close();
                if (conn != null) conn.close();
            } catch (SQLException e) {
                System.out.println("Error closing resources: " + e.getMessage());
            }
        }
    }

    // Command-line interface for school system
    public void startCLI() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the School Management System");

        while (true) {
            System.out.print("> ");
            String input = scanner.nextLine();
            String[] command = input.split(" ");

            switch (command[0]) {
                case "add_course":
                    addCourse(command[1]);
                    break;
                case "enroll_student":
                    enrollStudent(Integer.parseInt(command[2]), command[1], command[3]);
                    break;
                case "assign_grade":
                    assignGrade(Integer.parseInt(command[2]), command[1], Double.parseDouble(command[3]));
                    break;
                case "exit":
                    System.out.println("Exiting...");
                    return;
                default:
                    System.out.println("Unknown command");
            }
        }
    }

    public static void main(String[] args) {
        School school = new School();
        school.startCLI();
    }
}
```

### Imperative Changes:
1. **Step-by-Step Resource Handling**: Every individual step is explicitly written out, from connection creation to result closing, following a structured and linear approach.
2. **More Verbose Structure**: There is no abstraction of utility methods like `getConnection()`, and explicit steps are taken to handle each resource individually, which is typical of a more imperative style.

This version is more focused on detailing the step-by-step nature of the processes, which is a hallmark of imperative programming.

Here are the **JUnit 4.13.2** tests for the **imperative style** `School` class you provided. The tests will cover the following core functions: adding courses, enrolling students, and assigning grades.

### JUnit 4.13.2 Test Cases

```java
import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import static org.junit.Assert.*;

public class SchoolTest {

    private School school;

    // Utility method to clean up test data
    private void cleanupDatabase() {
        try (Connection conn = DriverManager.getConnection(School.URL, School.USER, School.PASSWORD)) {
            // Clear the Grades table first to handle foreign key constraint
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Grades")) {
                stmt.executeUpdate();
            }
            // Clear the Enrollments table
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Enrollments")) {
                stmt.executeUpdate();
            }
            // Clear the Courses table
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Courses")) {
                stmt.executeUpdate();
            }
            // Clear the Students table
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Students")) {
                stmt.executeUpdate();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }

    @Before
    public void setUp() {
        school = new School();
        cleanupDatabase();
    }

    @After
    public void tearDown() {
        cleanupDatabase();
    }

    // Test adding a course
    @Test
    public void testAddCourse() {
        school.addCourse("Mathematics");

        // Now verify if the course exists in the database
        try (Connection conn = DriverManager.getConnection(School.URL, School.USER, School.PASSWORD)) {
            String query = "SELECT course_id FROM Courses WHERE course_name = 'Mathematics'";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                assertTrue(stmt.executeQuery().next());
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }

    // Test enrolling a student
    @Test
    public void testEnrollStudent() {
        school.addCourse("History");
        school.enrollStudent(1, "John Doe", "History");

        // Verify if the student was enrolled in the course
        try (Connection conn = DriverManager.getConnection(School.URL, School.USER, School.PASSWORD)) {
            String query = "SELECT student_id FROM Enrollments WHERE student_id = 1";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                assertTrue(stmt.executeQuery().next());
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }

    // Test assigning a grade
    @Test
    public void testAssignGrade() {
        school.addCourse("Science");
        school.enrollStudent(2, "Jane Doe", "Science");
        school.assignGrade(2, "Science", 95.0);

        // Verify if the grade was assigned to the student
        try (Connection conn = DriverManager.getConnection(School.URL, School.USER, School.PASSWORD)) {
            String query = "SELECT grade FROM Grades WHERE student_id = 2 AND course_id = " +
                    "(SELECT course_id FROM Courses WHERE course_name = 'Science')";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                ResultSet rs = stmt.executeQuery();
                assertTrue(rs.next());
                assertEquals(95.0, rs.getDouble("grade"), 0.001);
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }

    // Test if assigning a grade to a non-existent course fails gracefully
    @Test
    public void testAssignGradeForNonExistentCourse() {
        school.assignGrade(3, "NonExistentCourse", 85.0);

        // Verify that no grade was assigned since the course does not exist
        try (Connection conn = DriverManager.getConnection(School.URL, School.USER, School.PASSWORD)) {
            String query = "SELECT grade FROM Grades WHERE student_id = 3";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                ResultSet rs = stmt.executeQuery();
                assertFalse(rs.next());
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }

    // Test enrolling a non-existent student (automatically adds the student)
    @Test
    public void testEnrollNonExistentStudent() {
        school.addCourse("Geography");
        school.enrollStudent(4, "New Student", "Geography");

        // Verify if the student was added to the Students table
        try (Connection conn = DriverManager.getConnection(School.URL, School.USER, School.PASSWORD)) {
            String query = "SELECT student_id FROM Students WHERE student_id = 4";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                ResultSet rs = stmt.executeQuery();
                assertTrue(rs.next());
                assertEquals(4, rs.getInt("student_id"));
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }
}
```

### Explanation of Test Cases:
1. **Database Setup/Cleanup**:
   - **`cleanupDatabase()`**: This utility function ensures a clean database state before and after each test by deleting rows from the dependent tables (`Grades`, `Enrollments`) first and then deleting rows from the parent tables (`Courses`, `Students`).
   - **`setUp()`**: Initializes the `School` object and cleans up the database before each test.
   - **`tearDown()`**: Cleans up the database after each test.

2. **Tests**:
   - **`testAddCourse()`**: Verifies that a course can be added to the database by checking the `Courses` table.
   - **`testEnrollStudent()`**: Verifies that a student can be enrolled in a course by checking the `Enrollments` table.
   - **`testAssignGrade()`**: Verifies that a grade can be assigned to a student in a course by checking the `Grades` table.
   - **`testAssignGradeForNonExistentCourse()`**: Verifies that trying to assign a grade to a non-existent course does not result in a grade being assigned.
   - **`testEnrollNonExistentStudent()`**: Verifies that enrolling a non-existent student adds the student to the `Students` table and then enrolls them in the course.

### Running the Tests:
Make sure you have the necessary **JUnit 4.13.2** and **Hamcrest 1.3** dependencies in your project to run the tests.

#### Maven Dependencies:

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.hamcrest</groupId>
    <artifactId>hamcrest-core</artifactId>
    <version>1.3</version>
    <scope>test</scope>
</dependency>
```

#### Gradle Dependencies:

```gradle
testImplementation 'junit:junit:4.13.2'
testImplementation 'org.hamcrest:hamcrest-core:1.3'
```

These tests ensure that the imperative-style `School` class functions correctly for core operations like adding courses, enrolling students, and assigning grades, while properly interacting with the database.





## Convert School into Procedural

To convert the program from an imperative to a more procedural style, we focus on separating functionality into individual procedures (or functions), while reducing the reliance on object-oriented principles like classes and encapsulation. Procedural programming emphasizes functions that operate on data, where data structures and logic are more separate.

Here are the key changes to convert the program to procedural style:

### Changes to make it procedural:

1. **Remove Classes**: Instead of encapsulating logic within classes like `School`, we define standalone functions that represent each operation (add course, enroll student, etc.).
2. **Separate Data and Functions**: In procedural programming, data is often kept separate from the functions that operate on it. However, since this program interacts with a database, we'll use global constants for database access.
3. **Use Global Variables/Constants**: The database connection details are now global constants instead of being encapsulated in a class.
4. **No Object Instances**: Instead of creating objects and calling methods on them (like `school.addCourse()`), we simply call standalone functions (like `addCourse()`).

### Procedural Style Code:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.Scanner;

// Global constants for database connection
final String URL = "jdbc:mysql://localhost:3306/bootcamp";
final String USER = "root";
final String PASSWORD = "password123";

// Function to get database connection
public Connection getConnection() throws SQLException {
    return DriverManager.getConnection(URL, USER, PASSWORD);
}

// Procedure to add a course
public void addCourse(String courseName) {
    Connection conn = null;
    PreparedStatement stmt = null;

    try {
        // Step 1: Open connection
        conn = getConnection();

        // Step 2: Prepare SQL query
        String query = "INSERT INTO Courses (course_name) VALUES (?)";
        stmt = conn.prepareStatement(query);
        stmt.setString(1, courseName);

        // Step 3: Execute query
        stmt.executeUpdate();
        System.out.println("Course '" + courseName + "' added.");
    } catch (SQLException e) {
        System.out.println("Error adding course: " + e.getMessage());
    } finally {
        // Step 4: Close resources
        closeResources(conn, stmt, null);
    }
}

// Procedure to enroll a student
public void enrollStudent(int studentId, String studentName, String courseName) {
    Connection conn = null;
    PreparedStatement courseStmt = null;
    PreparedStatement studentStmt = null;
    PreparedStatement addStudentStmt = null;
    PreparedStatement enrollStmt = null;
    ResultSet courseRs = null;
    ResultSet studentRs = null;

    try {
        // Step 1: Open connection
        conn = getConnection();

        // Step 2: Prepare and execute course query
        String courseQuery = "SELECT course_id FROM Courses WHERE course_name = ?";
        courseStmt = conn.prepareStatement(courseQuery);
        courseStmt.setString(1, courseName);
        courseRs = courseStmt.executeQuery();

        if (!courseRs.next()) {
            System.out.println("Error: Course '" + courseName + "' does not exist.");
            return;
        }
        int courseId = courseRs.getInt("course_id");

        // Step 3: Check if student exists
        String studentQuery = "SELECT student_id FROM Students WHERE student_id = ?";
        studentStmt = conn.prepareStatement(studentQuery);
        studentStmt.setInt(1, studentId);
        studentRs = studentStmt.executeQuery();

        if (!studentRs.next()) {
            // Step 4: Add student if not exists
            String addStudentQuery = "INSERT INTO Students (student_id, student_name) VALUES (?, ?)";
            addStudentStmt = conn.prepareStatement(addStudentQuery);
            addStudentStmt.setInt(1, studentId);
            addStudentStmt.setString(2, studentName);
            addStudentStmt.executeUpdate();
            System.out.println("Student '" + studentName + "' (ID: " + studentId + ") added.");
        }

        // Step 5: Enroll student in course
        String enrollQuery = "INSERT INTO Enrollments (course_id, student_id) VALUES (?, ?)";
        enrollStmt = conn.prepareStatement(enrollQuery);
        enrollStmt.setInt(1, courseId);
        enrollStmt.setInt(2, studentId);
        enrollStmt.executeUpdate();
        System.out.println("Student '" + studentId + "' enrolled in course '" + courseName + "'.");

    } catch (SQLException e) {
        System.out.println("Error enrolling student: " + e.getMessage());
    } finally {
        // Step 6: Close all resources
        closeResources(conn, courseStmt, courseRs);
        closeResources(conn, studentStmt, studentRs);
        closeResources(conn, addStudentStmt, null);
        closeResources(conn, enrollStmt, null);
    }
}

// Procedure to assign a grade
public void assignGrade(int studentId, String courseName, double grade) {
    Connection conn = null;
    PreparedStatement courseStmt = null;
    PreparedStatement gradeStmt = null;
    ResultSet courseRs = null;

    try {
        // Step 1: Open connection
        conn = getConnection();

        // Step 2: Prepare and execute course query
        String courseQuery = "SELECT course_id FROM Courses WHERE course_name = ?";
        courseStmt = conn.prepareStatement(courseQuery);
        courseStmt.setString(1, courseName);
        courseRs = courseStmt.executeQuery();

        if (courseRs.next()) {
            int courseId = courseRs.getInt("course_id");

            // Step 3: Prepare and execute grade insertion
            String gradeQuery = "INSERT INTO Grades (course_id, student_id, grade) VALUES (?, ?, ?)";
            gradeStmt = conn.prepareStatement(gradeQuery);
            gradeStmt.setInt(1, courseId);
            gradeStmt.setInt(2, studentId);
            gradeStmt.setDouble(3, grade);
            gradeStmt.executeUpdate();
            System.out.println("Grade '" + grade + "' assigned to student '" + studentId + "' in course '" + courseName + "'.");
        } else {
            System.out.println("Error: Course '" + courseName + "' does not exist.");
        }
    } catch (SQLException e) {
        System.out.println("Error assigning grade: " + e.getMessage());
    } finally {
        // Step 4: Close all resources
        closeResources(conn, courseStmt, courseRs);
        closeResources(conn, gradeStmt, null);
    }
}

// Utility function to close resources
public void closeResources(Connection conn, PreparedStatement stmt, ResultSet rs) {
    try {
        if (rs != null) rs.close();
        if (stmt != null) stmt.close();
        if (conn != null) conn.close();
    } catch (SQLException e) {
        System.out.println("Error closing resources: " + e.getMessage());
    }
}

// Main function to handle CLI
public void startCLI() {
    Scanner scanner = new Scanner(System.in);
    System.out.println("Welcome to the School Management System");

    while (true) {
        System.out.print("> ");
        String input = scanner.nextLine();
        String[] command = input.split(" ");

        switch (command[0]) {
            case "add_course":
                addCourse(command[1]);
                break;
            case "enroll_student":
                enrollStudent(Integer.parseInt(command[2]), command[1], command[3]);
                break;
            case "assign_grade":
                assignGrade(Integer.parseInt(command[2]), command[1], Double.parseDouble(command[3]));
                break;
            case "exit":
                System.out.println("Exiting...");
                return;
            default:
                System.out.println("Unknown command");
        }
    }
}

// Main entry point
public static void main(String[] args) {
    startCLI();
}
```

### Key Changes for Procedural Style:
1. **Global Constants**: The database connection details are now global variables (`URL`, `USER`, `PASSWORD`) instead of being encapsulated in a class.
2. **Standalone Functions**: Functions like `addCourse()`, `enrollStudent()`, and `assignGrade()` are now standalone procedures, no longer tied to a class or instance.
3. **No Object-Oriented Concepts**: There is no concept of objects or instances. All functionality is handled by functions, and the data (e.g., course name, student ID) is passed directly to them.
4. **Utility Functions**: The resource handling logic (such as closing `ResultSet`, `PreparedStatement`, `Connection`) is separated into a utility function `closeResources()` to avoid repetition and encapsulate common behavior.
5. **Global Access**: All functions operate independently, and shared state is accessed globally.

By structuring the code in this way, we’ve moved from an object-oriented imperative style to a more purely procedural approach where functions handle all operations without classes or objects, making the program more focused on processes rather than state management.



To write **JUnit 4.13.2** tests for the **`SchoolProcedural`** class, we need to test the core functions such as adding courses, enrolling students, and assigning grades. Each test will ensure the correct functionality by interacting with a real (or mock) database.

Here are the JUnit 4.13.2 tests for the **procedural style** code you provided.

### JUnit 4.13.2 Test Cases

```java
import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Optional;

import static org.junit.Assert.*;

public class SchoolProceduralTest {

    private SchoolProcedural school;

    // Utility method to clean up test data
    private void cleanupDatabase() {
        try (Connection conn = school.getConnection()) {
            // Clear the Enrollments, Courses, Students, and Grades tables
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Enrollments")) {
                stmt.executeUpdate();
            }
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Courses")) {
                stmt.executeUpdate();
            }
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Students")) {
                stmt.executeUpdate();
            }
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Grades")) {
                stmt.executeUpdate();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }

    @Before
    public void setUp() {
        school = new SchoolProcedural();
        cleanupDatabase();
    }

    @After
    public void tearDown() {
        cleanupDatabase();
    }

    // Test adding a course procedurally
    @Test
    public void testAddCourse() {
        school.addCourse("Mathematics");

        // Now verify if the course exists in the database
        try (Connection conn = school.getConnection()) {
            String query = "SELECT course_id FROM Courses WHERE course_name = 'Mathematics'";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                assertTrue(stmt.executeQuery().next());
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }

    // Test enrolling a student procedurally
    @Test
    public void testEnrollStudent() {
        school.addCourse("History");
        school.enrollStudent(1, "John Doe", "History");

        // Verify if the student was enrolled in the course
        try (Connection conn = school.getConnection()) {
            String query = "SELECT student_id FROM Enrollments WHERE student_id = 1";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                assertTrue(stmt.executeQuery().next());
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }

    // Test assigning a grade procedurally
    @Test
    public void testAssignGrade() {
        school.addCourse("Science");
        school.enrollStudent(2, "Jane Doe", "Science");
        school.assignGrade(2, "Science", 95.0);

        // Verify if the grade was assigned to the student
        try (Connection conn = school.getConnection()) {
            String query = "SELECT grade FROM Grades WHERE student_id = 2 AND course_id = " +
                    "(SELECT course_id FROM Courses WHERE course_name = 'Science')";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                ResultSet rs = stmt.executeQuery();
                assertTrue(rs.next());
                assertEquals(95.0, rs.getDouble("grade"), 0.001);
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }

    // Test if a course that does not exist fails correctly when assigning a grade
    @Test
    public void testAssignGradeForNonExistentCourse() {
        school.assignGrade(3, "NonExistentCourse", 85.0);

        // Verify that no grade was assigned since the course does not exist
        try (Connection conn = school.getConnection()) {
            String query = "SELECT grade FROM Grades WHERE student_id = 3";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                ResultSet rs = stmt.executeQuery();
                assertFalse(rs.next());
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }

    // Test if a student is added when trying to enroll a non-existent student
    @Test
    public void testEnrollNonExistentStudent() {
        school.addCourse("Geography");
        school.enrollStudent(4, "New Student", "Geography");

        // Verify if the student was added to the Students table
        try (Connection conn = school.getConnection()) {
            String query = "SELECT student_id FROM Students WHERE student_id = 4";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                ResultSet rs = stmt.executeQuery();
                assertTrue(rs.next());
                assertEquals(4, rs.getInt("student_id"));
            }
        } catch (SQLException e) {
            fail("Exception occurred: " + e.getMessage());
        }
    }
}
```

### Explanation:

1. **Database Setup/Cleanup**:
   - **`cleanupDatabase()`**: This method clears the relevant tables before and after each test, ensuring each test runs in isolation without being affected by the data from previous tests.

2. **Tests**:
   - **`testAddCourse()`**: This test adds a course and then verifies if the course was correctly inserted into the database by querying the `Courses` table.
   - **`testEnrollStudent()`**: This test adds a course, enrolls a student in the course, and then checks if the enrollment was recorded in the `Enrollments` table.
   - **`testAssignGrade()`**: This test adds a course, enrolls a student, assigns a grade, and then checks if the grade was correctly recorded in the `Grades` table.
   - **`testAssignGradeForNonExistentCourse()`**: This test tries to assign a grade for a non-existent course and verifies that no grade is assigned.
   - **`testEnrollNonExistentStudent()`**: This test enrolls a new student who does not exist yet and verifies that the student was added to the `Students` table.

3. **Assertions**:
   - **`assertTrue()`** and **`assertFalse()`**: These assertions check the presence or absence of data in the database.
   - **`assertEquals()`**: This checks that the correct values (such as the assigned grade) are present in the database.

### Running the Tests:
Ensure you have **JUnit 4.13.2** and **Hamcrest 1.3** in your project dependencies. You can run the tests using your IDE, Maven, or Gradle.

#### Maven Dependencies:

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.hamcrest</groupId>
    <artifactId>hamcrest-core</artifactId>
    <version>1.3</version>
    <scope>test</scope>
</dependency>
```

#### Gradle Dependencies:

```gradle
testImplementation 'junit:junit:4.13.2'
testImplementation 'org.hamcrest:hamcrest-core:1.3'
```

These tests ensure that your procedural `SchoolProcedural` code works as expected by interacting with the database and verifying the results.



## Convert School into Functional Programming Style

To shift this code from a procedural style to a **functional programming style**, we need to focus on immutability, higher-order functions, avoiding side effects, and separating logic from state management as much as possible. In Java, functional programming isn't as native as in languages like Haskell or Scala, but with features like **lambdas**, **streams**, and **optional**, we can approximate it. Below are the key changes and the transformed code.

### Key Changes for Functional Programming:
1. **Immutable Data**: Avoid mutating variables or using side effects. Wherever possible, use final variables and avoid modifying state.
2. **Pure Functions**: Each function should be "pure," meaning it doesn't cause side effects or rely on external mutable states.
3. **Functional Composition**: Use higher-order functions like `map`, `filter`, and `flatMap` for operations instead of imperative loops.
4. **Stream API**: Replace traditional loops with functional operations on collections using streams.
5. **Optional API**: Use `Optional` to handle null values or absent data in a functional way.
6. **Avoid Global State**: Instead of using global variables or state, functions receive all needed parameters and return results directly.

Here’s the code in a more functional programming style:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.Optional;
import java.util.Scanner;
import java.util.stream.Stream;

// Database connection function (no global variables)
public Connection getConnection() {
    try {
        return DriverManager.getConnection("jdbc:mysql://localhost:3306/bootcamp", "root", "password123");
    } catch (SQLException e) {
        throw new RuntimeException(e);
    }
}

// Functional interface for handling database interactions
@FunctionalInterface
interface DBAction<T> {
    T execute(Connection conn) throws SQLException;
}

// Higher-order function to handle database operations
public <T> Optional<T> withConnection(DBAction<T> action) {
    try (Connection conn = getConnection()) {
        return Optional.ofNullable(action.execute(conn));
    } catch (SQLException e) {
        System.out.println("Database error: " + e.getMessage());
        return Optional.empty();
    }
}

// Add course function (pure function)
public Optional<String> addCourse(String courseName) {
    return withConnection(conn -> {
        String query = "INSERT INTO Courses (course_name) VALUES (?)";
        try (PreparedStatement stmt = conn.prepareStatement(query)) {
            stmt.setString(1, courseName);
            stmt.executeUpdate();
            return "Course '" + courseName + "' added.";
        }
    });
}

// Check if course exists (returns Optional)
public Optional<Integer> findCourseIdByName(String courseName) {
    return withConnection(conn -> {
        String query = "SELECT course_id FROM Courses WHERE course_name = ?";
        try (PreparedStatement stmt = conn.prepareStatement(query)) {
            stmt.setString(1, courseName);
            try (ResultSet rs = stmt.executeQuery()) {
                return rs.next() ? rs.getInt("course_id") : null;
            }
        }
    });
}

// Add student (pure function)
public Optional<String> addStudent(int studentId, String studentName) {
    return withConnection(conn -> {
        String query = "INSERT INTO Students (student_id, student_name) VALUES (?, ?)";
        try (PreparedStatement stmt = conn.prepareStatement(query)) {
            stmt.setInt(1, studentId);
            stmt.setString(2, studentName);
            stmt.executeUpdate();
            return "Student '" + studentName + "' added.";
        }
    });
}

// Check if student exists (returns Optional)
public Optional<Integer> findStudentById(int studentId) {
    return withConnection(conn -> {
        String query = "SELECT student_id FROM Students WHERE student_id = ?";
        try (PreparedStatement stmt = conn.prepareStatement(query)) {
            stmt.setInt(1, studentId);
            try (ResultSet rs = stmt.executeQuery()) {
                return rs.next() ? rs.getInt("student_id") : null;
            }
        }
    });
}

// Enroll student in course (functional composition of pure functions)
public Optional<String> enrollStudent(int studentId, String studentName, String courseName) {
    return findCourseIdByName(courseName).flatMap(courseId -> {
        return findStudentById(studentId)
            .or(() -> addStudent(studentId, studentName).map(s -> studentId))
            .flatMap(id -> withConnection(conn -> {
                String enrollQuery = "INSERT INTO Enrollments (course_id, student_id) VALUES (?, ?)";
                try (PreparedStatement stmt = conn.prepareStatement(enrollQuery)) {
                    stmt.setInt(1, courseId);
                    stmt.setInt(2, studentId);
                    stmt.executeUpdate();
                    return "Student '" + studentId + "' enrolled in course '" + courseName + "'.";
                }
            }));
    });
}

// Assign grade (pure function using functional composition)
public Optional<String> assignGrade(int studentId, String courseName, double grade) {
    return findCourseIdByName(courseName).flatMap(courseId -> {
        return findStudentById(studentId).flatMap(id -> withConnection(conn -> {
            String gradeQuery = "INSERT INTO Grades (course_id, student_id, grade) VALUES (?, ?, ?)";
            try (PreparedStatement stmt = conn.prepareStatement(gradeQuery)) {
                stmt.setInt(1, courseId);
                stmt.setInt(2, studentId);
                stmt.setDouble(3, grade);
                stmt.executeUpdate();
                return "Grade '" + grade + "' assigned to student '" + studentId + "' in course '" + courseName + "'.";
            }
        }));
    });
}

// Main CLI function (functional, uses Optional and Streams)
public void startCLI() {
    Scanner scanner = new Scanner(System.in);
    System.out.println("Welcome to the School Management System");

    Stream.generate(scanner::nextLine)
        .map(input -> input.split(" "))
        .takeWhile(command -> !command[0].equals("exit"))
        .forEach(command -> {
            switch (command[0]) {
                case "add_course":
                    addCourse(command[1]).ifPresent(System.out::println);
                    break;
                case "enroll_student":
                    enrollStudent(Integer.parseInt(command[2]), command[1], command[3]).ifPresent(System.out::println);
                    break;
                case "assign_grade":
                    assignGrade(Integer.parseInt(command[2]), command[1], Double.parseDouble(command[3])).ifPresent(System.out::println);
                    break;
                default:
                    System.out.println("Unknown command");
            }
        });
    System.out.println("Exiting...");
}

public static void main(String[] args) {
    new School().startCLI();
}
```

### Key Changes for Functional Style:

1. **Higher-Order Functions**: We introduce a `withConnection()` function, which abstracts the connection handling and takes a lambda to execute the database operation. This avoids code duplication and ensures all database operations are handled functionally.
   
2. **Pure Functions**: Functions like `addCourse()`, `findCourseIdByName()`, and `enrollStudent()` are pure functions that return results without modifying global state or causing side effects. Each function works purely based on its input and produces an output, with no hidden state changes.

3. **Optional and FlatMap**: Instead of using `if` statements to check for the existence of courses or students, we use `Optional` and `flatMap()` to chain together operations. If any part of the chain fails (e.g., the course or student doesn’t exist), the entire chain fails gracefully without exceptions.

4. **Immutable Data**: No variables are mutated; instead, we use chained method calls and immutable results. Data is passed into and returned from functions, rather than being updated in place.

5. **Streams API**: The command-line interface (`startCLI()`) uses `Stream.generate()` to continuously process user input, and `takeWhile()` is used to end the loop when the user types "exit". This avoids an explicit loop construct.

6. **Declarative Logic**: The logic is now more declarative, where we define "what" should happen (e.g., map over input, flatMap results) rather than "how" to achieve it (e.g., using loops, conditions).

### Functional Programming Benefits:
- **Better Abstraction**: By using higher-order functions like `withConnection()`, we abstract common patterns such as resource management.
- **Easier Testing**: Pure functions are easier to test since they don’t rely on external mutable state.
- **Reduced Side Effects**: By working with `Optional` and functional constructs, there are fewer chances for null pointer exceptions or resource leaks.
  

This approach gives the program a more functional programming style while maintaining Java's syntax and idioms.



Following are **JUnit 4.13.2** test cases for the functional style `School` class. These tests will cover the core functionalities like adding courses, adding students, enrolling students, and assigning grades.

### JUnit 4.13.2 Test Cases

```java
import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Optional;

import static org.junit.Assert.*;

public class SchoolTest {

    private School school;

    // Utility method to clean up test data
    private void cleanupDatabase() {
        try (Connection conn = school.getConnection()) {
            // Clear the Enrollments, Courses, Students, and Grades tables
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Enrollments")) {
                stmt.executeUpdate();
            }
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Courses")) {
                stmt.executeUpdate();
            }
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Students")) {
                stmt.executeUpdate();
            }
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Grades")) {
                stmt.executeUpdate();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }

    @Before
    public void setUp() {
        school = new School();
        cleanupDatabase();
    }

    @After
    public void tearDown() {
        cleanupDatabase();
    }

    // Test adding a course functionally
    @Test
    public void testAddCourseFunction() {
        Optional<String> result = school.addCourse("Mathematics");
        assertTrue(result.isPresent());
        assertEquals("Course 'Mathematics' added.", result.get());

        Optional<Integer> courseId = school.findCourseIdByName("Mathematics");
        assertTrue(courseId.isPresent());
    }

    // Test finding a course by name functionally
    @Test
    public void testFindCourseIdFunction() {
        school.addCourse("Science");
        Optional<Integer> courseId = school.findCourseIdByName("Science");
        assertTrue(courseId.isPresent());
    }

    // Test adding a student functionally
    @Test
    public void testAddStudentFunction() {
        Optional<String> result = school.addStudent(1, "John Doe");
        assertTrue(result.isPresent());
        assertEquals("Student 'John Doe' added.", result.get());

        Optional<Integer> studentId = school.findStudentById(1);
        assertTrue(studentId.isPresent());
    }

    // Test finding a student by ID functionally
    @Test
    public void testFindStudentByIdFunction() {
        school.addStudent(2, "Jane Smith");
        Optional<Integer> foundStudent = school.findStudentById(2);
        assertTrue(foundStudent.isPresent());
        assertEquals((Integer) 2, foundStudent.get());
    }

    // Test enrolling a student in a course functionally
    @Test
    public void testEnrollStudentFunction() {
        school.addCourse("History");
        Optional<String> result = school.enrollStudent(1, "Alice", "History");
        assertTrue(result.isPresent());
        assertEquals("Student '1' enrolled in course 'History'.", result.get());

        Optional<Integer> studentId = school.findStudentById(1);
        assertTrue(studentId.isPresent());
    }

    // Test assigning a grade to a student in a course functionally
    @Test
    public void testAssignGradeFunction() {
        school.addCourse("Geography");
        school.enrollStudent(1, "Bob", "Geography");

        Optional<String> result = school.assignGrade(1, "Geography", 95.0);
        assertTrue(result.isPresent());
        assertEquals("Grade '95.0' assigned to student '1' in course 'Geography'.", result.get());
    }
}
```

### Test Breakdown:
1. **Database Setup and Cleanup**:
   - **`cleanupDatabase()`**: This utility function clears all data from the database before and after each test to ensure each test runs in isolation.
   
2. **Tests**:
   - **`testAddCourseFunction()`**: Tests adding a new course and ensures it can be retrieved by its name.
   - **`testFindCourseIdFunction()`**: Tests finding a course by name to ensure the correct `Optional<Integer>` course ID is returned.
   - **`testAddStudentFunction()`**: Tests adding a student and verifies the result is an `Optional<String>` containing a success message.
   - **`testFindStudentByIdFunction()`**: Tests finding a student by ID and asserts that the correct `Optional<Integer>` student ID is returned.
   - **`testEnrollStudentFunction()`**: Tests enrolling a student in a course and ensures the student is enrolled, with a success message returned in `Optional<String>`.
   - **`testAssignGradeFunction()`**: Tests assigning a grade to a student in a course and ensures the grade is assigned correctly with a success message in `Optional<String>`.

3. **Assertions**:
   - **`assertTrue()`**: Ensures that `Optional` values are present, confirming that the course, student, or enrollment operation succeeded.
   - **`assertEquals()`**: Verifies that the returned results from the functional operations match the expected values (e.g., success messages).

### Running the Tests:
To run these tests, ensure that **JUnit 4.13.2** and **Hamcrest 1.3** (required for assertions) are included in your project dependencies.

#### Maven Dependencies:

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.hamcrest</groupId>
    <artifactId>hamcrest-core</artifactId>
    <version>1.3</version>
    <scope>test</scope>
</dependency>
```

#### Gradle Dependencies:

```gradle
testImplementation 'junit:junit:4.13.2'
testImplementation 'org.hamcrest:hamcrest-core:1.3'
```

These tests ensure that the functional-style implementation of the `School` class works as expected, validating the core functionalities of adding courses, adding students, enrolling students, and assigning grades.



## Convert School into OOP programming Style 

To shift the code into **Object-Oriented Programming (OOP)** style, we focus on encapsulating functionality within classes, using objects to represent real-world entities, and leveraging principles such as **encapsulation**, **inheritance**, and **polymorphism**.

Here’s how the code can be restructured to follow an OOP style:

### Key Changes for OOP Style:
1. **Encapsulation**: Group related behavior and data inside objects (e.g., `Course`, `Student`, `School`). This improves modularity and hides implementation details.
2. **Separation of Concerns**: Divide the program into multiple classes, each with clear responsibilities (e.g., database access, course management, student management).
3. **Use of Objects**: Represent `Student` and `Course` as classes, encapsulating their properties and behaviors inside objects.
4. **Class Relationships**: Use composition and relationships between objects, such as a `School` containing `Student` and `Course` objects.
5. **Single Responsibility**: Each class handles a single responsibility (e.g., `School` manages overall school operations, `DatabaseHelper` handles database connections, `Course` represents course-related operations, etc.).

Here’s the OOP version of the program:

### Object-Oriented Version:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.Optional;
import java.util.Scanner;

// Database Helper Class
class DatabaseHelper {
    private static final String URL = "jdbc:mysql://localhost:3306/bootcamp";
    private static final String USER = "root";
    private static final String PASSWORD = "password123";

    // Method to get database connection
    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(URL, USER, PASSWORD);
    }
}

// Course Class
class Course {
    private String name;

    public Course(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    // Add course to the database
    public void addCourse() {
        try (Connection conn = DatabaseHelper.getConnection()) {
            String query = "INSERT INTO Courses (course_name) VALUES (?)";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                stmt.setString(1, this.name);
                stmt.executeUpdate();
                System.out.println("Course '" + this.name + "' added.");
            }
        } catch (SQLException e) {
            System.out.println("Error adding course: " + e.getMessage());
        }
    }

    // Find course ID by course name
    public static Optional<Integer> findCourseId(String courseName) {
        try (Connection conn = DatabaseHelper.getConnection()) {
            String query = "SELECT course_id FROM Courses WHERE course_name = ?";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                stmt.setString(1, courseName);
                try (ResultSet rs = stmt.executeQuery()) {
                    if (rs.next()) {
                        return Optional.of(rs.getInt("course_id"));
                    } else {
                        return Optional.empty();
                    }
                }
            }
        } catch (SQLException e) {
            System.out.println("Error finding course: " + e.getMessage());
            return Optional.empty();
        }
    }
}

// Student Class
class Student {
    private int id;
    private String name;

    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    // Add student to the database
    public void addStudent() {
        try (Connection conn = DatabaseHelper.getConnection()) {
            String query = "INSERT INTO Students (student_id, student_name) VALUES (?, ?)";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                stmt.setInt(1, this.id);
                stmt.setString(2, this.name);
                stmt.executeUpdate();
                System.out.println("Student '" + this.name + "' added.");
            }
        } catch (SQLException e) {
            System.out.println("Error adding student: " + e.getMessage());
        }
    }

    // Find student by ID
    public static Optional<Student> findStudentById(int studentId) {
        try (Connection conn = DatabaseHelper.getConnection()) {
            String query = "SELECT student_id, student_name FROM Students WHERE student_id = ?";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                stmt.setInt(1, studentId);
                try (ResultSet rs = stmt.executeQuery()) {
                    if (rs.next()) {
                        return Optional.of(new Student(rs.getInt("student_id"), rs.getString("student_name")));
                    } else {
                        return Optional.empty();
                    }
                }
            }
        } catch (SQLException e) {
            System.out.println("Error finding student: " + e.getMessage());
            return Optional.empty();
        }
    }
}

// School Class - Manages operations at the school level
class School {
    // Enroll a student in a course
    public void enrollStudent(int studentId, String studentName, String courseName) {
        Optional<Integer> courseIdOpt = Course.findCourseId(courseName);
        if (!courseIdOpt.isPresent()) {
            System.out.println("Error: Course '" + courseName + "' does not exist.");
            return;
        }
        int courseId = courseIdOpt.get();

        Optional<Student> studentOpt = Student.findStudentById(studentId);
        if (!studentOpt.isPresent()) {
            Student newStudent = new Student(studentId, studentName);
            newStudent.addStudent();
        }

        try (Connection conn = DatabaseHelper.getConnection()) {
            String query = "INSERT INTO Enrollments (course_id, student_id) VALUES (?, ?)";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                stmt.setInt(1, courseId);
                stmt.setInt(2, studentId);
                stmt.executeUpdate();
                System.out.println("Student '" + studentId + "' enrolled in course '" + courseName + "'.");
            }
        } catch (SQLException e) {
            System.out.println("Error enrolling student: " + e.getMessage());
        }
    }

    // Assign grade to a student in a course
    public void assignGrade(int studentId, String courseName, double grade) {
        Optional<Integer> courseIdOpt = Course.findCourseId(courseName);
        if (!courseIdOpt.isPresent()) {
            System.out.println("Error: Course '" + courseName + "' does not exist.");
            return;
        }
        int courseId = courseIdOpt.get();

        Optional<Student> studentOpt = Student.findStudentById(studentId);
        if (!studentOpt.isPresent()) {
            System.out.println("Error: Student with ID '" + studentId + "' does not exist.");
            return;
        }

        try (Connection conn = DatabaseHelper.getConnection()) {
            String query = "INSERT INTO Grades (course_id, student_id, grade) VALUES (?, ?, ?)";
            try (PreparedStatement stmt = conn.prepareStatement(query)) {
                stmt.setInt(1, courseId);
                stmt.setInt(2, studentId);
                stmt.setDouble(3, grade);
                stmt.executeUpdate();
                System.out.println("Grade '" + grade + "' assigned to student '" + studentId + "' in course '" + courseName + "'.");
            }
        } catch (SQLException e) {
            System.out.println("Error assigning grade: " + e.getMessage());
        }
    }
}

// Command Line Interface for managing school
class SchoolCLI {
    private final School school;

    public SchoolCLI(School school) {
        this.school = school;
    }

    public void start() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the School Management System");

        while (true) {
            System.out.print("> ");
            String input = scanner.nextLine();
            String[] command = input.split(" ");

            switch (command[0]) {
                case "add_course":
                    new Course(command[1]).addCourse();
                    break;
                case "enroll_student":
                    school.enrollStudent(Integer.parseInt(command[2]), command[1], command[3]);
                    break;
                case "assign_grade":
                    school.assignGrade(Integer.parseInt(command[2]), command[1], Double.parseDouble(command[3]));
                    break;
                case "exit":
                    System.out.println("Exiting...");
                    return;
                default:
                    System.out.println("Unknown command");
            }
        }
    }
}

// Main Class - Entry point to the program
public class Main {
    public static void main(String[] args) {
        School school = new School();
        SchoolCLI cli = new SchoolCLI(school);
        cli.start();
    }
}
```

### Key Changes for OOP Style:
1. **Encapsulation**: The logic for courses, students, and school operations is encapsulated in distinct classes (`Course`, `Student`, `School`, and `DatabaseHelper`).
   - Each class is responsible for its own behavior, making the code easier to maintain.
   - Classes `Course` and `Student` encapsulate the properties (`name`, `id`) and operations (`addCourse()`, `addStudent()`) related to courses and students, respectively.

2. **Separation of Concerns**: 
   - The `School` class manages high-level operations like enrolling students and assigning grades.
   - `DatabaseHelper` is responsible for managing the database connection.
   - `SchoolCLI` handles the command-line interface.

3. **Class Relationships**: The `School` class interacts with `Student` and `Course` objects to manage student enrollments and grade assignments. This creates clear relationships between classes.****



---

To write tests using **JUnit 4.13.2**, we'll focus on the core components of the OOP code. we use assertions to verify that operations behave correctly, mock database interactions where necessary, and clean up the test data after each test to ensure a consistent state for all tests.

### Key Components to Test:
1. **`Course` class**:
   - Test adding a course to the database.
   - Test finding a course by name.
   
2. **`Student` class**:
   - Test adding a student to the database.
   - Test finding a student by ID.

3. **`School` class**:
   - Test enrolling a student in a course.
   - Test assigning a grade to a student.

### Example Test Class for JUnit 4.13.2:

```java
import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Optional;

import static org.junit.Assert.*;

public class SchoolSystemTest {

    // Utility method to clean up test data
    private void cleanupDatabase() {
        try (Connection conn = DatabaseHelper.getConnection()) {
            // Clear the Enrollments, Courses, Students, and Grades tables
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Enrollments")) {
                stmt.executeUpdate();
            }
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Courses")) {
                stmt.executeUpdate();
            }
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Students")) {
                stmt.executeUpdate();
            }
            try (PreparedStatement stmt = conn.prepareStatement("DELETE FROM Grades")) {
                stmt.executeUpdate();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }

    @Before
    public void setUp() {
        cleanupDatabase();
    }

    @After
    public void tearDown() {
        cleanupDatabase();
    }

    // Test adding a course
    @Test
    public void testAddCourse() {
        Course course = new Course("Mathematics");
        course.addCourse();

        Optional<Integer> courseId = Course.findCourseId("Mathematics");
        assertTrue(courseId.isPresent());
    }

    // Test finding a course by name
    @Test
    public void testFindCourseId() {
        Course course = new Course("Science");
        course.addCourse();

        Optional<Integer> courseId = Course.findCourseId("Science");
        assertTrue(courseId.isPresent());
        assertEquals("Science", course.getName());
    }

    // Test adding a student
    @Test
    public void testAddStudent() {
        Student student = new Student(1, "John Doe");
        student.addStudent();

        Optional<Student> foundStudent = Student.findStudentById(1);
        assertTrue(foundStudent.isPresent());
        assertEquals("John Doe", foundStudent.get().getName());
    }

    // Test finding a student by ID
    @Test
    public void testFindStudentById() {
        Student student = new Student(2, "Jane Smith");
        student.addStudent();

        Optional<Student> foundStudent = Student.findStudentById(2);
        assertTrue(foundStudent.isPresent());
        assertEquals(2, foundStudent.get().getId());
        assertEquals("Jane Smith", foundStudent.get().getName());
    }

    // Test enrolling a student in a course
    @Test
    public void testEnrollStudent() {
        School school = new School();
        Course course = new Course("History");
        course.addCourse();

        school.enrollStudent(1, "Alice", "History");

        Optional<Student> student = Student.findStudentById(1);
        assertTrue(student.isPresent());
    }

    // Test assigning a grade to a student
    @Test
    public void testAssignGrade() {
        School school = new School();
        Course course = new Course("Geography");
        course.addCourse();
        school.enrollStudent(1, "Bob", "Geography");

        school.assignGrade(1, "Geography", 95.0);

        // Assuming there is a method to check grades (not implemented in the initial code).
        // You could add a method to verify grades in the database.
        // Optional<Double> grade = findGradeForStudent(1, "Geography");
        // assertTrue(grade.isPresent());
        // assertEquals(95.0, grade.get(), 0.01);
    }
}
```

### Explanation:

1. **Database Setup/Cleanup**:
   - **`cleanupDatabase()`**: This utility method clears all the test data from the database. It runs before (`@Before`) and after (`@After`) each test to ensure that tests run in isolation.

2. **Tests**:
   - **`testAddCourse()`**: Tests adding a new course and ensures it can be retrieved from the database.
   - **`testFindCourseId()`**: Verifies that the correct course ID is returned when a course is found by its name.
   - **`testAddStudent()`**: Tests adding a new student and checks that it can be retrieved using its ID.
   - **`testFindStudentById()`**: Ensures that a student can be found by their ID.
   - **`testEnrollStudent()`**: Tests enrolling a student in a course and ensures the student exists in the database afterward.
   - **`testAssignGrade()`**: Tests assigning a grade to a student in a course.

3. **Database Assertions**:
   - **`assertTrue()`**: Ensures that the course or student exists in the database after being added.
   - **`assertEquals()`**: Verifies that the data retrieved from the database matches the expected values.

### Running the Tests:
Ensure you have **JUnit 4.13.2** and **Hamcrest 1.3** (required for assertions) in your build dependencies (e.g., Maven or Gradle).

#### Maven Dependencies (in `pom.xml`):
```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.hamcrest</groupId>
    <artifactId>hamcrest-core</artifactId>
    <version>1.3</version>
    <scope>test</scope>
</dependency>
```

#### Gradle Dependencies (in `build.gradle`):
```gradle
testImplementation 'junit:junit:4.13.2'
testImplementation 'org.hamcrest:hamcrest-core:1.3'
```

These tests cover the core functionalities of the `Course`, `Student`, and `School` classes and ensure that the operations work as expected within the database context.









Below is the complete refactored code with the `SchoolCLI`, `SchoolService`, and `SchoolRepository` classes, along with the JUnit 4.13.2 test class using transactions for rolling back database changes.

### Complete Code

#### 1. `SchoolCLI` (Presentation Layer)

```java
import java.util.Scanner;

class SchoolCLI {
    private final SchoolService schoolService;

    public SchoolCLI(SchoolService schoolService) {
        this.schoolService = schoolService;
    }

    public void start() {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the School Management System");

        while (true) {
            System.out.print("> ");
            String input = scanner.nextLine();
            String[] command = input.split(" ");

            switch (command[0]) {
                case "add_course":
                    schoolService.addCourse(command[1]);
                    break;
                case "enroll_student":
                    schoolService.enrollStudent(Integer.parseInt(command[2]), command[1], command[3]);
                    break;
                case "assign_grade":
                    schoolService.assignGrade(Integer.parseInt(command[2]), command[1], Double.parseDouble(command[3]));
                    break;
                case "exit":
                    System.out.println("Exiting...");
                    return;
                default:
                    System.out.println("Unknown command");
            }
        }
    }
}
```

#### 2. `SchoolService` (Service Layer)

```java
class SchoolService {
    private final SchoolRepository schoolRepository;

    public SchoolService(SchoolRepository schoolRepository) {
        this.schoolRepository = schoolRepository;
    }

    public void addCourse(String courseName) {
        schoolRepository.addCourse(courseName);
    }

    public void enrollStudent(int studentId, String studentName, String courseName) {
        int courseId = schoolRepository.findCourseId(courseName);
        if (courseId == -1) {
            System.out.println("Error: Course '" + courseName + "' does not exist.");
            return;
        }

        Student student = schoolRepository.findStudentById(studentId);
        if (student == null) {
            schoolRepository.addStudent(new Student(studentId, studentName));
        }

        schoolRepository.enrollStudentInCourse(studentId, courseId);
    }

    public void assignGrade(int studentId, String courseName, double grade) {
        int courseId = schoolRepository.findCourseId(courseName);
        if (courseId == -1) {
            System.out.println("Error: Course '" + courseName + "' does not exist.");
            return;
        }

        Student student = schoolRepository.findStudentById(studentId);
        if (student == null) {
            System.out.println("Error: Student with ID '" + studentId + "' does not exist.");
            return;
        }

        schoolRepository.assignGrade(studentId, courseId, grade);
    }
}
```

#### 3. `SchoolRepository` (Repository Layer)

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

// Repository Layer
class SchoolRepository {
    private final Connection connection;

    public SchoolRepository(Connection connection) {
        this.connection = connection;
    }

    // Add course to the database
    public void addCourse(String courseName) {
        try {
            String query = "INSERT INTO Courses (course_name) VALUES (?)";
            try (PreparedStatement stmt = connection.prepareStatement(query)) {
                stmt.setString(1, courseName);
                stmt.executeUpdate();
                System.out.println("Course '" + courseName + "' added.");
            }
        } catch (SQLException e) {
            System.out.println("Error adding course: " + e.getMessage());
        }
    }

    // Find course ID by course name, returns -1 if not found
    public int findCourseId(String courseName) {
        try {
            String query = "SELECT course_id FROM Courses WHERE course_name = ?";
            try (PreparedStatement stmt = connection.prepareStatement(query)) {
                stmt.setString(1, courseName);
                try (ResultSet rs = stmt.executeQuery()) {
                    if (rs.next()) {
                        return rs.getInt("course_id");
                    }
                }
            }
        } catch (SQLException e) {
            System.out.println("Error finding course: " + e.getMessage());
        }
        return -1;
    }

    // Add student to the database
    public void addStudent(Student student) {
        try {
            String query = "INSERT INTO Students (student_id, student_name) VALUES (?, ?)";
            try (PreparedStatement stmt = connection.prepareStatement(query)) {
                stmt.setInt(1, student.getId());
                stmt.setString(2, student.getName());
                stmt.executeUpdate();
                System.out.println("Student '" + student.getName() + "' added.");
            }
        } catch (SQLException e) {
            System.out.println("Error adding student: " + e.getMessage());
        }
    }

    // Find student by ID, returns null if not found
    public Student findStudentById(int studentId) {
        try {
            String query = "SELECT student_id, student_name FROM Students WHERE student_id = ?";
            try (PreparedStatement stmt = connection.prepareStatement(query)) {
                stmt.setInt(1, studentId);
                try (ResultSet rs = stmt.executeQuery()) {
                    if (rs.next()) {
                        return new Student(rs.getInt("student_id"), rs.getString("student_name"));
                    }
                }
            }
        } catch (SQLException e) {
            System.out.println("Error finding student: " + e.getMessage());
        }
        return null;
    }

    // Enroll student in a course
    public void enrollStudentInCourse(int studentId, int courseId) {
        try {
            String query = "INSERT INTO Enrollments (course_id, student_id) VALUES (?, ?)";
            try (PreparedStatement stmt = connection.prepareStatement(query)) {
                stmt.setInt(1, courseId);
                stmt.setInt(2, studentId);
                stmt.executeUpdate();
                System.out.println("Student '" + studentId + "' enrolled in course '" + courseId + "'.");
            }
        } catch (SQLException e) {
            System.out.println("Error enrolling student: " + e.getMessage());
        }
    }

    // Assign grade to a student in a course
    public void assignGrade(int studentId, int courseId, double grade) {
        try {
            String query = "INSERT INTO Grades (course_id, student_id, grade) VALUES (?, ?, ?)";
            try (PreparedStatement stmt = connection.prepareStatement(query)) {
                stmt.setInt(1, courseId);
                stmt.setInt(2, studentId);
                stmt.setDouble(3, grade);
                stmt.executeUpdate();
                System.out.println("Grade '" + grade + "' assigned to student '" + studentId + "' in course '" + courseId + "'.");
            }
        } catch (SQLException e) {
            System.out.println("Error assigning grade: " + e.getMessage());
        }
    }

    // Check if a student is enrolled in a course
    public boolean isStudentEnrolledInCourse(int studentId, int courseId) {
        try {
            String query = "SELECT * FROM Enrollments WHERE student_id = ? AND course_id = ?";
            try (PreparedStatement stmt = connection.prepareStatement(query)) {
                stmt.setInt(1, studentId);
                stmt.setInt(2, courseId);
                try (ResultSet rs = stmt.executeQuery()) {
                    return rs.next(); // Return true if a result exists
                }
            }
        } catch (SQLException e) {
            System.out.println("Error checking enrollment: " + e.getMessage());
        }
        return false;
    }

    // Find grade for a student in a course
    public double findGradeForStudentInCourse(int studentId, int courseId) {
        try {
            String query = "SELECT grade FROM Grades WHERE student_id = ? AND course_id = ?";
            try (PreparedStatement stmt = connection.prepareStatement(query)) {
                stmt.setInt(1, studentId);
                stmt.setInt(2, courseId);
                try (ResultSet rs = stmt.executeQuery()) {
                    if (rs.next()) {
                        return rs.getDouble("grade");
                    }
                }
            }
        } catch (SQLException e) {
            System.out.println("Error finding grade: " + e.getMessage());
        }
        return -1.0; // Return -1 if grade not found
    }
}
```

#### 4. `Student` Class (Model)

```java
class Student {
    private int id;
    private String name;

    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }
}
```

#### 5. `SchoolServiceTest` (JUnit 4.13.2 Test Class)

```java
import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

import static org.junit.Assert.*;

public class SchoolServiceTest {
    private Connection connection;
    private SchoolRepository schoolRepository;
    private SchoolService schoolService;

    @Before
    public void setUp() throws SQLException {
        // Get a connection and start a transaction
        connection = DriverManager.getConnection("jdbc:mysql://localhost:3307/bootcamp_test", "root", "password123");
        connection.setAutoCommit(false); // Start a transaction
        schoolRepository = new SchoolRepository(connection); // Pass the connection to repository
        schoolService = new SchoolService(schoolRepository);
    }

    @After
    public void tearDown

() throws SQLException {
        // Rollback any changes made during the test
        if (connection != null) {
            connection.rollback(); // Rollback the transaction
            connection.close();    // Close the connection
        }
    }

    @Test
    public void testAddCourse() {
        // Test adding a course
        schoolService.addCourse("Mathematics");

        // Verify that the course has been added to the database
        int courseId = schoolRepository.findCourseId("Mathematics");
        assertTrue(courseId != -1); // Course should exist

        // Verify that the course ID is valid
        assertTrue(courseId > 0);
    }

    @Test
    public void testEnrollStudentInCourse() {
        // First, add the course
        schoolService.addCourse("Physics");

        // Enroll the student
        schoolService.enrollStudent(1, "John Doe", "Physics");

        // Verify the enrollment by checking if the student and course exist
        Student student = schoolRepository.findStudentById(1);
        assertNotNull(student); // Student should exist

        int courseId = schoolRepository.findCourseId("Physics");
        assertTrue(courseId != -1); // Course should exist

        // Verify enrollment
        boolean enrolled = schoolRepository.isStudentEnrolledInCourse(1, courseId);
        assertTrue(enrolled); // Student should be enrolled in the course
    }

    @Test
    public void testAssignGrade() {
        // Add a course and student
        schoolService.addCourse("Chemistry");
        schoolService.enrollStudent(2, "Jane Doe", "Chemistry");

        // Assign a grade to the student
        schoolService.assignGrade(2, "Chemistry", 85.0);

        // Verify the grade assignment
        double grade = schoolRepository.findGradeForStudentInCourse(2, schoolRepository.findCourseId("Chemistry"));
        assertEquals(85.0, grade, 0.01); // Check that the grade matches
    }
}
```

### Explanation:
- **JUnit 4.13.2** is used for testing.
- **Transactions** are handled by setting auto-commit to `false` and rolling back in the `@After` method to ensure the database state is reset after each test.
- **Database operations** are tested using actual JDBC queries.
- The tests verify the addition of courses, student enrollments, and grade assignments, ensuring correct functionality of the system. 

This approach ensures a clean and isolated testing environment by using transactions to rollback changes after every test.