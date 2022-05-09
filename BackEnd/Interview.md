Interview :  

#### ** What are the features of Java Programming Language :

1- **Simple** : Java syntax easier to learn

2- **Object**–**Oriented** :  managing the code with the help of objects. Java is a pure object-oriented language except for the primitive variables.  Java doesn’t support multiple inheritance.

3- **Platform Independent** : doesn’t depend upon the operating system to execute the code

4- **Secured:** Java doesn’t use any pointers it has its own  mechanism of handling memory management and with perfect authorization  process then only it gives access to the data to the program. Also, it  uses the concept of Byte Code and Exception handling which makes it more secured. 

5-**Robust:** The concepts like Automatic garbage collection, Exception handling, etc. make it more robust because it uses strong memory management mechanism.



*********************

#### **What is the importance of the main() method in Java?

- main() method in java is the entry point for any java program

  With the main method being public and static it helps java to access it without initializing the class. The value which is passed in the input parameter is an array of String by which runtime arguments are passed

*******************

#### 3) What is the difference between path and classpath variables?

Answer: The path is an environment variable which is used by operating systems to locate the executables. That’s the reason why when we install java for the first time or want an executable to be found by OS, we need to add the directory location in the Path variable.

Classpath is very specific to Java and used for locating class files by java executables. It can be a directory, ZIP files JAR files, etc. when we provide classpath location while running java application.

****************************

#### ** Is Java Pass By or Pass By Reference?

 But according to the Java Spec stated that everything in Java is Pass by Value. 

 when we pass a reference of complex types as any method parameters then the memory address is copied to a new reference variable in the exact same manner.

*****************

#### 5) What is the final Keyword in Java?

Answer: Final keyword is used with the class to make sure that any other class can’t extend it. For example String class is final and we can‘t extend it. Final keyword is also used with different methods so that it can’t be overridden by any child classes.

Variable is also made final so it is only assigned once. Java interfaces variable is also by default final and static.

**************************

####  What are the access modifiers in Java?

Answer: Access Modifiers are the keywords which are used for set accessibility to classes, methods, and other members. In Java, these are the four access modifiers:

**Public:** The classes, methods, variables, and other members who are defined as public, can be accessed by any class or method.

**Protected:** As it sounds, it has special characteristics. Classes or methods that are defined as protected can be accessed by the class of the same package,st or by the sub-class of the parent class, or within the same class.

**Default:** Default is accessible within the package only. All the classes, methods, and variables are of default when the public, protected, or private are not used.

**Private:** Classes, methods, and variables which are defined as private can be accessed within the class only.



*********************

#### What is a static import?

Answer: If we have to use any static variable or method from other class, usually we import the class and then import the method/variable with the class name.

import java.lang.Math;

//inside class

double test = Math.PI * 8;

We can do the same thing by importing the static method or variable then by only we can use it in the same class it belongs to.

import java.lang.Math.PI;



*****************

#### What is Enum in Java?

Answer: Enum was introduced in with Java 1.5 version as a new type whose field consists of fixed sets of constants. Enum constants are final

*******************

#### What is Composition in Java?

Answer: The composition is the design technique used in java to implement a has-a relationship in classes.

*****************

#### What is the Java Reflection API?

Answer: Java Reflection API provides the ability to inspect and modify the behavior of any application during runtime. 

*****************************

####  What is marker interface:

The marker interface in java is a design pattern used to provide run-time information about the objects . Serializable interface is a good example of marker interface

******

#### ) What is the difference between the user thread and daemon thread?

Answer: When a thread is created in a java program, it is known as user thread. A daemon thread is a thread which runs on background and doesn’t prevent JVM from terminating. When there is no user thread running then JVM shutdowns the program and quits. A child thread created from daemon thread is known as a daemon thread.

***********

#### What is CountDownLatch in Java?

Answer: CountDownLatch in Java is synchronizer which allows one Thread to wait for one or more Threads before start processing

**********

