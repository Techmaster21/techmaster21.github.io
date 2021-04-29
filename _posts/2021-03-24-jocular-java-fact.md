---
title: "Jocular Java Facts 3-24-21"
published: true
---

Hello and welcome to the fourth release of Aj’s Jocular Java facts, so called because it’s alliterative, not necessarily because they’re funny.

Let’s talk about Java versions. The most commonly used Java version right now is version 8. Version 8 was released in March 2014, officially 7 years ago now. Java 11 is the next most popular, which was released in September 2018, only 2 and a half years ago. The current version of Java is 16 (released 8 days ago). 8 and 11 are both LTS, which means that they are supported for longer than the other versions. The next LTS release will be Java 17, which is due to release this September. 

Java tends to be pretty good at maintaining backwards compatibility, for better or for worse. The fact is, that if your dependencies are up to date and your code compiles, it almost certainly functions as it did before upgrading versions.

What does upgrading get you? For one, numerous performance, jar size, and memory usage improvements! For two, numerous language enhancements, highlights of which I will list here, by version starting at 9
* [9](http://cr.openjdk.java.net/~iris/se/9/latestSpec/): A modern HTTP client (has HTTP/2 and Websocket support)
* [10](https://www.oracle.com/java/technologies/javase/10-relnote-issues.html): Tons of APIs for creating unmodifiable collections, such as List.of(). I find myself trying to use that one a lot. The biggest change though, is var, which is a way to declare a local variable with an inferred type. So instead of writing “String test = “test”;” you can write “var test = “test””.
* [11](https://www.oracle.com/java/technologies/javase/11-relnote-issues.html): Nice new String methods like isBlank(), simple List to Array conversion methods, and var support for lambdas.
* [12](https://www.oracle.com/java/technologies/javase/12-relnote-issues.html): A new String method, and some cool preview features which I’ll mention in later releases when they become standardized.
* [13](https://www.oracle.com/java/technologies/javase/13-relnote-issues.html): Nothing big or particularly interesting except for changes to preview features.
* [14](https://www.oracle.com/java/technologies/javase/14-relnote-issues.html): Switch expressions were made part of the standard after being in preview for the past two versions. They are awesome. I highly recommend reading about them here.
* [15](https://www.oracle.com/java/technologies/javase/15-relnote-issues.html): Helpful null pointer exceptions made the default, and Text Blocks were released. While I wish Text Blocks included string interpolation, this release does add a String method formatted which provides an easy way to do something similar.
* [16](https://www.oracle.com/java/technologies/javase/16-relnote-issues.html): This is a big one. Records become part of the standard, which are a way to make immutable classes without all the boilerplate. Similar to data classes in Kotlin. Additionally, instanceof pattern matching While this is a pretty niche enhancement, it proves that pattern matching is possible in Java and will hopefully lead to more advanced pattern matching in the future.
* ([17](https://openjdk.java.net/projects/jdk/17/)): Can’t say definitively what will be in this one, but we can take a pretty good guess. It’s likely we’ll see Sealed Classes, which are a way to specify which classes are allowed to extend a particular class. This enables all kinds of goodness, including compiler checks to make sure you don’t forget to handle particular subclasses, as well as preventing bad behavior resulting from users extending a class that was never intended to be extended by anything but internal classes. We might see foreign memory API, which should help libraries improve their code, and therefore, by extension, your code. We also might see the release of the Vector API, which probably won’t be too useful unless you do heavy numerical calculations.

In short, lots of great features! Nothing as big as you would get by switching to another JVM based language like Kotlin or Clojure, but still significant!
