---
title: "Jocular Java Facts 3-18-21"
published: true
---

Hello and welcome to the third release of Aj’s Jocular Java facts, so called because it’s alliterative, not necessarily because it’s funny.

When’s the last time you used a stream? Streams were added to Java 8 as part of an effort to add more functional programming elements to the Java language. I personally love them. Streams are intended to perform common tasks in a way that is declarative rather than imperative. In short, you tell Java what you want, rather than how to do it. As an example, let’s say you have a list of rock stars and the bands they belong to. You would like to group them together so that they are with fellow members of their bands. Doing this imperatively is a bit of a pain. You would have to create a map from band to list of rock stars, loop through all the rock stars, check their band and append the rock star to the appropriate band (or initialize the list if it hasn’t already been initialized). In contrast, with a stream, you would simply type the following:

```java
Map<Band, List<RockStar>> rockStarsByBand = 
    rockStars.stream()
    .collect(groupingBy(RockStar::getBand));
```

Streams have other benefits in addition to often being simpler to write than imperative code. They are intended to be side-effect free which means that their operations should not affect other parts of your code. They are also inherently immutable, returning a new List instead of modifying the current one. They are often more efficient, or only slightly less efficient than what you would write imperatively.

You can overuse streams, just like anything, so you have to be careful that your use of streams is actually making the code simpler and not actually complicating it.

As an aside, Kotlin, which is a JVM targeting language designed to address common criticisms of Java, has streams as first-class objects in the language, and thus removes a lot of the boilerplate:
```kotlin
val rockStarsByBand = rockStars.groupBy { it.getBand() }
```