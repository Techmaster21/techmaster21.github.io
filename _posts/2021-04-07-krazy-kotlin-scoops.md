---
title: "Krazy Kotlin Scoops 4-07-21"
published: true
---

Hello and welcome to another installment of Aj’s Krazy Kotlin Scoops brought to you by my Kotlin fever dream last night.

Do you know what Kotlin is? You should, because I’ve mentioned it before in one of Aj’s Jocular Java Facts! It’s a language that runs on the JVM and which was designed with seamless Java interoperability in mind, while also fixing common problems with Java. Let me go through just a small subset:
1.	Types must be explicitly nullable. Null pointer exceptions are almost a thing of the past in Kotlin! All types are by default non-nullable which means that you cannot assign anything that might be a null to them without checking if they’re null first. The compiler enforces this ensuring you will never be surprised to receive a null from a method again! Also it provides several useful language features for working with null, such as object?.property which resolves to object.property is object is not null, and null otherwise; as well as variable ?: other which returns variable if it is not null and other otherwise
2.	No more worrying about the difference between primitives and objects. There are no primitives in Kotlin, except when it comes to the compiler. The compiler intelligently determines which of your Ints should be compiled to primitives and which need to be objects. Generally, they are only compiled to objects if you use the type Int? which means it could be null.
3.	Way more functional methods. Remember that groupingBy deal in Java and how much shorter it was in Kotlin? That’s because in Kotlin, they have implemented way more functional-style methods that Java doesn’t even have! And they’ve made using them way more intuitive (how do you group by something then map the values in Java? I can never remember, it’s so obtuse. In Kotlin it’s just groupBy {}.mapValues {} and that was from the top of my head)
4.	Data classes. Java 15 has these in Records, but Kotlin has had them a lot longer, and they can be deconstructed like so val (firstName, lastName, age) = person
5.	Speaking of val, Kotlin makes you choose at declaration whether a variable should be able to be reassigned or not. val’s cant be, while var’s can. Also Kotlin can usually automatically infer the type of the variable by how you use it!
6.	Pattern matching via the when() expression
7.	It’s the official language of Android development. This isn’t a feature, but it shows you it has a big supporter in Google.
8.	About 100 more things I could list but this email needs to end at some point
