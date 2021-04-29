---
title: "Jocular Java Facts 3-8-21"
published: true
---

Hello and welcome to the second release of Aj’s Jocular Java facts, so called because it’s alliterative, not necessarily because it’s funny.

First of all, happy International Women’s day! Did you know that COBOL, a business oriented language whose syntax is designed to resemble English, was partly based on an earlier language designed by rear admiral Grace Hopper? She also found an actual computer bug in 1947, when she discovered a moth was behind the issues they were having with Harvard University’s Mark II! This moth and the related log is currently housed in the Smithsonian Museum of American History, but is not currently on display. This story is often told as the origin of the word bug to describe such an engineering/computer flaw, but in fact that usage of the word had been around since at least the time of Edison! A fact I first learned minutes ago while making sure I got my facts straight 😄.

Now, onto the Java facts.

Do you use immutable objects? You should! According to *Effective Java 3rd Edition*, item 17, you should work to “minimize mutability.” Why is that? Well there are several reasons. While it may feel more natural to describe an object as mutable, as that is the way we tend to think about object in the real world, in practice it tends to be more complicated to reason about. Mutable objects can be changed at any time and any place, and you have to constantly account for this when coding. This becomes an especially big issue when you are coding a concurrent system. You have to deal with issues like visibility, synchronization, deadlocks, etc. Immutable objects on the other hand, take care of a lot of these issues for you. There are some gotchas, but they are relatively straightforward unlike mutable gotchas. Immutability should be the default, until it’s determined that mutability would meaningfully improve performance or simplify usage. Did you know that if you are using Set, the contained objects can’t change with regards to the equals method? I didn’t until I read Effective Java! But it is documented, right at the top in the documentation for [Set](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html).

So how do you create an immutable object? The basic procedure for Java is documented [here](https://docs.oracle.com/javase/tutorial/essential/concurrency/imstrat.html) but can be summed up in the following sentence: The view of your object you provide to the outside world should never change, under any circumstances. For more information, I recommend referring *Effective Java 3rd Edition* item 17, but you can probably find the same information on the internet. 

There are a few tools that can help you create immutable objects. If you are creating value classes (classes whose main purpose is to hold values), then AutoValue or Immutables is a great choice. Lombok can also produce immutable objects, but it also can create mutable objects, so you have to be careful to only use the annotations that will produce an immutable object. For immutable versions of built in Java objects, like Map or List, look at `Guava` or `Eclipse Collections`. As a final note, this isn’t technically a Java specific fact. While I’ve focused on Java specific resources and libraries, you can create immutable objects in nearly every language with OOP features. In most functional languages, immutability is even the default!

Think immutably!
