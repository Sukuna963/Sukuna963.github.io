---
layout: post
title: "Java 301 - Advanced Concepts"
author: "Leonardo Marques"
categories: course
tags: [software]
image: advanced-java/Advanced-java.png
---

|
[Course](https://codingnomads.com/course/java-programming-301)
|
[Code](https://github.com/Sukuna963/Java_301-Advanced_Concepts)
|

# Exception Handling

### Introduction to Java Exception Handling

* An **Exception** in Java is a class that handles exceptions in your program

* **Exception** handling is the process of predicting and preparing for exceptions in your program

* Uncaught exceptions are errors that happen in a program and haven't been predicted by the developer

**Five Keywords for Exception Handling**
* try
* catch
* throw
* throws
* finally

### Java Exception Hierarchy
* Every **Exception** class is a subclass of the **Throwable** class

* **Error** and **Exception** are the two subclasses of **Throwable**

* **Error** exceptions are typically caused by the machine

* **Exception** exceptions are typically caused by program activity

* Many standard exceptions come from the **RuntimeException** class

* Java comes with many built-in exceptions in the **java.lang** package

### Try Catch
* The **try-catch** block is the foundation of **Exception** handling in Java

* You can't have a **try** without a **catch** and vice versa

* The **try** section will attempt to run a section of code

* The **catch** section will activate if an applicable **Exception** is generated

* You can add multiple **catch** blocks to each **try** block

* The **try-catch** block can be nested within itself

```java
try {
    // Block of code to monitor for errors
} catch (Exception exc) {
    // Handle for Exception exc
}
```
### Try Catch Finally
* The **finally** block in Java comes after the last **catch** in a **try-catch** block

* The code inside a **finally** block will always be executed, regardless of what happens inside the **try-catch** blocks

* The **finally** block is a great place to force the closing of a connection that was opened inside of a **try** block

```java
try {
    // Code that needs to be monitored for errors
} catch (Exception exc) {
    // Handler for Exception object exc
} finally {
    // Code to execute no matter the result of try/catch
}
```

### Method "Throws" Exception
* The **throws** keyword is used in Java to indicate that a method may "throw" a generated exception back to the calling method

* The calling method must therefore be ready to handle any exception it receives in a graceful manner

* The **throws** keyword is placed inside the method signature

```java
public your_return_type your_method() throws YourException{
    // Your Code
}
```

### Java Throwable Exception Methods

| Method | Description |
|---|---|
| Throwable fillInStackTrace() | Returns a Throwable object that contains a completed stack trace |
| String getLocalizedMessage() | Returns a localized description of the exception |
| String getMessage() | Returns a description of the exception |
| String getCause() | Returns the cause of the exception |
| void printStackTrace() | Displays the stack trace |
| String toString() | Returns a String object containing a description of the exception |

# Input / Output (I/O)

### Read & Write Files with Java I/O Streams
* A stream is a connection between your program and a file

* A stream is also often referred to as input-output or simply I/O (or IO)

* Byte streams and **Character** streams are the two primary I/O streams

* There are many subclasses of **IOException** since exceptions are common when working with streams

### Byte Stream vs Character Stream
* Byte streams have a read-length of 8 bits at a time

* Byte streams are for reading **byte** by **byte**

* Byte streams have the word **stream** in the class name

* **Character** streams have a read-length of 16 bits at a time

* **Character** streams are for reading character by character

* **Character** streams are required to ensure that each character in the human language is properly read by the machine

* **Character** streams have either the word **reader** or **writer** in the class name

* If a file contains data in the form of a human language, you probably want to use a **Character** stream

### Java Input Streams
* The **Inputstream** class is the parent class for all inputs in I/O

* The **Outputstream** class is the parent class for all outputs in I/O

* Both classes are the foundation of **Byte** streams

* **Byte** streams ready one byte at a time (1 byte = 8 bits)

### Java Buffered Input Streams
* Buffering creates a block of storage between the reader and the data source

* Buffering stores parts of the data that is being requested

* Buffering increases the speed and efficiency of data transfer

* Buffering in Java can be done by wrapping a class in a buffering class

* Wrapping is the process of adding a class around another to add functionality

* The **BufferedInputStream** class is an example of buffering a Byte stream

``Benefits of Buffering``
1. Reducing I/O operations
2. Fluid and smooth data transfer
3. Reducing delays caused by the data source

### Reading & Writing Files with Character Streams
* Files are often read using **FileReader**

* All Character stream I/O classes are subclasses of **Reader** and **Writer**

* Stream classes automatically translate between the internal **char** format to the desired local character set

* Using the **BufferedReader** and **BufferedWriter** classes is helpful for reading/writing many characters at a time to improve efficiency

### Try-With-Resources
* When using any of Java Byte Streams or Character Streams, use the **try-with-resources**

* Using the **try-with-resources** cleans up your code base and eliminates unnecessary **finally** blocks with **try-catch** statements within

* The **try-with-resources** can manage multiple connections

* Moving forward, **try-with-resources** is the recommended way of managing I/O connections

# Multithreading

### What is Java Multithreading?
* A **Thread** is a class in Java that represents a process of execution

* Java is written to include multithreading

* Multithreading is the process of executing multiple threads in parallel

* Multithreading improves processing efficiency

``How to Create a Thread?``
1. Implement the Runnable Interface
2. Extend the Thread class

### Implement Runnable Interface
* Java threads can be created by implementing the **Runnable** interface

* Any class can use implements Runnable`

* **run()** is an abstract method inside of **Runnable** and must be overridden

* Implementing the **Runnable** interface is typically the preferred way to create threads

### Extend the Java Thread Class
* The Java Thread class is extended using the **extends** keyword

* This is not the preferred method for creating threads in Java unless you need access to the Thread class

* The process of extending the **Thread** class is very similar to implementing the **Runnable** class

* The **run()** method must be implemented when extending the **Thread** class

### Java Thread Priority
* Every **Thread** automatically receives a priority in Java

* Priorities range from 1 (low) to 10 (high)

* The JVM will preference higher priority threads if computational power is low

* Java comes with three static final variables for setting priorities

    * **Thread.MIN_PRIORITY** equals 1
    * **Thread.NORM_PRIORITY** equals 5
    * **Thread.MAX_PRIORITY** equals 10
* The **setPriority()** method is used to manually set the priority

### Java Thread Join
* Threads can be joined together in Java, putting them in sequential order

* A joined **Thread** will only execute once its previous **Thread** has been completed

* Threads are joined using the **join()** method

``Three Types of the Join Method``
1. join()
2. join(long millis)
3. join(long millis, int nanos)

### Synchronizing Java Threads
* The **synchronized** keyword ensures order in multithreading scenarios.

* Synchronization helps prevent race conditions when multiple threads access shared resources concurrently.

* Synchronizing methods ensures only one thread can execute the synchronized method at a time.

* Synchronized blocks provide more control over critical sections within methods.

* Synchronizing static methods uses the class as a lock.

* Synchronizing objects synchronizes based on specific objects for fine-grained control.

* Ensure well-structured synchronized blocks to avoid deadlocks.

### Threads: wait() and notify()
* **wait()** and **notify()** facilitate inter-thread communication and synchronization.

* **wait()** is used to make a thread wait until notified.

* **notify()** is used to wake up a waiting thread.

* Always use **wait()** inside a loop to handle spurious wake-ups.

* **wait()** and **notify()** must be called from a synchronized context.

### Thread Deadlock
* A deadlock happens when at least two threads are waiting on each other
* Resolving deadlocks can be done by looking at the logs, using debug mode, and dumping the JVM state

``Program Components Affected by Deadlocks``
* Resources
* Performance
* Data loss
* Troubleshooting

``Preventing Deadlocks``
* Avoid manual multithread orchestration
* Keep each thread's code independent and encapsulated
* Apply timeouts to threads
* Use optimistic locking instead of synchronization

### Thread Livelock
* A livelock is very similar to a deadlock

* A livelock enters into an infinite loop of execution instead of having its execution blocked as it is in a deadlock

* The majority of preventions and debugging techniques for livelocks are the same as for deadlocks

* Livelocks are harder to identify than deadlocks

* Debugging a livelock can be done by looking at the logs and dumping the system state

### Thread Race Condition
* A race condition is when two threads change the value of a resource at different times
* Race conditions can result in data loss
* Race conditions are hard to detect, debug, and prevent
* Race conditions are often detected after receiving several tickets with complaints from the users

``Steps to Debug``
* Add debugging logs
* Apply attention while coding to resources affected by data corruption
* Add sleep delays to replicate the problem

``Steps to Prevent``
* Make thread code independent and encapsulated
* Make shareable resources read-only
* Try optimistic locking

# Generics
* Generics is a functionality in Java that allows for flexible type declaration

* Class definitions of generics type support abstraction

* Class definitions of generics don't require type information

* You indicate the data type of a generic class when you instantiate an object of a generic class

* An **ArrayList** is an example of generics in Java - for instance **ArrayList<String> words = new ArrayList();**

* Type erasure is when generic type parameters are replaced at compile time. For instance, all the method parameter types and return types in the ArrayList class

* Type inference is when the instantiating constructor can infer the type in its declaration. For instance, **ArrayList<String> words = new ArrayList();** instead of ``ArrayList words = new ArrayList ();``

### Java Generics and Primitive Types
* Generics work only with object data types

* You cannot use primitive data types with generics

* **int** is a primitive data type, and **Integer** is its wrapper

* Primitive wrapper classes offer additional functionality

* You can explicitly and implicitly convert from the wrapper type to the primitive type

### Generic Java Method
* A generic method is a method that has generic parameter types and/or generic return types

* Generic methods are used when only itself and not the entire class need the generic type

* The generic parameter must be defined before the return type as well as in the parameter list

### Generics with Bounded Types
* Objects with generic types can limit the possible chosen types

* A bounded type parameter is applied using the **extends** or **implements** keywords

* Bounded type parameters can contain single or multiple bounds

* Multiple bounds are separated using the **&** character

```java
public <Your_TYpe_Parameter extends Your_Bound> Type Method_Name() {...}
```

# Enumerations
* Enumerations are sets of related items. For example, "North", "South", "East", and "West".

* An enumeration is also referred to as an enum

* An enum is a specific type in Java - similar to a class

* Enums can be set with values and contain methods

```java
public enum Your_Enum {
    YOUR_EXAMPLE_VALUE_1,
    YOUR_EXAMPLE_VALUE_2,
    YOUR_EXAMPLE_VALUE_3;
}
```

# Lambda Expressions & Methods References

### Anonymous Class
* An anonymous class is created and initiated at the same time

* An inner class is a class created inside of another

* Anonymous classes are very often anonymous inner classes

* An anonymous class can reduce code compared to creating an interface, creating a class that implements that interface, and then creating another class that uses the class that implements the interface

### Functional Interface
* A functional interface is just a normal **interface** in Java. But, a functional interface can only have one abstract method

* The **@FunctionalInterface** annotation indicates that the following is a functional interface

* There are several built-in functional interfaces in Java's **java.util.function** package

* **Predicate**, **Function**, and **BinaryOperator** are functional interface examples built into the **java.util.function** package

### Lambda Expressions
* A lambda expression is an anonymous function

* Lambda expressions can be created without belonging to a class

* Lambdas were introduced in Java 8

* The **->** operator separates a lambda's parameters from the method body

* Lambdas can be used inside of **forEach()** method

``Provided Lambda Examples``
* Set a Lambda to a Variable

* Lambda Expression with No Parameter

* Passing a Lambda as a Method Parameter

* List Processing with Lambdas

```java
your_variable = (yout_type your_parameter -> your_method_body)
```

### Method Reference
* A method reference is used to reference a method without executing it

* The **::** operator is used to separate the object and the method name

* A method reference can be used when a lambda expression only calls one existing method

``Four Types of Method References``
* A method reference to a static method

* A method reference to an instance method of an object of a particular type

* A method reference to an instance method of an existing object

* A method reference to a constructor

``Static Method``
* Syntax: **Class::staticMethod**

* Arguments are automatically passed through the reference

``Instance Method with a Particular Object``
* Syntax: **Class::instanceMethod**

* Arguments are automatically passed through the reference

``Instance Method with an Arbitrary Object and Particular Type``
* Syntax: **obj::instanceMethod**

* Arguments are automatically passed through the reference

``Static Method``
* Syntax: **Class::new**

* Arguments are not automatically passed through the reference

* The Function or BiFunction classes are used to pass through arguments

* The apply() method is used to pass through the argument to the constructor

### Stream API
* The **stream** API helps to iterate over a **Collection**

* Streams reduce the length of your code and increase efficiency

* Streams are compatible with functional interfaces and lambda expressions

* Streams can contain terminal and non-terminal operations

* Streams must contain one and only one terminal operation

* Streams can contain zero or more non-terminal operations

``Steps to Create Java Streams``
* Obtain a stream

* Call zero or more non-terminal operations on the stream

* Call at least one terminal operation on the stream

``Commonly Used Non-Terminal Operations``
* **map()**

* **filter()**

* **sorted()**

* **distinct()**

* **limit()**

* **skip()**

``Commonly Used Terminal Operations``
* **forEach()**

* **toArray()**

* **sum()**

* **count()**

* **min()/max()**

* **collect()**

* **anyMatch()/allMatch()**

# Java Database Connectivity
* JDBC stands for Java Database Connectivity

* JDBC allows your application to efficiently connect to multiple databases

* JDBC leverages separate drivers for each database

* The JDBC lifecycle involves establishing a connection to a database, creating and executing 
SQL statements, processing results, and finally, closing the connection to release resources.

### MySQL Connector Java
* The MySQL Connector connects your Java application to MySQL

* The MySQL JDBC driver is called MySQL Connector/J

* The classpath is a system variable that points Java to your project's dependencies

* Adding dependencies to your classpath can be done manually or automatically

* Dependency management and build tools like Maven and Gradle will automatically add dependencies to your classpath.

### Connection
* Many Java applications use a database connection and JDBC API

* These applications have a six-stage connection process

* The JDBC lifecycle involves establishing a connection to a database, creating and executing SQL statements, processing results, and finally, closing the connection to release resources.

``JDBC Life Cycle``
* Load the JDBC driver

* Open a database connection

* Create a **Statement** / **PreparedStatement** / **CallableStatement**

* Execute SQL statements

* Retrieve and potentially process the results of any SQL query

* Close database connection

### Connection Queries
* There are three major JDBC query types

1. Statements are used for general-purpose access to the database
2. Prepared statements are used for repeated SQL queries
3. Callable statements for accessing a database's stored procedure

* Examples of INSERT, UPDATE, SELECT, and DELETE are provided for statements and prepared statements

### ResultSet
* The ResultSet is an interface in Java for iterating through table data

* The next() is used to move the ResultSet cursor to the next row

* The default ResultSet cannot be used to update data

* The ResultSetMetaData stores the metadata of the ResultSet

* Both the ResultSet and the ResultSetMetaData come with many built-in methods to access the data

### ResultSet into a Java Object
* Java objects allow query resultsets to be easily incorporated into an application

* Mapping a **ResultSet** to a Java object requires a class that mirrors the desired table in the database

* Often a **ResultSet** is mapped to an **ArrayList** of these objects

* Mapping to Java objects can be done with simple and complex SQL queries

### Java Hibernate ORM
* Hibernate and Java Persistence API (JPA) are two commonly used ORMs

* An ORM is an Object-Relational Mapping framework

* ORMs facilitate integrating OOP Java applications with relational tables

* The term "Object-Relational Impedance Mismatch" is used to describe the inherent challenges of integrating OOP applications with relational databases.

``What are the Five Object-Relational Impedance Mismatch``
* Granularity

* Subtypes (inheritance)

* Identity

* Associations

* Data navigation