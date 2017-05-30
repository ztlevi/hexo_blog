---
title: Some tricks in Java
categories: coding
tags: coding
date: 2017-05-29 22:13:07
---

# Java

Some basic knowledge of Java in the book "Cracking the Coding Interview, 6th Edition".

Your interviewer may be equally---or more---impressed if you can derive the answer than if you automatically knew it. Don't try to bluff though.

## Overloading vs. Overriding P165

Overloading is a term used to describe when two methods have the same name but differ in the type or number of arguments.

``` java
public double computeArea(Circle c) {...}
public double computeArea(Square s) {...}
```

<!--more-->

Overriding, however, occurs when a method shares the same name and function signature as another method in its super class.

## Collection Framework P166

Java's collection framework is incredibly useful.

- ArrayList: An ArrayList is dynamically resizing array, which grows as you insert elements.
- Vector: A vector is very similar to ArrayList, while Vector is synchronized. This means if one thread is working on Vector, no other thread can get a hold of it. Unlike ArrayList, only one thread can perform an operation on vector at a time.
- LinkedList: LinkedList is, of course, Java's built-in ListkedList class. Though it rarely comes up in an interview, it's useful to study because it demonstrates some of the syntax for an iterator.
- HashMap: The HashMap collection is widely used, both in interviews and in the real world. Also Set collections like HashSet are required to learn.

