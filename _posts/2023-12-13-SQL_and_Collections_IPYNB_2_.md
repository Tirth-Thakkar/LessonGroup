---
toc: True
comments: True
layout: notebook
title: SQL Student Lesson Section
description: by Tirth T, Haseeb B, Sreeja G, Ekam K, Drew R, Adan R
---

## SQL

SQL is a programming language focused on managing and manipulating relational (table-based) databases. It acts as the backbone for many of this class's project backends, allowing users to create, read, update and delete data efficiently. To get a better idea of how data is formatted with JPA to be stored in an SQL database, we'll be looking at the `Person` object in the lesson backend. Follow along in this notebook.

### Person Model File Setup

After the first three tags, which specify to Lombok that `@AllArgsConstructor` and `@NoArgsConstructor` methods should be created

The `@Entity` tag indicates that Person objects will be stored as entities in a database. Generally, entities' attributes are represented by values in columns in the SQLite table.


```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@Entity
@Convert(attributeName ="person", converter = JsonType.class)
public class Person //...
```

The `@Id` tag specifies to that this value will be used as the unique identifier for each object in the database, and `@GeneratedValue(strategy = GenerationType.AUTO)` allows these ID's to be automatically generated when a new Person is created. In order for data to be most easily differentiated and manipulated in a database, IDs are deeply important to use.


```java
@Id
@GeneratedValue(strategy = GenerationType.AUTO)
private Long id;
```

### Many-to-Many Relationship

A "Many-to-Many" relationship (shown in the @ManyToMany tag) indicates that entities on both sides of a relationship can have multiple connections with each other.

This condition allows for one object to be related to multiple different objects, and those different objects on the other side of the relationship can have their own relationship to other objects.


```java
@ManyToMany(fetch = EAGER)
private Collection<PersonRole> roles = new ArrayList<>();
```

(fetch = EAGER) specifies that, whenever a `Person` object is loaded, its corresponding `PersonRole` objects should be loaded simultaneously.

Objects in a "many-to-many" relationship often use "join tables" to represent the connections between these objects.

```text
| person_id | role_id |
|-----------|---------|
| 1         | 1       |
| 1         | 2       |
| 2         | 2       |
| 3         | 1       |
| 3         | 3       |
```

This is what a "join table" may look like with multiple interconnected people and roles. There is a table in the backend repository's SQLite.db called `person_roles` that acts as a join table for the two roles, but you'll notice that it's empty. If you can show it filled up, that sounds like a good reason to give extra points.

#### Popcorn Hack!

Explain in your own words what the relationship between `Person` objects and `PersonRole` objects is. Why is this relevant to collections? (Hint: In the code above, multiple `PersonRole` objects are stored within a `Person` object's roles attribute.)

### Many-to-One Relationship

On the other hand, there is also a "Many-to-One" relationship that can exist between two objects. It means that multiple instances of one entity (the "many" side) are associated with a single instance of another entity (the "one" side). This can be seen applied to the `Note` object in relation to the `Person` object.


```java
@ManyToOne(fetch = FetchType.LAZY, optional = false)
@JoinColumn(name = "tutorial_id", nullable = false) // notice this!
@OnDelete(action = OnDeleteAction.CASCADE)
@JsonIgnore
private Person person;
```

Notice the `@JoinColumn(name = "tutorial_id", nullable = false)` tag. Then, check the `note` table in the sqlite.db file.

#### Popcorn Hack!

Where do you see "tutorial_id" on the table? What does it represent in relation to the leftmost "id" column?

### Storing HashMaps with jsonb

JSONB is a binary representation of JSON data. It is a data type used in some relational databases (such as SQL databases) to store JSON documents in a more efficient and flexible way compared to traditional JSON. Within SQL databases, this data from the JSON can often be filtered, searched and/or extracted using provided functions.


```java
@JdbcTypeCode(SqlTypes.JSON)
@Column(columnDefinition = "jsonb")
private Map<String,Map<String, Object>> stats = new HashMap<>(); 
```

JSONB allows for the storage of nested and dynamic data structures. In the context of `Person` object stats, it means that each person can store activity data with the formatted date as the key, and the structure of this JSON data can be modified or extended without altering the database schema.

You can view the way this data is structured in the `person` sqlite.db table.
