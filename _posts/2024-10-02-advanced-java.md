---
layout: post
title: "Java 301 - Advanced Concepts"
author: "Leonardo Marques"
categories: java
tags: [java, cs, programming-language, dsa]
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

    #### Benefits of Buffering
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

    #### How to Create a Thread?
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

    #### Three Types of the Join Method
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

    #### Program Components Affected by Deadlocks
    * Resources
    * Performance
    * Data loss
    * Troubleshooting

    #### Preventing Deadlocks
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

    #### Steps to Debug
    * Add debugging logs
    * Apply attention while coding to resources affected by data corruption
    * Add sleep delays to replicate the problem

    #### Steps to Prevent
    * Make thread code independent and encapsulated
    * Make shareable resources read-only
    * Try optimistic locking