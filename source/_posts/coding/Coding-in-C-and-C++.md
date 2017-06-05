---
title: "C and C++: you do not know"
categories: coding
tags: [coding, c, c++]
date: 2017-05-29 22:08:56
---
<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-generate-toc again -->
**Table of Contents**

- [C and C++](#c-and-c)
    - [Pointers an References](#pointers-an-references)
    - [Hash Table vs STL Map p423](#hash-table-vs-stl-map-p423)
    - [Virtual Functions p424](#virtual-functions-p424)
    - [Shallow vs Deep Copy p425](#shallow-vs-deep-copy-p425)
    - [Volatile p426](#volatile-p426)
    - [Virtual Base Class: Why does a destructor in base class need to be declared virtual? p427](#virtual-base-class-why-does-a-destructor-in-base-class-need-to-be-declared-virtual-p427)

<!-- markdown-toc end -->
<!--more-->
C and C++
=========

Some basic knowledge of C and C++ in the book[^1].

Pointers an References
----------------------

1.  A pointer holds the address of a variable and can be used to perform any operation that could be directly done on the variable, such as accessing and modifying it.
2.  Note that the size of a pointer varies depending on the architecture: 32 bits on a 32-bit machine and 64 bits on a 64-bit machine.
3.  A reference is another name (an alias) for a pre-existing object and it does not have memory of its own. Unlike pointers, references cannot be null and cannot be reassigned to another piece of memory.

Hash Table vs STL Map p423
--------------------------

1.  Since hash tables use the key to find the index that will store the value, an insert or loopup can be done in amortized O(1)
2.  A hash table is traditionally implemented with an array of linked lists, where each node in the linked list holds two pieces of data: the value and the original key.
    -   We want to use a good hash function to ensure that the keys are well distributed.
    -   No matter how good the hash function is, there are still collisions.
    -   We may also wish to implement methods to dynamically increase or decrease the hash table size depending on capacity. For example, when the ratio of the number of elements to the table size exceeds a certain threshold, we may wish to increase the hash table size. This would mean creating a new hash table and transferring the entries from the old table to the new table. Because this is an expensive operation, we want to be careful to not do it too often.

Virtual Functions p424
----------------------

1.  A virtual function depends on a "vtable" or "Virtual Table". A vtable is constructed which stores addresses of the virtual functions of this class. The compiler also adds a hidden vptr variable in all such classes which points to the vtable of that class.
2.  if a virtual functions is not overridden in the derived class, the vtable of of the derived class stores the address of the function in its parent class.
3.  The vtable is used to resolved the address of the function when the virtual functions is called.

Shallow vs Deep Copy p425
-------------------------

1.  A shallow copy copies all the member values from one object to another. A deep copy does all this and also deep copies any pointer objects.
2.  One must also be careful with destructions of objects in a shallow copy.
3.  In real life, shallow copy is rarely used. Deep copy should be used in most cases, especially when the size of the copied structure is small.

Volatile p426
-------------

1.  The key word volatile informs the compiler that the value of variable it it applied to can change from the outside, without any update done by the code.
2.  Declaration statement.

        int volatile x
        volatile int x

Virtual Base Class: Why does a destructor in base class need to be declared virtual? p427
-----------------------------------------------------------------------------------------

1.  If destructor were not virtual, then Foo's destructor would be called, even when p is really of type Bar.

        class Foo{}
        class Bar : public Foo{}
        Foo * p = new Bar()

[^1]: Cracking the Coding Interview, 6th Edition.
