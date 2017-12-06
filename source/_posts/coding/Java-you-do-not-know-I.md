---
title: "Java: you do not know I"
categories: coding
tags: [coding, java]
date: 2017-05-29 22:13:07
---

Some basic knowledge of Java in the book[^1]. Well, I pick the title "you don't know". Precisely, it's something I don't know while you may already knew years ago. But it just sounds so stupid to named after "Java: I don't know"...

Your interviewer may be equally---or more---impressed if you can derive the answer than if you automatically knew it.


# Overriding

```java
public double computeArea(Circle c) {...}
public double computeArea(Square s) {...}
```

Overriding, however, occurs when a method shares the same name and function signature as another method in its super class.

<!--more-->

# Collection Framework <P166>

Java's collection framework is incredibly useful.

- ArrayList: An ArrayList is dynamically resizing array, which grows as you insert elements.
- Vector: A vector is very similar to ArrayList, while Vector is synchronized. This means if one thread is working on Vector, no other thread can get a hold of it. Unlike ArrayList, only one thread can perform an operation on vector at a time.
- LinkedList: LinkedList is, of course, Java's built-in ListkedList class. Though it rarely comes up in an interview, it's useful to study because it demonstrates some of the syntax for an iterator.
- HashMap: The HashMap collection is widely used, both in interviews and in the real world. Also Set collections like HashSet are required to learn.

# Private Constructor <P433>
Q: In terms of inheritance, what is the effect of keeping a constructor private?

This has direct implications for inheritance, since a subclass class calls its parent's constructor. Who, other than A, can access A's private methods and constructor? A's inner classes can. This means, the class A can be inherited, but only by its own or its parent's inner classes.

# Return from Finally <P433>
Q: In Java, does the finally block get executed if we insert a return statement inside the try block o a try-catch-finally?

Yes, it will get executed. The finally block always executes when the try block exits. This ensures that the finally block is executed even if an unexpected exception occurs. But finally is useful for more than just exception handling — it allows the programmer to avoid having cleanup code accidentally bypassed by a return, continue, or break. Putting cleanup code in a finally block is always a good practice, even when no exceptions are anticipated.

Note: If the JVM exits while the try or catch code is being executed, then the finally block may not execute. Likewise, if the thread executing the try or catch code is interrupted or killed, the finally block may not execute even though the application as a whole continues.

# What's the difference between final, finally, and finalize? <P433-435>
Despite their similar sounding names, **final**, **finally** and **finalize** have very different purposes.
To speak in very general terms:
1. The **final** is used to control whether a variable, method, or class is "changeable".

The **final** statement has a different meaning depending on context.

- When applied to a variable(primitive): The value of the variable cannot change.
- When applied to a variable(reference): The reference variable cannot point to any other object on the heap.
- When applied to a method: The method cannot be overridden.
- When applied to a class: The class cannot. be subclassed

2. The **finally** keyword is used in a try/catch block to ensure that a segment of code is always executed.

There is an optional **finally** block after the try block or after the catch block. The **finally** block is often used to write the clean-up code. It will be executed after the try and catch blocks, but before control transfers back to its origin.

3. The **finalize**() method is called by the garbage collector once it determines that no more references exist.

The automatic garbage collector calls the **finalized**() method just before actually destroying the object. A class can therefore override the **finalized**() method from the Object class in order to define custom behavior during garbage collection.

```java
protected void finalize() throws Throwable {
    /* Close open files, release resources, etc */
}
```

# Generics vs Templates <P435>
Q: Explain the difference between templates in C++ dand generics in Java.

Many programmers consider templates and generics to be essentially equivalent because both allow you to do something like **List<String>**. But, how each language does this, and why, varies significantly.

The implementation of Java generics is rooted in an idea of "type erasure". This technique eliminates the parameterized types then source code is translated to the Java Virtual Machine(JVM) byte code.

For example, suppose you have the Java code below:

```java
Vector<String> vector = new Vector<String>();
vector.add(new String("hello"));
String str = vector.get(0)
```
During the compilation, this code is re-written into:

```java
Vector vector = new Vector();
vector.add(new String("hello"));
String str = (String) vector.get(0);
```

The use of Java generics didn't really change much about our capabilities; it just made things a bit prettier. For this reason, Java generics are sometimes called "syntactic sugar".

This is quite different from C++. In C++, templates are essentially a glorified macro set, with the compiler creating a new copy of the template code for each type.

In Java, static variables are shared across instances of Class, regardless of the different type parameters.

There are other differences between Java generics and C++ templates.
- C++ templates can use primitive types, like **int**, Java cannot and must instead use **Integer**.
- In Java, you can restrict the template's type parameters to be of a certain type. For instance, you might use generics to implement a **CardDeck** and specify that the type parameter must extend from **CardGame**.
- In C++, the type parameter can be instantiated, whereas Java does not support this.
- In Java, the type parameter cannot be used for static methods and variables, since these would be shared between classes. In C++, these classes are different, so the type parameter can be used for static methods and variables.
- In Java, all instances of the same class, regardless of their type parameters, are the same type. The type parameters are erased at runtime. In C++, instances with different type parameters are different types.

[^1]: Cracking the Coding Interview, 6th Edition.
