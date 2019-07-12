---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - scala
  - java

toc_footers:
  - <a href='https://github.com/JasonNeo/'>Made by Jason Neo</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - cheatsheet

search: true
---

<aside class="warning">
This is a work-in-progress, if you'd like to contribute let me know!
</aside>

# Introduction

Welcome to the Java To Scala! This is aimed at Java developers who are new to the Scala programming language.

Each section contains code examples for both Scala and Java! You can view the code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Variables & Values

Scala has two types of variables: 1. Values and 2. variables. A value variable is really just a constant, meaning once assigned, you cannot change its value (immutable). A regular variable on the other hand, is mutable, meaning you can change its value (reassigning).

When you assign an initial value to a variable, the Scala compiler can automatically figure out the `type` of the varible based on the value assigned to it. This is called **type inference**.
> Variables & Values

```scala
var myVar : Int = 0;
val myVal : Int = 1;

myVal = 3 // Reassignment to val gives you an error
```

If, however, you did not assign an initial value to the variable, the compiler cannot figure out what type it is. Therefore, you have to explicitly specify the type if you do not assign an initial value to the variable. Here is how it looks: 

```scala
var myVar :Int;
val myVal :Int;
```

# Functions
Functions are expressions that take parameters. They can be assigned to an object `(val/var)` to be reused.

> Functions

```scala
val addOne = (x: Int) => x + 1
println(addOne(1)) // 2
```

# Methods
Methods look and behave very similar to functions, but there are a few key differences between them.

Methods are defined with the def keyword. def is followed by a name, parameter lists, a return type, and a body.

`def methodName ([list of parameters]) : [return type]`

> Methods

```scala
def ellipse(original: String, maxLength: Int) : String = {
    return "Not implemented yet";
}
```

In Scala, the compiler can automatically infer the return type from what is being returned. However, it can’t infer the types of the parameters so we’ll have to leave those explicit specifications in.

> Automatically infer return type

```scala
def ellipse(original: String, maxLength: Int) = {
    return "Not implemented yet";
}
```

If we don’t use the return statement, the compiler will just assume that we want to return the value of the last statement. However, if we want to return from the middle of a method the `return` keyword is needed.

> Automatically infer return statement

```scala
def ellipse(original: String, maxLength: Int) = {
    "Not implemented yet";
}
```

