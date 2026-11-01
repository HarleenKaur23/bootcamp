### JUnit 4 Basics Tutorial

JUnit is one of the most popular testing frameworks in Java. JUnit 4 provides annotations, assertions, and test runners to help developers test their code efficiently.

Here’s a step-by-step tutorial on JUnit 4 basics.

### 1. **Setting Up JUnit 4**
To start using JUnit 4, you need to add the JUnit 4 dependency to your project. If you're using Maven, include this in your `pom.xml` file:

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
```

Alternatively, download the JUnit 4 JAR file and add it to your classpath.

### 2. **Basic Annotations in JUnit 4**

JUnit 4 introduced annotations that simplify test writing. Here are the key annotations:

- `@Test`: Marks a method as a test method.
- `@Before`: Runs before each test method (used for setup).
- `@After`: Runs after each test method (used for cleanup).
- `@BeforeClass`: Runs once before any test methods in the class (used for class-level setup).
- `@AfterClass`: Runs once after all test methods in the class (used for class-level cleanup).
- `@Ignore`: Temporarily disables a test method.

### 3. **Writing Your First Test Case**

```java
import org.junit.Before;
import org.junit.Test;
import static org.junit.Assert.*;

public class CalculatorTest {

    private Calculator calculator;

    // This method will be called before every test
    @Before
    public void setUp() {
        calculator = new Calculator();  // Initialize the Calculator object
    }

    // Test method to check the addition functionality
    @Test
    public void testAdd() {
        int result = calculator.add(2, 3); //SUT
        assertEquals(5, result);  // Assert that the result is 5
        assertTrue(5==result);
    }

    // Test method to check division functionality
    @Test(expected = ArithmeticException.class)
    public void testDivideByZero() {
        calculator.divide(10, 0);  // This should throw ArithmeticException
    }
}
```

### 4. **JUnit Assertions**

JUnit provides a set of assertion methods to check if the test passes or fails. Some commonly used assertion methods are:

- `assertEquals(expected, actual)`: Verifies that two values are equal.
- `assertTrue(condition)`: Verifies that a condition is true.
- `assertFalse(condition)`: Verifies that a condition is false.
- `assertNotNull(object)`: Verifies that an object is not null.
- `assertNull(object)`: Verifies that an object is null.
- `assertSame(expected, actual)`: Verifies that two references point to the same object.
- `assertArrayEquals(expectedArray, actualArray)`: Verifies that two arrays are equal.

### 5. **Test Execution Order: `@Before`, `@Test`, and `@After`**

Here’s how the execution works:
1. **`@Before`**: Runs before each test.
2. **`@Test`**: Runs the test case.
3. **`@After`**: Runs after each test.

```java
import org.junit.After;
import org.junit.Before;
import org.junit.Test;

public class ExampleTest {

    @Before
    public void setUp() {
        System.out.println("Setting up the test...");
    }

    @Test
    public void testMethod1() {
        System.out.println("Running test method 1...");
    }

    @Test
    public void testMethod2() {
        System.out.println("Running test method 2...");
    }

    @After
    public void tearDown() {
        System.out.println("Cleaning up after the test...");
    }
}
```

**Output:**
```
Setting up the test...
Running test method 1...
Cleaning up after the test...
Setting up the test...
Running test method 2...
Cleaning up after the test...
```

### 6. **Testing Exceptions**

You can test whether a method throws an expected exception by adding the `expected` attribute to the `@Test` annotation.

```java
@Test(expected = NullPointerException.class)
public void testNullPointerException() {
    String str = null;
    str.length();  // This will throw NullPointerException
}

@Test(expected = CourseAlreadyAvailableException.class)
public void testNullPointerException() {
  school.addCourse("Math101");
  school.addCourse("Math101");
 }
```

### 7. **Ignoring Tests**

If you want to skip a test temporarily, use the `@Ignore` annotation:

```java
import org.junit.Ignore;
import org.junit.Test;

public class IgnoreTest {

    @Test
    public void testActive() {
        System.out.println("This test runs.");
    }

    @Ignore("Temporarily disabled test")
    @Test
    public void testIgnored() {
        System.out.println("This test is ignored.");
    }
}
```

### 8. **Parameterized Tests (Advanced)**

JUnit 4 supports parameterized tests where a test is run multiple times with different inputs.

```java
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;

