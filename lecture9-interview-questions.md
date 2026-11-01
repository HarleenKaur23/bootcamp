### Frequently Asked Interview Questions

#### 1. **Evaluate Collections**
- **Data Access Pattern**: LIFO vs FIFO or Key-Value Mapping
- **Insertion Order**: Maintains insertion order or not
- **Sorting**: Automatic sorting available
- **Allows Null Values**: Supports null values or not
- **Duplicate Values**: Allows duplicates
- **Thread Safety**: Thread-safe or not
- **Backward/Forward Access**: Ability to access data in both directions
- **Fail-Safe vs Fail-Fast**: Which mechanism is supported

---

#### 2. **Threading**
- **Thread-Safe Code**: A code block that can be executed by multiple threads and guarantees consistent results.
  
  **To Achieve Thread Safety**:
  - Avoid shared mutable state.
  - If shared mutable state is necessary:
    - Store it in the database and leverage row-level synchronization provided by the DB.
    - Use **atomic variables** if they serve the purpose.
    - Use the `synchronized` keyword at the right granularity (method or class level) if database synchronization isn’t feasible. 
      - [Synchronization](https://www.javamex.com/tutorials/synchronization_concurrency_synchronized1.shtml#)
  - **Volatile Keyword**: 
    - [Volatile in Java](https://www.javamex.com/tutorials/synchronization_volatile.shtml)
  - **Thread Lifecycle**:
    - [Java Thread Lifecycle](https://www.baeldung.com/java-thread-lifecycle)
  - **Avoiding Deadlocks**:
    - [How to Avoid Deadlocks](https://javarevisited.blogspot.com/2018/08/how-to-avoid-deadlock-in-java-threads.html)
    - [StackOverflow: Prevent Deadlocks](https://stackoverflow.com/questions/16780937/tips-to-prevent-deadlocks-in-java)
  - **Volatile vs Atomic Variables**:
    - [Volatile vs Atomic](https://www.javacodegeeks.com/2018/03/volatile-java-works-example-volatile-keyword-java.html)
    - [StackOverflow: Volatile vs Atomic](https://stackoverflow.com/questions/19744508/volatile-vs-atomic)

---

#### 3. **Other Key Concepts**
- **Marker Interfaces**: `Serializable`, `Cloneable`
- **Fail-Fast vs Fail-Safe vs Thread-Safe**
- **Volatile vs Transient**
- **Semaphore** (Threading)
- **Overriding vs Overloading**
- **Comparator vs Comparable**:
  - [Comparator vs Comparable](https://www.edureka.co/blog/comparable-in-java/)
- **Interfaces**: `Serializable`, `Cloneable`, `Iterable`, `Iterator`
- **Private Constructors**
- **Finally, Finalize, Final**
- **Garbage Collection**:
  - [Java Memory Management](https://www.baeldung.com/java-memory-management-interview-questions)
- **Runnable vs Callable**
- **Statement vs PreparedStatement vs CallableStatement**
- **Equals vs HashCode**
- **Collection Selection**: Understanding which collection to use
- **Java Pass by Value vs Reference**
- **Polymorphism**: Static vs Dynamic
- **Design Patterns**
- **Threading, Generics, Exception Handling, IO, Java 8 Streams & Lambdas**

---

#### 4. **Spring vs Spring Boot**
- [Spring vs Spring Boot](https://www.baeldung.com/spring-vs-spring-boot)

---

1. OOP fundamentals (Abstraction, Polymorphism, Inheritance, Encapsulation)
2. Method Overriding vs Method Overloading
3. Compile-time vs Run-time Polymorphism
4. SOLID principles
5. Java Generics - What is type erasure? What's the point of generics if type erasure is done regardless by the compiler?
6. Exception Handling (Can you catch a runtime exception or an error? What will happen when you do, and should you catch them?)
7. Features of Java 8 (Lambda, Streams, Optionals, Date-Time APIs)
8. Given a list of employees, provide one string with names of all employees, delimited by commas.
9. How to find min, max, and average in a stream of objects.
10. What is the point of using `Optional`?
11. What are functional interfaces? (Examples of functional interfaces)
12. What are marker interfaces? (Examples of marker interfaces)
13. What is serialization and how to implement serialization?
14. Difference between `Comparable` and `Comparator`
15. Given a list of integers, how would you find the max value using streams?
16. What is a default method, and where do we use it?
17. Collections - What collections have you used and for what purposes?
18. The role of `hashCode` and `equals` in `HashMap`
19. In Java 8, `HashMap` implementation changed, why? (Hint: it used a different data structure for handling collisions)
20. What is time complexity? (Time complexity for removing an object from an `ArrayList`, for removing a value from an array, for accessing elements in a map)
21. What is Spring IOC, Dependency Injection, BeanFactory, ApplicationContext?
22. Common annotations used for Spring and Spring Boot
23. Difference between JPA, Spring Data, and Spring Data JPA
24. Benefits of using Spring Boot (Hint: there are 6 main ones)
25. Difference between `@Component`, `@Service`, `@Repository`, and `@Controller`
26. Difference between `@Bean` and `@Component` annotations
27. What is slice-based testing, Spring JPA test, and MVC test?
28. What is a transaction?
29. Difference between isolation and propagation in a transaction?
30. What is AOP (Aspect-Oriented Programming)? Where do we use it?
31. How do you handle profile-based applications (What is a profile and how to run in different environments)?
32. What is the role of polymorphism?
33. Difference between Monolithic and Microservices architectures
34. What is distributed logging and tracing? How is it done using Spring Cloud Sleuth?
35. What are the reasons to use Docker containers and Kubernetes?
36. Kubernetes commands for deployment and scaling
37. How do you start with a new project? Begin with entity modeling, checking relationships (Domain-Driven Design). Then create a Swagger contract (Contract-first approach).
38. Write a REST controller with CRUD operations for an Employee entity starting from [http://start.spring.io](http://start.spring.io), call it from Postman, and change the input/output from JSON to XML.  
    - Hook it up to the H2 Database, completing the service and repository layer  
    - Hook it up to MongoDB
39. Difference between PUT, PATCH, and POST (Idempotent vs not, takes ID vs not)
40. Difference between Contract-First and Contract-Last approaches

---

**DB Questions:**
1. Find the list of employees with the same salary (duplicate values) using Java Stream and SQL.
2. Find the max depth of a tree (Hint: use recursion).
3. Write a method to delete a node from a linked list.

---

1. APM (Application Performance Management) - Dynatrace
2. API Gateway setup
3. JIRA setup
4. Agile Scrum practices (Standup, Retrospective meetings, Sprint planning, and backlog refinement meetings)

---

1. Share your experience, recent projects, technical skills.
2. How did you secure your API?
3. What OAuth flow did you use?  
   What are the other OAuth flows?  
   Which is more secure?  
   When do you use one over another - Resource Owner, Authorization Code?
4. What are the other ways to secure an API?
5. Basic Authentication
6. What is two-way SSL?  
   Can you explain more about the handshake process?
7. ArrayList vs LinkedList
8. Transient, Volatile
9. Heap Dump - How do you clear heap memory?  
   More about the garbage collector.
10. How do you clear off stack memory?
11. Spring Boot Actuator - More about the health endpoint  
    How do you secure it?  
    EnableWebSecurity - How can you implement security without using Spring Security?
12. JWT - How do you validate a JWT token?
13. Why Kafka?  
    What is ISR in Kafka?  
    What happens if the leader goes down?  
    Why Consumer Offset? Is it maintained at partition or topic level?  
    How to make Kafka work like a queue?
14. How do you handle exceptions in Spring Boot?  
    How to handle exceptions only from a particular controller?



Here’s a neatly formatted version of your list:

- **Data Structure Selection Criteria**
- **Time Complexity of Normal Operations using Lists and Sets**  
  - *Delete* and *Insert*
- **Data Structure Selection for Duplicate Avoidance and Natural Sorted Order**  
  - Considerations when maintaining *insertion order* or *natural sorted order*.
- **Preemptive Striking**  
  - Using more elaborate keywords to describe the concept.
- **Spring vs Spring Boot**  
  - Key differences between the two frameworks.
- **Thread Safety**  
  - Definition of thread safety.
  - Techniques for achieving thread safety.

### Notes for Test:

**Create a RestAPI with CRUD operations against an H2 database:**

1. Implement all request methods:
   - `POST`
   - `PUT`
   - `PATCH`
   - `DELETE`
   - `GET`

**Create additional endpoints:**

- Return a list of employees based on salary (use streams):
  - Employees should be joined with a delimiter (`:`).
  
- Return a list of employees based on postal code (use streams).

- Return the highest salary employee or employee list.



