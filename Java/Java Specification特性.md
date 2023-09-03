## Reference Books				

[Core Java Volumn I - Fundamentals]()

[The Java® Language Specification Java SE 8 Edition](https://docs.oracle.com/javase/specs/jls/se8/html/index.html)

[The Java Virtual Machine Specification, Java SE 8 Edition](https://docs.oracle.com/javase/specs/jvms/se8/html/index.html)

[深入理解JVM虚拟机 4th Edtion]()

[Java Performance](https://www.oreilly.com/library/view/java-performance-2nd/9781492056102/)

[Modern Java in Action](https://www.manning.com/books/modern-java-in-action)

[Java8 In Action](https://www.manning.com/books/java-8-in-action)

[Head First Java](https://learning.oreilly.com/library/view/head-first-java/9781492091646/)

[java in a nutshell](https://learning.oreilly.com/library/view/java-in-a/9781492037248/)



Oracle 

## Strength of Java

Java is not only a programming language, but also a platform, including JVM to support "compile once, run everywhere"

* 1.java is used everywhere

Web, internet of thing,   android mobile,  IOT, BIG DATA

* 2.JAVA TOOLS

IDE，

* 3.Java community

Industry, meetup, conference, mature, resources

* 4.ease of learning

## Chapters of Knowledge Point

###  Refrence Type 引用類型

Different with Primitive Type: byte, short, int, long, (numeric) float, double, boolean, char

Refrence Type includes 1.Class, 2.Interface, 3.Array, 4.Enumeration; 5. Annotation



*ClassDeclaration*: 

​	NormalClassDeclaration 

​	EnumDeclaration 

NormalClassDeclaration:

​	 { ClassModifier } class  Identifier  [ TypeParameters ]  [ Superclass ] [ Superinterfaces ] ClassBody

class contain class



```
top level class

nested class as follow 3:

member class, local class, annoymous class
```



Generics 泛型

**Generics** refer to the ability to use a [type](https://www.codecademy.com/resources/docs/java/data-types) as a parameter to [methods](https://www.codecademy.com/resources/docs/java/methods) and [classes](https://www.codecademy.com/resources/docs/java/classes). This provides the ability to define a set of related classes or methods that can operate on many different types with a single declaration. This also allows type safety at compile-time allowing invalid types to be caught during compilation.



### 1.*Behavior Parameterization* 行為參數化

use Lamda expression 

### 2.Functional Programming

函數式編程

#### 2.1.Stream



### 3.Lamada Expression



###  4.Nested Class

![a table showing qualities of non-static and static classes](https://static-assets.codecademy.com/Courses/intermediate-java/nested-classes/Art1720NestClassesStaticvsNonStatic-ForImplementation.svg)

#### **Implementing Inner (Non-Static Nested) Classes**

To instantiate a non-static nested class that can access other members of the outer class first we need to instantiate an object of the outer class: `Outer outer = new Outer()`. Next, we can instantiate an inner class object: `Outer.Inner inner = outer.new Inner()`. Note that we use the `outer` object along with the keyword `new` to create an instance of the inner class.

```java
class Lib {
  String objType;
  String objName;

  // Assign values using constructor
  public Lib(String type, String name) {
    this.objType = type;
    this.objName = name;
  }

  // private method
  private String getObjName() {
    return this.objName;
  }

  // Inner class
  class Book {
    String description;

    void setDescription() {
      if(Lib.this.objType.equals("book")) {
        if(Lib.this.getObjName().equals("nonfiction")) {
          this.description = "Factual stories/accounts based on true events";
        } else {
          this.description = "Literature that is imaginary.";
        }
      } else {
        this.description = "Not a book!";
        }
    }
    String getDescription() {
      return this.description;
    }
  }
}

public class Main {
  public static void main(String[] args) {
    Lib fiction = new Lib("book", "fiction");
    Lib.Book book = fiction.new Book();
    book.setDescription();
    System.out.println("Fiction Book Description = " + book.getDescription());

    Lib nonFiction = new Lib("book", "nonfiction");
    book = nonFiction.new Book();
    book.setDescription();
    System.out.println("Non-fiction Book Description = " + book.getDescription());

  }
}
```



#### **Implementing Static Nested Classes**

- Unlike non-static nested classes, static classes cannot access any non-static members of its enclosing class, including private and protected members.
- To instantiate a static nested class, you are not required to first instantiate its enclosing class.
- The keyword `static` in member creation is what differentiates a static member from a non-static member in any Java program.

```java
  class Outer {
    String outer;
    static String typeStatic = "static String type";
    String typeGeneric = "generic String type";
   
    // Assign values using constructor
    public Outer(String name) {
      this.outer = name;
    }
   
    // private method
    private String getName() {
      return this.outer;
    }
   
    // static nested class
    static class Inner {
      String inner;
      String outer;
   
      void printTypeMethod() {
        // Can access static member of outer class
        System.out.println("Type of member = " + typeStatic);
      }
    }
  }
```

  

![image-20220623173351844](https://tva1.sinaimg.cn/large/e6c9d24egy1h3ib7uhwbfj20wp0l5gmi.jpg)



### 5. Thread

![diagram of a thread inside a process](https://static-assets.codecademy.com/Courses/intermediate-java/threading/ART-1622-ThreadsOverview-ForImplementation.svg)

#### 5.1.extends Thread

instance field:  shared memory

#### 5.2. Implements Runnable

lambda expression

```java
public class Factorial {
 public int compute(int n) {
   // ... the code to compute factorials
 }
 
 public static void main(String[] args) {
   Factorial f = new Factorial();
 
   // the lambda function replacing the run method
   new Thread(() -> {
     System.out.println(f.compute(25));
   }).start();
 
   // the lambda function replacing the run method
   new Thread(() -> {
     System.out.println(f.compute(10));
   }).start();
 }
}
```

This syntax has several benefits:

- Your class no longer needs to extend `Thread` OR implement `Runnable`. You can make a thread from anything!
- Your class no longer needs a constructor to store arguments! Since you can pass an argument directly into the compute function when you create your thread, we no longer need to create a separate instance of our object any time we want to perform a threaded task with it.
- Your class is easier to read! The lambda syntax makes it so that people reading your code can immediately identify what task is being performed in your thread, without having to read your class first to find the `run` method.

#### 5.3.**Supervising a Thread**

```java
import java.time.Instant;
import java.time.Duration;
 
public class Factorial {
 public int compute(int n) {
   // the existing method to compute factorials
 }
 
 // utility method to create a supervisor thread
 public static Thread createSupervisor(Thread t) {
   Thread supervisor = new Thread(() -> {
     Instant startTime = Instant.now();
     // supervisor is polling for t's status
     while (t.isAlive()) {
       System.out.println(Thread.currentThread().getName() + " - Computation still running...");
       Thread.sleep(1000);
     }
   });
 
   // setting a custom name for the supervisor thread
   supervisor.setName("supervisor");
   return supervisor;
 
 }
 
 public static void main(String[] args) {
   Factorial f = new Factorial();
 
   Thread t1 = new Thread(() -> {
     System.out.println("25 factorial is...");
     System.out.println(f.compute(25));
   });
 
 
   Thread supervisor = createSupervisor(t1);
 
   t1.start();
   supervisor.start();
 
   System.out.println("Supervisor " + supervisor.getName() + " watching worker " + t1.getName());
 }
}
```

#### 5.4.**Waiting for Thread Completion**

communication between differentt Threads

#### 5.5.Thread Synchronization

Another important scenario when working with multi-threaded programs is *managing shared resources* between threads

### 6.Concurrency & parallelism

**Package: **java.util.concurrent

**Interface:** Executor, ExecutorService, Runnable, Callable, Future, Lock, Condition

* **Thread safe Collection** ConcurrentMap,  BlockingQueue

**Classes:** ThreadPoolExecutor, static Executors,  RecursiveAction, RecursiveTask

* **Thread safe Collection**  ConcurrentHashMap, ConcurrentLinkedDeque, ConcurrentLinkedQueue, ConcurrentSkipListMap, ConcurrentSkipListSet, CopyOnWriteArrayList, CopyOnWriteArraySet

**Exception:**  ExecutionException

Join & fork

ThreadPool





#### 6.0.Callable, Future for pooling

Similar to Runnable. Task that runs asynchronously

Definiton: The Callable interface is similar to Runnable, in that both are designed for classes whose instances are potentially executed by another thread. A Runnable, however, does not return a result and cannot throw a checked exception.

```java
		V call() throws Exception;

    //Future is blocking
    /**
     * Waits if necessary for the computation to complete, and then
     * retrieves its result.
     */
    V get() throws InterruptedException, ExecutionException;
```

#### 6.1. Executor Interface for pooling

Difference between Executor and Thread

Definiton:  An object that executes submitted tasks. This interface provides a way of decoupling **task submission** from **the mechanics** of how each task will be run, including details of thread use, scheduling, etc

```java
void execute(Runnable command);
```

#### 6.2.ExecutorService

Definiton:  An Executor that provides methods to manage termination and methods that can produce a **Future** for tracking progress of one or more asynchronous tasks.

```java
public interface ExecutorService implements Executor{
	 void shutdown();
  
   <T> Future<T> submit(Callable<T> task);
   Future<?> submit(Runnable task);
}     
```

#### 6.3.ThreadPoolExecutor 

```java
public abstract class AbstractExecutorService implements ExecutorService {
      
}

ExecutorService executorService = Executors.newSingleThreadPool();
Future<T> future = executorService.submit(new Callable<T>());
if (future.isDone()){
  T t = future.get(); // Blocking
}
executorService.shutdown();


public abstract class ScheduledExecutorService implements ScheduledExecutorService {
     public <V> ScheduledFuture<V> schedule(Callable<V> callable, long delay, TimeUnit unit);
}
```

### 7.Generics

#### 7.0.Why use generics?

- Stronger type checks at compile time.

- Elimination of casts.

  The following code snippet without generics requires casting:

  ```
  List list = new ArrayList();
  list.add("hello");
  String s = (String) list.get(0);
  ```

  When re-written to use generics, the code does not require casting:

  ```
  List<String> list = new ArrayList<String>();
  list.add("hello");
  String s = list.get(0);   // no cast
  ```

- Enabling programmers to implement generic algorithms

  By using generics, programmers can implement generic algorithms that work on collections of different types, can be customized, and are type safe and easier to read.

#### 7.1.Type Parameters

Cast is must after retrieve Object from generics Collection 

#### 7.2.Generic Class/ Method/ Interface

Type Variables

#### 7.3 Type erasure

#### 7.4.Restrictions and Limitations

 refer to 8.6 Restrictiosn and Limitations of Book [[Core Java Volumn I - Fundamentals]()]

* Type Parameters can not be instantiated by Primitive Types
* Cannot instantiate Type Variables
* Cannot construct a generic Array

#### 7.5. Rules using Genericsn and inheretance

[**Rules To Follow While Implementing Generic Interfaces:**](https://javaconceptoftheday.com/generic-interfaces-java/)

- Only generic classes can implement generic interfaces. Normal classes can’t implement generic interfaces. For example, above generic interface can be implemented as,
- A normal class can implement a generic interface if type parameter of generic interface is a wrapper class. For example, below implementation of GenericInterface is legal.
- Class implementing generic interface at least must have same number and same type of parameters and at most can have any number and any type of parameters.
- You can change the type of parameter passed to generic interface while implementing it. When changed, the class which is implementing should have new type as parameter and also, you have to change old type with new type while implementing the methods.

[Generics And Their Inheritance ](https://javaconceptoftheday.com/generics-and-their-inheritance/)

- A generic class can extend a non-generic class.
- Generic class can also extend another generic class. When generic class extends another generic class, sub class should have at least same type and same number of type parameters and at most can have any number and any type of parameters.

- Non-generic class can’t extend generic class except of those generic classes which have already pre defined types as their type parameters.

* 

Sample: http://www.java2s.com/Tutorials/Java/Java_Language/8030__Java_generic_hierarchy.htm

https://docs.oracle.com/javase/tutorial/java/generics/inheritance.html
