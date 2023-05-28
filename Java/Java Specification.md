## Reference Books				

[The Java® Language Specification Java SE 8 Edition](https://docs.oracle.com/javase/specs/jls/se8/html/index.html)

[The Java Virtual Machine Specification, Java SE 8 Edition](https://docs.oracle.com/javase/specs/jvms/se8/html/index.html)

[深入理解JVM虚拟机 4th Edtion]()

[Java Performance](https://www.oreilly.com/library/view/java-performance-2nd/9781492056102/)

[Modern Java in Action](https://www.manning.com/books/modern-java-in-action)

[Java8 In Action](https://www.manning.com/books/java-8-in-action)

[Head First Java](https://learning.oreilly.com/library/view/head-first-java/9781492091646/)

[java in a nutshell](https://learning.oreilly.com/library/view/java-in-a/9781492037248/)

## Strength of Java

* 1.java is used everywhere

Web, internet of thing,   android mobile,  IOT, BIG DATA

* 2.JAVA TOOLS

IDE，

* 3.Java community

Industry, meetup, conference,   mature, resources

* 4.ease of learning

## Chapters of Knowledge Point

###  Refrence Type

Primitive Type: numeric, boolean

Class Type, Array Type, Interface Type



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





### 1.*Behavior Parameterization*



### 2.Functional Programming



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

#### 1.extends Thread

instance field:  shared memory

#### 2. Implements Runnable

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

#### 3.**Supervising a Thread**

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

#### 4.**Waiting for Thread Completion**

communication between differentt Threads

#### 5.Thread Synchronization

Another important scenario when working with multi-threaded programs is *managing shared resources* between threads
