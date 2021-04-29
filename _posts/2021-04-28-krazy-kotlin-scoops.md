---
title: Krazy Kotlin Scoops
published:true
---

Welcome back to Krazy Kotlin Scoops. Today we're going to talk about Kotlin's type safe builders.

Most commonly, Kotlin's type-safe builders are used as part of DSLs or Domain Specific Languages. For instance, if one wanted to write an HTML page using Kotlin, you can do that with [kotlinx.html](https://github.com/Kotlin/kotlinx.html)! Or you can set up routes in a fluent manner using [Ktor](https://ktor.io/)! However, you can also utilize this builder pattern for yourself as an alternative to Java style builders. Let's start with an example of a Java style builder:

```java
public class Dog {
    private String name;
    private String breed;
    private int legs;
    private int ears;

    public static Builder builder() {
        return new Builder();
    }

    /* Getters for instance variables */

    public static class Builder {
        private final Dog dog;
        private Builder() {
            dog = new Dog();
        }

        public Builder setName(String name) {
            dog.name = name;
            return this;
        }

        public Builder setBreed(String breed) {
            dog.breed = breed;
            return this;
        }

        public Builder setLegs(int legs) {
            dog.legs = legs;
            return this;
        }

        public Builder setEars(int ears) {
            dog.ears = ears;
            return this;
        }

        public Dog build() {
            return dog;
        }
    }
}
```

and then we would use it like so

```java
public class Main {

    public static void main(String[] args) {
        Dog punHusky = Dog.builder()
                .setBreed("Husky")
                .setName("Pun Husky")
                .setEars(2)
                .setLegs(4)
                .build();
        petDog(punHusky)
    }
}
```

Verbose, but fluent and immutable. In Kotlin we would do this a little differently.

We can often forgo builders entirely in Kotlin by making use of [named](https://kotlinlang.org/docs/functions.html#named-arguments) and [default](https://kotlinlang.org/docs/functions.html#default-arguments) arguments. For instance, if you use a data class (like a normal class, but generates some default methods for you), that comes with a method `copy` for free, already generated for you. It's a common pattern when using Immutable objects to have to have methods like `withEars(newEars)` to create an exact copy of the object the method is called on, except with one value changed. But what if you wanted to change ears and legs? You would either have to create a method that took two parameters, or call two methods one after another, which would actually create an extra object that you would never even use. `copy` does this all easily and for free with data classes. Instead of calling `dog.withEars(newEars).withLegs(newLegs)` you can simply call `dog.copy(legs = newLegs, ears = newEars)`. About the same length of code, but with only one method and no extraneous object creation. Using the copy method or similar, you can often avoid builders in the first place.

What about when you really can't or the times when named and default parameters just really don't fit your needs? Well, Kotlin has type-safe builders for that. Consider the following Kotlin file:

```kotlin
fun dog(init: Dog.Builder.() -> Unit): Dog = Dog.dog(init)

class Dog private constructor(val name: String, val breed: String, val legs: Int, val ears: Int) {
    private constructor(builder: Builder) : this (builder.name, builder.breed, builder.legs, builder.ears)

    companion object {
        fun dog(init: Dog.Builder.() -> Unit): Dog {
          val builder = Dog.Builder()
          builder.init()
          return Dog(builder)
        }
    }

    class Builder {
        var name: String = "Fido"
        var breed: String = "Pomeranian"
        var legs: Int = 4
        var ears: Int = 2
    }
}
```

Here we have a `Dog` class with a private primary constructor, a private secondary constructor that takes a builder, as well as an inner class `Builder`, a function called `dog`, and a private constructor. There are a couple of options for where to put the `dog` function, you can also have it as a top level function (outside of a class). Here we have it as a member of a `companion object` (similar to marking it `static` in java). The main benefit of this is that you can mark the `Dog` constructors private to ensure Dogs are only constructed using the builder method. In order to make it a bit easier to use, we also provide a top level function that just delegates to the companion object's implementation. This is how you would use it:

```kotlin
// no imports needed as long as top level function "dog" is in the same module
fun main() {
    val doge = dog { // this: Dog.Builder
        name = "Doge" // implicit this.name
        breed = "Shiba Inu"
        val dogeLegs = numberOfDogeLegs() // this block is just a lambda, we can write regular code inside
        legs = dogeLegs
        // defaults are fine for ears
    }
    petDog(doge)
}
```

How does this work? Well, first note that `dog` is a function. The `function {}` syntax is the standard in kotlin when function takes a function as an argument (or if it ends with a function argument `function(otherArg) {}`). `{}` designates a lambda in Kotlin. So, `dog` is a function that takes a function. But not just any function, an `extension function`. An extension function is a function that acts as if it were a method on the object it is extending, but in fact only has access to members of that object according to where the function was declared relative to the object's class, just like a regular function. So the `dog` function takes a function `init` that extends `Dog.Builder`, creates a dog builder, then calls init on the builder it just created, then returns a new Dog created from this builder. `this` within init refers to the `Dog.Builder` object, since it acts like a method on `Dog.Builder`.
