---
title: "Databases: you do not know"
categories: coding
tags: coding
date: 2017-07-05 10:20:33
---

# Implicit and Explicit join p169

## Explicit Join

```sql
SELECT CourseName, TeacherName
From Courses INNER JOIN TEACHERS
ON Courses.TeacherID = Teachers.TeacherID
```

## Implicit Join

```sql
SELECT CourseName, TeacherName
FROM Courses, Teachers
WHERE Courses.TeacherID = Teachers.TeacherID
```

<!--more-->

# Denormalized vs. Normalized Databases <p169>

Normalized databases are designed to minimize redundancy, while denormalized databases are designed to optimized read
time.

In a traditional normalized database with data like Courses and Teachers, Courses might contain a column called
TeacherID, which i a foreign key to Teacher. One benefit of this is that information about the teacher (name, address,
etc.) is only stored once in the database. The drawback is that many common queries will require expensive joins.

Instead, we can denormalize the database by storing redundant data. For example, if we knew that we would have to repeat
this query often, we might store the teacher's name in the Courses table. Denormalization is commonly used to create
highly scalable systems.

## Pros and Cons

| Cons of Denormalization                                                    | Pros of Denormalization                                                                                             |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| Updates and inserts are more expensive.                                    | Retrieving data is faster since we do fewer joins.                                                                  |
| Denormalization can make update and insert code harder to write.           | Queries to retrieve can be simpler (and therefore less likely to have bugs), since we need to look at fewer tables. |
| Data maybe inconsistent. Which is the "correct" value for a piece of data? |                                                                                                                     |
| Data redundancy necessitates more storage.                                 |                                                                                                                     |

# Small Database Design <p171>

## Step 1: Handle Ambiguity

Database questions often have some ambiguity, intentionally or unintentionally. Before you proceed with your design, you
must understand exactly what you need to design.

Imagine you are asked to design a system to represent an apartment rental agency. You will need to know whether this
agency has multiple locations or just one. You should also discuss with your interviewer how general you should be. For
example, it would be extremely rare for a person to rent two apartments in the same building. But does that mean you
shouldn't be able to handle that? Maybe, maybe not. Some very rare conditions might be best handled through a work
around (like duplicating the person's contact information in the database).

## Step 2: Define the Core Objects

Next, we should look at the core objects of our system. Each of these core objects typically translates into a table. In
this case, our core objects might be Property, Building, Apartment, Tenant and Manager.

## Step 3

Outlining the core objects should give us a good sense of what the tables should be. How do these tables relate to each
other? Are they many-to-many? One-to-many?

## Step 4

Finally, we fill in the details. Walk through the common actions that will be taken and understand how to store and
retrieve the relevant data. We'll need to handle lease terms, moving out, rent payments, etc. Each of these actions
requires new tables and columns.