#### What is the volatile keyword in Java?

Answer: Volatile keyword in Java is used with variables and all the threads read its value directly from the memory location and don’t cache it. Volatile keyword makes sure that the read value is exactly the same as in the memory location.

**********

####  What is OutOfMemoryError in Java?

Answer: OutOfMemoryError in Java is a subclass of java.lang.VirtualMachineError and its thrown by the JVM when it ran out of the heap memory. This error can be fixed by providing more memory to run in the java application using following java options:

$>java MyProgram –Xms1024m –Xmx1024m –XX:PermSize=64m –XX:MaxPermSize=256m

*********

#### Can we have an empty catch block?

Answer: Yes, we can use an empty catch block but it’s not a right way of programming. When we use an empty catch block and if it catches any exception then we will have no information about that exception and it will be a nightmare of the situation to debug it. There should be a log statement file for logging all the exception details.

********

#### What happens when an exception is thrown by the main method?

Answer: When the main0 method throws out an exception then the Java Runtime Environment terminates the program and the print the exception message which was stacked in system console.

************

####  What is JDBC API and when do we use it?

Answer: Java DataBase connectivity API allows us t work with the relational database in java programming. JDBC API classes and interfaces are the part of java.sql and javax.sql package. It is used for getting the database connection, run SQL queries and stored procedures in the database server and process the results.

JDBC API is designed in a way which allows loose coupling between our java program and actual JDBC drivers which makes our life easier from switching one database server to another.

**  ****

#### What is JDBC ResultSet?

Answer: JDBC ResultSet is like a table of data which represents a database result set, which is generated when a database is queried by an executing statement.



****************

***************************************

#### Explain the JVM architecture?

Answer: Java Virtual Machine is the abstract machine or specification that provides a runtime environment to execute the bytecode. JVM supports Java and many other languages known as [JVM languages](https://www.whizlabs.com/blog/jvm-languages/), the program written in these languages is compiled into the bytecode and then executed by the JVM. contains key components which are classloader, memory area, execution engine etc.

**a) Classloader**

It is a subsystem of JVM which load class files. Whenever a Java program is run, it is loaded by the classloader.

**b) Class Area**

Class Area holds class-level data of each class file such as metadata, constant run pool, and static variables.

**c) Heap**

It is the runtime data which is used for allocating objects.

**d) Stack**

The stack is used for storing temporary variable. This component has a stack frame which is allocated one frame to each thread and when the execution of the thread is completed then that frame is also gets destroyed.

**e) Registers**

This component contains the address of JVM instruction which currently being executed.

**f) Native Method Stack**

All the native method stack used in the application are stored in this.

**g) Execution Engine**

It contains:

- A virtual processor
- An interpreter that executes the instructions after reading the bytecode.
- JIT compiler, used for improving the performance due to the slow execution. It compiles the similar part of the bytecode at the same time which reduces the total time needed for compilation.

**h) Java Native Interface**

It provides an interface which is needed for communicating with another application developed in another language like C, C++, C# etc.



**********

#### What is the use of Classloader in Java?

Answer: A Java program is made up of a different number of custom classes and pre-defined classes. When a program is executed, JVM is used to load all the content of that needed class and through the use of Classloader JVM, it finds that class.

************

####  Which class is a superclass of all classes?

Answer: Java.lang.The object is the root class for all the java classes and we don’t need to extend it. Every other java classes fall back under the object. All the different non-primitive types including arrays are inherited directly or indirectly from this class.

*******

#### 4. Which class is a superclass of all classes?

Answer: Java.lang.The object is the root class for all the java classes and we don’t need to extend it. Every other java classes fall back under the object. All the different non-primitive types including arrays are inherited directly or indirectly from this class.

#### 5. What is the static keyword?

Answer: The static keyword is used with a class level variable to make it global so all the objects will be able to share the same variable. It can also be used with methods. A static method can access only static variables of the class and invoke only a static method of the class.

*************

####  What are finally and finalize in Java?

