---
toc: True
comments: True
layout: notebook
title: HashMaps, HashSets, Collections, SQL Student Lessons
description: by Tirth T, Haseeb B, Sreeja G, Ekam K, Drew R, Adan R
courses: {'csp': {'week': 1}}
type: hacks
---

# Collections

### What are collections?
Collections are any group of individual objects that are represented as a single unit is known as a Java Collection of Objects. In Java, a separate framework named the “Collection Framework” has been defined in JDK 1.2 which holds all the Java Collection Classes and Interface in it. It works as an interface that defines the highest-level of shared collection behavior, and extends Iterable which allows usage of ForEach loop.

### How are collections used? 
Collections can be used in the following ways

### Types of Collections

- **List:**  
    - Ordered collection
    - Allows duplicate elements
    - Example: **ArrayList** and **LinkedList**

- **Set:**  
    - Unordered collection 
    - No duplicates
    - Example: **HashSet** and **TreeSet**

- **Map:**  
    - Key-pair values
    - Each key must be unique
    - Example: **HashMap** and **TreeMap**

- **Queue:**  
    - Follows First-In-First-Out order
    - Example: **LinkedList** and **PriorityQueue**

- **Deque:**  
    - Double ended queue
    - Insertion and removal at both ends
    - Example: **ArrayDeque**

### Popcorn Hack!
Come up with a real world example in which collections are used! Write your answer below:

## HashMaps 

#### What are they? 

Hash Maps are a **data structure** with keys and values; very similar to a Python dictionary. The keys in Hash Maps have a single value assigned to them, which can be accessed by calling the key: 


```Java
import java.util.HashMap;  //Hashmaps are part of the java.util package

public class PlanetDistances {
    public static void main(String[] args) {

        HashMap<String, Double> hashMap = new HashMap<>();

        // key-value pairs, where the key is the planet (a string) and the value is the double assigned to each key
        hashMap.put("Mercury", 0.39);
        hashMap.put("Venus", 0.72); //adding an element
        hashMap.put("Earth", 1.00);
        hashMap.remove("Earth", 1.00); //removing an element

        // the value 0.39 can be accessed by calling the key "Mercury"
        double value = hashMap.get("Mercury");
        boolean exists = hashMap.containsKey("Mercury"); //you can also check if a key exists
        System.out.println("Mercury is " + value + " astronomical units away from the Sun");
    }
}

PlanetDistances.main(null);
```

    Mercury is 0.39 astronomical units away from the Sun


As shown above, the data type of the keys and values must be defined when creating the Hashmap. You cannot use data types for keys or values that are different from the ones assigned to it. Also, keys must be non-null objects. However, values can be null!

<br>

Keys in a Hashmap must be unique. Otherwise the previous values of the key get overwritten.


```Java
import java.util.HashMap;  

public class ShoePrices {
    public static void main(String[] args) {

        HashMap<String, Double> hashMap = new HashMap<>();

        hashMap.put("Nike", 41.97);
        hashMap.put("Nike", 80.97); //this value replaces the previous value 
        hashMap.put("Adidas", 69.99);
        hashMap.put("Vans", 55.00);

        double value = hashMap.get("Nike");
        System.out.println("A Nike shoe would cost " + value);
    }
}

ShoePrices.main(null);
```

    A Nike shoe would cost 80.97


#### Popcorn hack: what can we do if we want to assign multiple values to a single key? Do it below!: 




```Java
import java.util.HashMap;  

public class ShoePrices {
    public static void main(String[] args) {

        HashMap<String, Double> hashMap = new HashMap<>();

        hashMap.put("Nike", 41.97);
        hashMap.put("Nike", 80.97);
        hashMap.put("Adidas", 69.99);
        hashMap.put("Vans", 55.00);

        double value = hashMap.get("Nike");
        System.out.println("A Nike shoe would cost " + value);
    }
}

ShoePrices.main(null);
```

Note that collisions can still occur when two keys produce the same hash code. Hash codes are assigned to each key through a hash function (this is called hashing). They are used to determine what the key-value pair's index should be iwthin the Hashmaps. A bad hash function may cause collisions to occur, in which case the function would need to be adjusted. 

HashMaps do not store the input order of the key-value pairs, and there is no guarantee the pairs will always be stored in the same order. Therefore if something needs to be found within a HashMap, iteration must be used. This can be done through `keySet()`, `values()`, or `entrySet()`


<br>

**keySet()** -- provides access to the set of keys. Useful for if you only need to access keys w/out values 


