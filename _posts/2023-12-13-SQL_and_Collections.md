---
toc: True
comments: True
layout: notebook
title: SQL Student Lesson Section
description: by Tirth T, Haseeb B, Sreeja G, Ekam K, Drew R, Adan R
---

Covering:
- Person model file
    - Lombok: @Data, @AllArgsConstructor, @NoArgsConstructor create getters, setters and toString methods
    - @Entity tag - indicates that this is a JPA entity that will be stored in SQL database records
    - @Id for private long Id - indicates that this will be a unique identifier for each entry in the SQL database
    - @GeneratedValue(strategy = GenerationType.AUTO) - indicates that the ID will be automatically generated based on the previous contents of the database
    - @NotEmpty, @Size(min=5), @Column(unique=true), @Email - these all set restrictions on the kind of information
- ManyToMany Relationship
    - A "Many-to-Many" relationship is a type of association in a relational database design where entities on both sides of the relationship can have multiple connections to each other. In other words, each entity on one side of the relationship can be associated with multiple entities on the other side, and vice versa.
    - The (fetch = EAGER) specifies that when a Person entity is loaded, its associated PersonRole entities should be fetched eagerly (loaded immediately along with the Person entity).
- ManyToOne Relationship
    - In the context of a relational database, a many-to-one relationship typically means that multiple instances of one entity (the "many" side) are associated with a single instance of another entity (the "one" side).
    - The tag being assigned to Notes indicates that it is the many side, so multiple notes can be attributed to one Person object but a note can only be associated with a single Person object.
- jsonb


```java
@ManyToMany(fetch = EAGER)
private Collection<PersonRole> roles = new ArrayList<>();

@JdbcTypeCode(SqlTypes.JSON)
@Column(columnDefinition = "jsonb")
private Map<String, Map<String, Object>> stats = new HashMap<>();
```