import java.util.Arrays;
import java.util.Collection;

import static org.junit.Assert.assertEquals;

@RunWith(Parameterized.class)   //this is important - Junit specific Assertion
public class ParameterizedTest { //this name could be anything

    private int input1;
    private int input2;
    private int expected;

    public ParameterizedTest(int input1, int input2, int expected) {
        this.input1 = input1;
        this.input2 = input2;
        this.expected = expected;
    }

    @Parameterized.Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][]{
                {1, 2, 3},
                {2, 3, 5},
                {5, 5, 10}
        });
    }

    @Test
    public void testAddition() {
        Calculator calculator = new Calculator();
        assertEquals(expected, calculator.add(input1, input2));
    }
}
```

### 9. **JUnit 4 Test Suites**

You can group several test classes together in a suite using `@SuiteClasses`:

```java
import org.junit.runner.RunWith;
import org.junit.runners.Suite;

@RunWith(Suite.class)
@Suite.SuiteClasses({
    CalculatorTest.class,
    ExampleTest.class,
  SchoolUITest.class,
  SchoolBusinessTest.class,
  SchoolRepositoryTest.class
   
})
public class TestSuite {
    // This class remains empty. It's used only as a holder for the above annotations.
}
```

### 10. **Running JUnit Tests**

You can run JUnit tests in several ways:
- **IDE**: Most IDEs like Eclipse, IntelliJ IDEA, and NetBeans have built-in support for running JUnit tests.
- **Command Line**: Using Maven or Gradle.
  - Maven: `mvn test` 
  - Gradle: `gradle test`

### 11. **Example Calculator Class for Testing**

For testing purposes, here's an example `Calculator` class used in the test cases above:

```java
public class Calculator {

    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }

    public int multiply(int a, int b) {
        return a * b;
    }

    public int divide(int a, int b) {
        if (b == 0) {
            throw new ArithmeticException("Cannot divide by zero.");
        }
        return a / b;
    }
}
```

### Summary

- **JUnit 4 Basics**: Use annotations like `@Test`, `@Before`, and `@After` to define test cases and lifecycle methods.
- **Assertions**: Use JUnit assertions like `assertEquals()`, `assertTrue()`, and `assertNull()` to verify the test output.
- **Testing Exceptions**: Use `expected` in `@Test` to verify exception throwing.
- **Ignore Tests**: Use `@Ignore` to skip tests temporarily.
- **Parameterized Tests**: Run tests with multiple input values.
- **Test Suites**: Group multiple test classes into one suite for batch testing.



Here is the updated JUnit 4 test class that uses different features such as `expected` for exceptions, `@Before` for setup, and `@Parameterized` for parameterized tests.

### **JUnit 4 Tests for `Calculator` Class**

#### 1. **Basic Tests with `expected` Attribute for Exception Handling**

```java
import org.junit.Before;
import org.junit.Test;
import static org.junit.Assert.*;

public class CalculatorTest {

    private Calculator calculator;

    // Setup method to initialize the Calculator instance before each test
    @Before
    public void setUp() {
        calculator = new Calculator();
    }

    // Test for the addition method
    @Test
    public void testAdd() {
        assertEquals(5, calculator.add(2, 3));
        assertEquals(-1, calculator.add(-2, 1));
        assertEquals(0, calculator.add(2, -2));
    }

    // Test for the division method
    @Test
    public void testDivide() {
        assertEquals(2, calculator.divide(10, 5));
        assertEquals(3, calculator.divide(9, 3));
    }

    // Test for division by zero, which should throw an ArithmeticException
    @Test(expected = ArithmeticException.class)
    public void testDivideByZero() {
        calculator.divide(10, 0); // This should throw ArithmeticException
    }

    // Test for subtraction
    @Test
    public void testSubtract() {
        assertEquals(0, calculator.subtract(2, 2));
        assertEquals(-1, calculator.subtract(2, 3));
    }