```Java
import java.util.HashMap;
import java.util.Set;

public class OscarWinners {
    public static void main(String[] args) {

        HashMap<String, Integer> oscarWinnersYear = new HashMap<>();

        oscarWinnersYear.put("Nomadland", 2020);
        oscarWinnersYear.put("Parasite", 2019);
        oscarWinnersYear.put("Green Book", 2018);
        oscarWinnersYear.put("The Shape of Water", 2017);

        Set<String> oscarWinners = oscarWinnersYear.keySet(); //using keySet to get keys 

        System.out.println("List of Oscar winners " + oscarWinners);
    }
}

OscarWinners.main(null);
```

    List of Oscar winners [Nomadland, Parasite, Green Book, The Shape of Water]


**values()** -- returns set of values, without any keys 


```Java
import java.util.HashMap;
import java.util.Set;

public class OscarWinners {
    public static void main(String[] args) {

        HashMap<String, Integer> oscarWinnersYear = new HashMap<>();

        oscarWinnersYear.put("Nomadland", 2020);
        oscarWinnersYear.put("Parasite", 2019);
        oscarWinnersYear.put("Green Book", 2018);
        oscarWinnersYear.put("The Shape of Water", 2017);

        Collection<Integer> oscarWinnerYears = oscarWinnersYear.values(); //using values to get values 

        System.out.println("Years movies won Oscars " + oscarWinnerYears);
    }
}

OscarWinners.main(null);
```

    Years movies won Oscars [2020, 2019, 2018, 2017]


**entryset()** -- returns keys and values in the form of objects. Useful for when working with key-value pair relationships


```Java
import java.util.HashMap;
import java.util.Set;

public class OscarWinners {
    public static void main(String[] args) {

        HashMap<String, Integer> oscarWinnersYear = new HashMap<>();

        oscarWinnersYear.put("Nomadland", 2020);
        oscarWinnersYear.put("Parasite", 2019);
        oscarWinnersYear.put("Green Book", 2018);
        oscarWinnersYear.put("The Shape of Water", 2017);

        Set<Map.Entry<String, Integer>> oscarWinnersAndYears = oscarWinnersYear.entrySet(); //using values to get values 

        System.out.println("Oscars and their years " + oscarWinnersAndYears);
    }
}

OscarWinners.main(null);
```

    Oscars and their years [Nomadland=2020, Parasite=2019, Green Book=2018, The Shape of Water=2017]


HashMaps have a time complexity of O(1) on average!

## HashSet

### What is a hashset?
- A hashset is a data structure that stores only unique values and does not allow duplicates. You can also think of it as a set of keys with no values.  


```Java
import java.util.HashSet;
import java.util.Set;

public class Colors{
    static Set<String> colors = new HashSet<>();

    public static void main(String[] args) {
        colors.add("Red");
        colors.add("Blue");
        colors.add("Green");
        System.out.println(colors);
    }
}

Colors.main(null);
```

    [Red, Blue, Green]


### What if we add duplicates?
- If we try add duplicates, the hashset will simply not add the duplicate value and return false as seen bellow. 


```Java
public class ColorsButDifferent{
    static Set<String> colors = new HashSet<>();

    public static void main(String[] args) {
        System.out.println(colors.add("Blue"));
        System.out.println(colors.add("Green"));
        System.out.println(colors.add("Green"));
        System.out.println(colors);
    }
}

ColorsButDifferent.main(null);
```

    true
    true
    false
    [Blue, Green]


### Order?
- Hashsets are not ordered and do not store the order in which the values were added that means that if values are removed their order will not be preserved. 


```Java
public class Fruits{
    static Set<String> fruits = new HashSet<>();

    public static void main(String[] args) {
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        System.out.println(fruits);

        fruits.remove("Banana");

        System.out.println(fruits);
    }
}

Fruits.main(null);
```

    [Apple, Orange, Banana]
    [Apple, Orange]


### How do you know if a value is in a hashset?
- You can use the contains method to check if a value is in a hashset.


```Java
public class Fruits{
    static Set<String> fruits = new HashSet<>();

    public static void main(String[] args) {
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");

        System.out.println(fruits.contains("Apple"));
    }
}

Fruits.main(null);
```

    true


### Other methods
- clear() - removes all values from the hashset
- isEmpty() - returns true if the hashset is empty
- size() - returns the number of values in the hashset
- toArray() - returns an array of the values in the hashset