To know more about Scala methods, click [here] (http://joelabrahamsson.com/learning-scala-part-five-methods/).

# Arrays #

In Scala arrays are immutable objects. You create an array like this: 

**Instantiation & Initialization**

`var myArray : Array[String] = new Array[String](10);`

**Accessing Array Elements**

`var aString : String = myArray(0);`

**Assignment**

`myArray(0) = "some value";`

# If/Else Statements

 The Scala if command executes a certain block of code, if a certain condition is true. Here is an example:

> If/Else Statements

```scala
var myInt : Int = 0;
if(myInt == 0) {
  println("myInt equals to 0!");
}
```

<aside class="notice">
Omitting { } in if - statements
Like in Java it is possible to omit the {} in an if-statement around the code to execute, if the code consists of a single line.
</aside>

> Omitting {}

```scala
var myInt : Int = 1;
if(myInt == 0)
  println("myInt == 0");
 else
  println("myInt != 0");
```

# Loops

## While Loops ##

> While Loops

```scala
var input = ""
while(input != "exit")
    input = readLine();
```

## Do-While Loop ##

> Do-While Loop

```scala
var input = "exit"
do {
    input = readLine();
    } while(input != "exit")
```

## For Loops ##
The for loop in Scala is referred to as “for comprehension” or “for expression” in the Scala community and it can do some pretty funky stuff. Let’s begin by creating a simple Person class and a list of Person instances:

> For Loops

```scala
class Person(val name: String, val female: Boolean)

val people = List(
    new Person("Cliff Barnes", false),
    new Person("J. R. Ewing", false),
    new Person("Sue Ellen Ewing", true))
```

We can traverse the list, “comprehending” each instance using a for loop that syntactically is very similar to Java’s.

```scala
for(person <- people)
    println(person.name)
```

```java
for(Person person : people)
    System.out.println(person.name);
```

As we can see the for loop is very similar to Java’s, except it doesn’t require us to specify the type of the temporary variable as the compiler can infer it and the : operator is replaced with the <- operator. The <- operator is called a generator and a Scala for expression must always start with a generator which specifies which collection of objects to iterate over and a temporary variable that holds the current object.

### Filtering ###
Let’s say that we only want to print the names of the women in the collection. We can add a filter for that.

> Filtering

```scala
for(person: Person <- people
    if person.female)
    println(person.name)
```

### Yielding ###

Using the yield keyword we can use for expressions to create new collections. The code on the right creates a new collection named `names` containing all of the names of the people in the collection of `Persons`.

> Yielding

```scala
val names = for(person <- people) yield person.name
for(name <- names) println(name)
```

# Classes #

Scala classes are very much like Java classes, with some differences mainly in how we declare constructors.

> Declaration and Instantiation

```scala
class Greeter {
  def SayHi() = println("Hello world!")
}

var greeter = new Greeter()
greeter.SayHi() // "Hello world!"
```

## Class Constructors ##

### Primary Constructors ###
In Scala the primary constructor is the class’ body and it’s parameter list comes right after the class name.

> Primary Constructors

```scala
class Greeter(message: String) {
    def SayHi() = println(message)
}

val greeter = new Greeter("Hello world!")
greeter.SayHi() // "Hello world!"
```

The compiler automatically creates a field for us. By default, the field is set as val (immutable) and it’s access is public.

### Auxiliary Constructors ###
We are free to add as many additional auxiliary constructors as we want. However, an auxiliary constructor must be on the first line of it’s body, and call either another auxiliary constructor that has been declared before it or the primary constructor.

`this()`

> Auxiliary Constructors

```scala
class Greeter(message: String, secondaryMessage: String) {
    def this(message: String) = this(message, "") // Auxiliary Constructor
    
    def SayHi() = println(message + secondaryMessage)
}
```

## Abstract Classes ##

An abstract class can have abstract methods and non-abstract methods as well. Abstract class is used to achieve abstraction. Abstraction is a process in which we hide complex implementation details and show only functionality to the user.

> Abstract Classes

```scala
abstract class Greeter {
    val message: String
    def SayHi() = println(message)
}

class SwedishGreeter extends Greeter{
    message = "Hej världen!"
}

val greeter = new SwedishGreeter()
greeter.SayHi()
```

## Case Classes ##
Scala has a special type of class called a “case” class. By default, case classes are immutable and compared by value.

`case class Point(x: Int, y: Int)`

You can instantiate case classes without new keyword.

`val point = Point(1, 2)`

To learn more on Scala case class, click [here] (https://www.alessandrolacava.com/blog/scala-case-classes-in-depth/)

## Objects ##
Objects are single instances of their own definitions. Also known as singleton objects.

> Objects

```scala
object IdFactory {
  private var counter = 0
  def create(): Int = {
    counter += 1
    counter
  }
}
```

You can access an object by referring to its name.

```scala
val newId: Int = IdFactory.create()
println(newId) // 1
val newerId: Int = IdFactory.create()
println(newerId) // 2
```

## Traits ##
Traits are used to share interfaces and fields between classes. They are similar to Java 8’s interfaces. Classes and objects can extend traits but traits cannot be instantiated and therefore have no parameters.

An awesome [post](http://joelabrahamsson.com/learning-scala-part-seven-traits/) by Joel Abrahamsson describes the importance of traits.

### Defining a trait ###
A minimal trait is simply the keyword trait and an identifier:

> Traits

```scala
trait HairColor
```

### Using traits ###
Use the `extends` keyword to extend a trait. Then implement any abstract members of the trait using the `override` keyword.

> Using traits

```scala
trait Iterator[A] {
  def hasNext: Boolean
  def next(): A
}

class IntIterator(to: Int) extends Iterator[Int] {
  private var current = 0
  override def hasNext: Boolean = current < to
  override def next(): Int = {
    if (hasNext) {
      val t = current
      current += 1
      t
    } else 0
  }
}


val iterator = new IntIterator(10)
iterator.next()  // returns 0
iterator.next()  // returns 1
```

# Collections

# ScalaFX #

# Additional Resources #

1. http://tutorials.jenkov.com/scala/index.html
2. https://docs.scala-lang.org/

# Credits #

Icons made by [photo3idea_studio] (https://www.flaticon.com/authors/photo3idea-studio) from [www.flaticon.com] (https://www.flaticon.com/) is licensed by [CC 3.0 BY] (http://creativecommons.org/licenses/by/3.0/)