---
title: 'Java: you do not know Ⅱ'
categories: coding
tags: [coding, java]
date: 2017-06-05 18:19:51
---
#  *Treemap*, *HashMap*, *LinkedHashMap* <P436>
Q: Explain the differences between *TreeMap*, *HashMap*, and *LinkedHashMap*. Provide an example of when each one would be best.

A: The most important distinction between these classes is the time guarantees and the ordering of the keys.

- *HashMap* offers O(1) lookup and insertion. If you iterate through the keys, though, the ordering of the keys is essentially arbitrary. It is implemented by an array of linked lists.
- *TreeMap* offers P(logN) lookup and insertion. Keys are ordered, so if you need to iterate through the keys in sorted order, you can. This means that keys must implement the *Comparable* interface. TreeMap is implemented by a Red-Black Tree.
- *LinkedHashMap* offers O(1) lookup and insertion. Keys are ordered by their insertion order. It is implemented by doubly-linked buckets.

<!--more-->

Q: What suppose to the key ordering with the input ordering {1, -1, 0}?

A:
| HashMap      | LinkedHashMap | TreeMap    |
|--------------|---------------|------------|
| any ordering | {1, -1, 0}    | {-1, 0, 1} |

Q: When might you need ordering in real life?

A:
- Suppose you were creating a mapping of names to *Person* objects. You might want to periodically output the people in alphabetical order by name. A *TreeMap* lets you do this.
- A *TreeMap* also offers a way to, given a name, output the next 10 people. This could be useful for a "More" function in many applications.
- A *LinkedHashMap* is useful whenever you need the ordering of keys to match the ordering of insertion. This might be useful in a caching situation, when you want to delete the oldest item.

Generally, unless there is a reason not to, you would use *HashMap*.

# Object Reflection <P437>

Q: Explain what object reflection is in Java and why it is useful?

A: Object Reflection is a feature in Java that provides a way to get reflective information about Java classes and objects, and perform operations such as:

1. Getting information about the methods and fields present inside the class at runtime.
2. Creating a new instance of a class.
3. Getting and setting the object fields directly by getting field reference, regardless of what the access modifier is.

# Lambda Expression <P438>

Q: There is a class *Country* that has methods *getContinent()* and *getPopulation()*. Write a function *int getPopulation(List<Country> countries, String continent)* that computes the total population of a given continent, given a list of all countries and the name of a continent.

A: This question really comes in two parts. First, We need to generate a list of the countries in North America. Then, we need to compute their total population.

Without lambda expression, this is fairly straightforward to do.

```java
int getPopulation(List<Country> countries, String continent) {
    int sum = 0;
    for (Country c : countries) {
        if (c.getContinent().equals(continent)) {
            sum += c.getPopulation();
        }
    }
    return sum;
}
```

To implement this with lambda expression, let's break this up into multiple parts.

```java
int getPopulation(List<Country> countries, String continent) {
    /* Filter countries.*/
    Stream<Country> northAmerica = countries.stream.filter(
        country -> {return country.getContinent().equals(continent);}
    );

    /* Convert to list of populations.*/
    Stream<Integer> populations = northAmerica.map(
        c -> c.getPopulation()
    );

    /* Sum list.*/
    int population = populations.reduce(0, (a, b) -> a + b);
    return population;
}
```

Alternatively, the following code will disregard the countries no within *continent* according to the sum.

```java
int getPopulation(List<Country> countries, String continent) {
    Stream<Integer> populations = countries.stream().map(
        c -> c.getPopulation().equals(continent) ? c.getPopulation() : 0
        );

    return populations.reduce(0, (a, b) -> a + b);
}
```

# Lambda Random <P439>

Q: Using Lambda expressions, write a function *List<Integer> get RandomSubset(List<Integer> list)* that returns a random subset of arbitrary size. All subsets (including the empty set) should be equally likely to be chosen.

A: To implement this approach using lambda expressions, we can do the following:

```java
List<Integer> getRandomSubset(List<Integer> list) {
    Random random = new Random();
    List<integer> subset = list.stream().filter(
        k -> {return random.nextBoolean(); // Flip coin
        }).collect(Collectors.toList());
    return subset;
}
```