```Java
public class Fruits{
    static Set<String> fruits = new HashSet<>();

    public static void main(String[] args) {
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        System.out.println(fruits);

        System.out.println();
        System.out.println("Length of Hashmap: " + fruits.size());
        
        System.out.println();
        System.out.println("Array Version of Hashmap: " + fruits.toArray());

        System.out.println();
        fruits.clear();
        System.out.println("Hashmap After Clearing " + fruits);

    }
}

Fruits.main(null);
```

    [Apple, Orange, Banana]
    
    Length of Hashmap: 3
    
    Array Version of Hashmap: [Ljava.lang.Object;@665e264a
    
    Hashmap After Clearing []


### Iterations
- You can iterate through a hashset using a for each loop or an iterator. The order of the values is not guaranteed and can change as values are removed or added.
- These two methods are can be called using the `iterator()` and `forEach()` methods. For the `forEach()` method you can pass in a lambda expression (a lambda expression is an anonymous function) or a method reference.


```Java
// foreach loop to iterate through a set

public class Fruits{
    static Set<String> fruits = new HashSet<>();

    public static void main(String[] args) {
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");
        System.out.println(fruits);

        // Using foreach loop to iterate through the set and print each fruit as it goes
        fruits.forEach(fruit -> System.out.println(fruit));
    }
}

Fruits.main(null);

```

    [Apple, Orange, Banana]
    Apple
    Orange
    Banana



```Java
// Different version of foreach loop to iterate through a set

public class Cheeses{
    static Set<String> cheeses = new HashSet<>();

    public static void main(String[] args) {
        cheeses.add("Cheddar");
        cheeses.add("Brie");
        cheeses.add("Gouda");
        System.out.println(cheeses);

        cheeses.forEach(cheese -> {
            if(cheese.equals("Brie")) {
                System.out.println("I love " + cheese);
            } else {
                System.out.println("I like " + cheese);
            }
        });
    }
}

Cheeses.main(null);
```

    [Brie, Cheddar, Gouda]
    I love Brie
    I like Cheddar
    I like Gouda



```Java
// using iterator to iterate through a set

import java.util.Iterator;

public class Games{
    static Set<String> games = new HashSet<>();

    public static void main(String[] args) {
        games.add("Monopoly");
        games.add("Scrabble");
        games.add("Sorry");
        System.out.println(games);
        System.out.println();

        Iterator<String> iterator = games.iterator();
        while(iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}

Games.main(null);
```

    [Sorry, Monopoly, Scrabble]
    
    Sorry
    Monopoly
    Scrabble


### How to check for equality?
- You can check if two hashsets are equal by using the `equals()` method. This method will return true if the hashsets contain the same values and false if they do not.


```Java
public class Pokemon {
    public static void main(String[] args) {
        Set<String> pokemonSet1 = new HashSet<>();
        Set<String> pokemonSet2 = new HashSet<>();

        // Populate the sets
        pokemonSet1.add("Pikachu");
        pokemonSet1.add("Charmander");
        pokemonSet1.add("Pikaman");

        pokemonSet2.add("Pikachu");
        pokemonSet2.add("Charmander");
        pokemonSet2.add("Pikaman");

        // Check equality
        boolean areEqual = pokemonSet1.equals(pokemonSet2);
        System.out.println("Are the sets equal? " + areEqual);
    }
}

Pokemon.main(null);

```

    Are the sets equal? true


### Other kinds of hashsets
- There are other kinds of hashsets that are similar to the hashset but have some differences. These include the linkedhashset and the treeset. 
- The linkedhashset is similar to the hashset but it maintains the order in which the values were added. 
- The treeset is similar to the hashset but it sorts the values in ascending order.


```Java
// LinkedHashSet

import java.util.LinkedHashSet;
import java.util.Set;

public class LinkedHashSetExample {
    public static void main(String[] args) {
        Set<String> linkedHashSet = new LinkedHashSet<>();

        // Add elements
        linkedHashSet.add("Pikachu");
        linkedHashSet.add("Charmander");
        linkedHashSet.add("Pikaman");

        // Iterate through the LinkedHashSet
        System.out.println("LinkedHashSet: ");
        linkedHashSet.forEach(pokemon -> System.out.println(pokemon));
        System.out.println();

        linkedHashSet.remove("Pikachu");
        System.out.println("New hashset: " + linkedHashSet);
    }
}

LinkedHashSetExample.main(null);
```

    LinkedHashSet: 
    Pikachu
    Charmander
    Pikaman
    
    New hashset: [Charmander, Pikaman]



```Java
// TreeSet
import java.util.Set;
import java.util.TreeSet;

public class TreeSetExample {
    public static void main(String[] args) {
        Set<String> treeSet = new TreeSet<>();

        // Add elements
        treeSet.add("Alberquerque, New Mexico");
        treeSet.add("Pikachu");
        treeSet.add("Charmander");
        treeSet.add("Pikaman");

        // Iterate through the TreeSet
        treeSet.forEach(pokemon -> System.out.println(pokemon));
        // The values for the TreeSet are sorted alphabetically
    }
}

TreeSetExample.main(null);
```

    Alberquerque, New Mexico
    Charmander
    Pikachu
    Pikaman

