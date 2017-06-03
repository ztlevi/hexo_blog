---
title: Coding in Java
categories: coding
tags: [coding, java]
date: 2017-05-29 22:13:07
---

<!--more-->
# Java

Some basic knowledge of Java in the book[^1].

Your interviewer may be equally---or more---impressed if you can derive the answer than if you automatically knew it. Don't try to bluff though.

## Overloading vs. Overriding P165

Overloading is a term used to describe when two methods have the same name but differ in the type or number of arguments.

``` java
public double computeArea(Circle c) {...}
public double computeArea(Square s) {...}
```

Overriding, however, occurs when a method shares the same name and function signature as another method in its super class.

## Collection Framework P166

Java's collection framework is incredibly useful.

- ArrayList: An ArrayList is dynamically resizing array, which grows as you insert elements.
- Vector: A vector is very similar to ArrayList, while Vector is synchronized. This means if one thread is working on Vector, no other thread can get a hold of it. Unlike ArrayList, only one thread can perform an operation on vector at a time.
- LinkedList: LinkedList is, of course, Java's built-in ListkedList class. Though it rarely comes up in an interview, it's useful to study because it demonstrates some of the syntax for an iterator.
- HashMap: The HashMap collection is widely used, both in interviews and in the real world. Also Set collections like HashSet are required to learn.

## Private Constructor P433
Q: In terms of inheritance, what is the effect of keeping a constructor private?

This has direct implications for inheritance, since a subclass class its parent's conductor. The class A can be inherited, but its own or its parent's inner classes.

## Return from Finally P433
Q: In Java, does the finally block get executed if we insert a return statement inside the try block o a try-catch-finally?

Yes, it will get executed. The finally block always executes when the try block exits. This ensures that the finally block is executed even if an unexpected exception occurs. But finally is useful for more than just exception handling — it allows the programmer to avoid having cleanup code accidentally bypassed by a return, continue, or break. Putting cleanup code in a finally block is always a good practice, even when no exceptions are anticipated.

Note: If the JVM exits while the try or catch code is being executed, then the finally block may not execute. Likewise, if the thread executing the try or catch code is interrupted or killed, the finally block may not execute even though the application as a whole continues.

[^1]: Cracking the Coding Interview, 6th Edition.