    // Test for multiplication
    @Test
    public void testMultiply() {
        assertEquals(10, calculator.multiply(2, 5));
        assertEquals(0, calculator.multiply(0, 5));
        assertEquals(-15, calculator.multiply(-3, 5));
    }
}
```

#### 2. **Parameterized Tests for `add()` Method**

JUnit 4 supports parameterized tests, which allow you to run the same test with different sets of inputs and expected results. Here’s how you can test the `add()` method using parameterized tests.

```java
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import java.util.Arrays;
import java.util.Collection;
import static org.junit.Assert.assertEquals;

@RunWith(Parameterized.class)
public class CalculatorParameterizedTest {

    private int input1;
    private int input2;
    private int expected;

    // Constructor to initialize the test data
    public CalculatorParameterizedTest(int input1, int input2, int expected) {
        this.input1 = input1;
        this.input2 = input2;
        this.expected = expected;
    }

    // Provide test data as a collection of parameters
    @Parameterized.Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][] {
            { 1, 2, 3 },
            { 2, 3, 5 },
            { 5, 5, 10 },
            { -2, 2, 0 },
            { -5, -3, -8 }
        });
    }

    // Test method to check addition
    @Test
    public void testAdd() {
        Calculator calculator = new Calculator();
        assertEquals(expected, calculator.add(input1, input2));
    }
}
```

### **Using Parameterized Tests for Subtraction**

You can also apply parameterized tests to check the subtraction method in a similar way.

```java
@RunWith(Parameterized.class)
public class CalculatorSubtractionParameterizedTest {

    private int input1;
    private int input2;
    private int expected;

    // Constructor to initialize test data
    public CalculatorSubtractionParameterizedTest(int input1, int input2, int expected) {
        this.input1 = input1;
        this.input2 = input2;
        this.expected = expected;
    }

    // Provide test data as a collection of parameters
    @Parameterized.Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][] {
            { 5, 3, 2 },
            { 10, 5, 5 },
            { 0, 0, 0 },
            { -5, -3, -2 }
        });
    }

    // Test method to check subtraction
    @Test
    public void testSubtract() {
        Calculator calculator = new Calculator();
        assertEquals(expected, calculator.subtract(input1, input2));
    }
}
```

### **Testing `divide()` Method with Exception Handling**

```java
import org.junit.Before;
import org.junit.Test;
import static org.junit.Assert.*;

public class CalculatorDivisionTest {

    private Calculator calculator;

    // Setup method to initialize the Calculator instance before each test
    @Before
    public void setUp() {
        calculator = new Calculator();
    }

    // Test normal division
    @Test
    public void testDivide() {
        assertEquals(2, calculator.divide(10, 5));
        assertEquals(3, calculator.divide(9, 3));
    }

    // Test division by zero, which should throw an ArithmeticException
    @Test(expected = ArithmeticException.class)
    public void testDivideByZero() {
        calculator.divide(10, 0); // This should throw ArithmeticException
    }
}
```

### **JUnit Test Suite**

You can bundle all these test classes together into a suite using the following code:

```java
import org.junit.runner.RunWith;
import org.junit.runners.Suite;

@RunWith(Suite.class)
@Suite.SuiteClasses({
        CalculatorTest.class,
        CalculatorParameterizedTest.class,
        CalculatorSubtractionParameterizedTest.class,
        CalculatorDivisionTest.class
})
public class CalculatorTestSuite {
    // This class remains empty, it's used only to hold the above annotations.
}
```

### **Summary of the Tests**

1. **Basic Tests**: For each method in the `Calculator` class (like `add()`, `subtract()`, `multiply()`, `divide()`), basic unit tests check the functionality, and exception handling is verified using the `expected` attribute in the `@Test` annotation.
   
2. **Parameterized Tests**: Test the `add()` and `subtract()` methods with multiple sets of inputs and expected outputs, ensuring the functionality works for different cases using `@Parameterized`.

3. **Exception Handling**: Tests like `testDivideByZero()` confirm that dividing by zero correctly throws an `ArithmeticException`.

4. **Test Suite**: The test suite `CalculatorTestSuite` allows you to group all your test classes together and run them as one batch.

### Running the Tests
Run these tests in your IDE (such as IntelliJ IDEA or Eclipse) or use Maven (`mvn test`) to execute them from the command line.

Let me know if you need further assistance or clarifications!