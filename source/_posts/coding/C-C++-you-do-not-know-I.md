---
title: "C and C++: you do not know"
categories: coding
tags: [coding, c, c++]
date: 2017-05-29 22:08:56
---

Some basic knowledge of C and C++ in the book[^1]. Well, I pick the title "you don't know". Precisely, it's something I
don't know while you may already knew years ago. But it just sounds so stupid to named after "Java: I don't know"...

# Pointers an References

1.  A pointer holds the address of a variable and can be used to perform any operation that could be directly done on
    the variable, such as accessing and modifying it.
2.  Note that the size of a pointer varies depending on the architecture: 32 bits on a 32-bit machine and 64 bits on a
    64-bit machine.
3.  A reference is another name (an alias) for a pre-existing object and it does not have memory of its own. Unlike
    pointers, references cannot be null and cannot be reassigned to another piece of memory.

<!--more-->

# Hash Table vs STL Map <p423>

1.  Since hash tables use the key to find the index that will store the value, an insert or loopup can be done in
    amortized O(1)
2.  A hash table is traditionally implemented with an array of linked lists, where each node in the linked list holds
    two pieces of data: the value and the original key.
    - We want to use a good hash function to ensure that the keys are well distributed.
    - No matter how good the hash function is, there are still collisions.
    - We may also wish to implement methods to dynamically increase or decrease the hash table size depending on
      capacity. For example, when the ratio of the number of elements to the table size exceeds a certain threshold, we
      may wish to increase the hash table size. This would mean creating a new hash table and transferring the entries
      from the old table to the new table. Because this is an expensive operation, we want to be careful to not do it
      too often.

## Q: How is a hash table implemented?

A: A hash table is traditionally implemented with an array of linked lists, where each node in the linked list holds two
pieces of data: the value and the original key. When we want to insert a key value pair, we map the key to index in the
array using a hash function. The value is then inserted into the linked list at that position.

> Note that the elements in a linked list at a particular index of the array do not have the same key. Rather,
> _hashFunction(key)_ is the same for these values.

![hash table](https://ws1.sinaimg.cn/large/006tKfTcgy1fixt173z44j30v60iojss.jpg)

In addition, we will want to note the following design criteria:

1. We want to use a good hash function to ensure that the keys are well distributed. If they are not well distributed,
   then we would get a lot of collisions and the speed to find an element would decline.

2. No matter how good the hash function is, we still have collisions, so we need a method for handling them, This often
   means chaining via a linked list, but it's not the only way.

3. We may also wish to implement methods to dynamically increase or decrease the hash table size depending on capacity.
   For example, when the ratio of the number of element to the table size exceeds a certain threshold, we may wish to
   increase the hash table size. This would mean creating a new hash table and transferring the entries from the old
   table to the new table. Because this is an expensive operation, we want to be careful to not do it too often.

# Virtual Functions <p424>

1.  A virtual function depends on a "vtable" or "Virtual Table". A vtable is constructed which stores addresses of the
    virtual functions of this class. The compiler also adds a hidden vptr variable in all such classes which points to
    the vtable of that class.
2.  if a virtual functions is not overridden in the derived class, the vtable of of the derived class stores the address
    of the function in its parent class.
3.  The vtable is used to resolved the address of the function when the virtual functions is called.

# Shallow vs Deep Copy <p425>

1.  A shallow copy copies all the member values from one object to another. A deep copy does all this and also deep
    copies any pointer objects.
2.  One must also be careful with destructions of objects in a shallow copy.
3.  In real life, shallow copy is rarely used. Deep copy should be used in most cases, especially when the size of the
    copied structure is small.

# Volatile <p426>

1.  The key word volatile informs the compiler that the value of variable it it applied to can change from the outside,
    without any update done by the code.
2.  Declaration statement.

        int volatile x
        volatile int x

# Virtual Base Class: Why does a destructor in base class need to be declared virtual? <p427>

1.  If destructor were not virtual, then Foo's destructor would be called, even when p is really of type Bar.

        class Foo{}
        class Bar : public Foo{}
        Foo * p = new Bar()

[^1]: Cracking the Coding Interview, 6th Edition.