Answer: Finally block is used with a try-catch block to put the code that you always want to get executed even the execution is thrown by the try-catch block. Finally is just used for releasing the resources which were created by the try block.

Finalize() is a special method in Object class that we can override in our classes. Finalize() is called by the Garbage collector to collect the garbage value when the object is getting it. This method is generally overridden to release the system resources when garbage value is collected from the object.

*******************

####  What is Type casting in Java?

- Here are some basic rules to keep in mind when casting variables:
  1. Casting an object from a sub class to a super class doesn’t require an explicit cast.
  2. Casting an object from a super class to a sub class requires an explicit cast.
  3. The compiler will not allow casts to unrelated types.
  4. Even when the code compiles without issue, an exception may be thrown at run time if the object being cast is not actually an instance of that class. This will result in the run time exception ClassCastException.

**************

#### What is break and continue statement?

Answer: In a while or do-while loop, we use break for a statement to terminate the loop. We use a break statement in a switch statement to exit the switch case. We can also use break statement for terminating the nested loop.

The continue statement is used for skipping the current iteration of a for, while or do-while loop. 

*****************

#### What is an interface?

Answer: Interfaces are the core part of Java programming language used a lot in JDK, java design patterns, and most of the frameworks and tools. The interface provides a way to achieve abstraction in Java and used to define the contract for the subclasses to implement. , it’s better to use interfaces as a superclass in most of the cases.

****

#### What is the use of System class in Java?

Answer: This question is among the most common Java interview questions for freshers. Java System class is one of the core classes. One of the easiest ways to log information for debugging is System.out.print() method. System class is final so we can’t subclass and override its behavior through inheritance.

System class doesn’t provide any public constructors, so we can’t instantiate this class and that’s why all of its methods are static. Some of the utility methods of System class are for array copy, get the current time, and reading environment variables.



*********************************

####  What is an instanceof keyword?

Answer: We can use instanceof keyword in java to check whether an object belongs to a class or not. We should avoid much usage of it

*************

####  What is an Iterator?

Answer: Iterator interface provides methods to iterate over any collection. We can get iterator instance from a collection using iterator() method. Iterator takes the place of Enumeration in the Java Collection Framework. The iterator allows the caller to remove elements from the underlying collection during the iteration. Java Collection iterator provides a generic way for transversal elements of a collection and implements Iterator Design Pattern.

******

####  What is the Java Collections Framework?

Answer: Collections are used in every programming language and when initial java was released it contained few classes for collections: Vector, Stack, Array, and Hashtable. But for larger scope and usage, Java 1.2 came up with Collection Framework that grouped all the collections interfaces, implementations, and algorithms.

Java Collection has come a long way with the usage of Generic and concurrent Collection classes for thread-safe operations. It has included blocking interfaces and their implementations in Java concurrent package.

************

#### . Explain the Java Exception Hierarchy.

Answer: Java Exceptions are hierarchical and inheritance is used for categorizing the different types of exceptions. Throwable is the parent class of Java Exceptions Hierarchy and it has two child objects – Error and Exceptions.

Errors are exceptional scenarios which are out of the scope of applications and it’s not possible to anticipate and recover from them, for example, hardware failure, JVM crash or out of memory error. Exceptions are further divided into checked and runtime exception.

**Checked exceptions** are exceptional scenarios that we can anticipate in a program and try to recover from it, for example, FileNotFoundException. We should catch this exception and provide a useful message to the user and log it properly for debugging purpose. The exception is the parent class of all the Checked exceptions.

**Runtime exceptions** are caused by bad programming, for example, trying to retrieve an element from the Array. At first, we should check the length of the array before trying to retrieve the element otherwise it might throw ArrayIndexOutOfBoundException at runtime. RuntimeException is the parent class of all runtime exceptions.

**********

####  What happens when an exception is thrown by the main method?

Answer: When an exception is thrown by the main() method, Java Runtime terminates the program and print the exception message and stack trace in system console.

***********







