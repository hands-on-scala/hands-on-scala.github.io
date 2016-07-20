+++
categories = ["intro"]
date = "2016-06-08T17:30:00+02:00"
title = "Scala collections - part 2"

+++

# Basic data structures in Scala: Tuples

In the previous post we learned about <a href='{{< relref "post/lists.md" >}}'>Lists in Scala</a>. Now I'll briefly cover _tuples_.

You can think about a tuple as simple "wrapper" around a handful of things,
it just keeps its elements together, at their own place.

<!--more-->

Tuples are similar to lists in some ways, but there are also some key differences.

It is also worth noting that strictly speaking, a tuple is not a _Scala collection_, because
it's not one of the classes that implement the necessary functionality to be called a real collection.

## What are they good for?

So why is it handy that we can wrap a couple of things together? 

Well, if you are a Java developer then you probably know how annoying
it is when you have to create a custom new class just to be able to
return more than one value that have been computed together within a method.

Tuples provide a very ligth-weight tool to pass around a small group
of values together.

## Creating tuples

Let's see two quick examples: 
{{< highlight scala >}}
val myFirstTuple = (-2, 8, 13)
val result:Double = 42.0
val mySecondTuple = (result, "Hello", '!', "Scala")
{{< / highlight >}}

Creating a tuple is as easy as listing its elements, separated by commas, 
and wrap all this in parentheses.
No special keyword is needed.

As _Lists_, tuples also keep the order of their elements, and duplicates among the elements are allowed.

Tuples are always _immutable_, there's no way to change their elements.

### First difference from List: types of elements

As you may remember, Lists were used to hold elements of the same type. It might not be obvious,
because of Scala's smart automatic type inference, but if you put all kinds of things into a List, like here: 
{{< highlight scala >}}
val myList = List(-2, 48, "hello")
{{< / highlight >}}
then the "myList" will be of type _List[Any]_ (because _Any_ is the "mother-of-all" type in Scala; as is _Object_ in Java).
So, from this point of view, this "myList" still contains elements of the same type!

On the other hand, tuples were designed to hold different types of objects.
The type description of "mySecondTuple" from the first example, will be:

{{< highlight scala >}}
(Double, String, Char, String)
{{< / highlight >}}

### Second difference from Lists: allowed length

List could be of any length. But there is an upper limit for the number of elements in a tuple: it's 22. (Don't ask me why.)

Trying to create a tuple with 23 or more elements will lead to an error. But 22 items is well enough.

### Third difference from Lists: indexing

Lists (and usually all kinds of collections) index their elements starting from zero. 
But tuples are different: their elements are indexed from one. 

The syntax is also a bit weird, you need a dot plus an underscore between the tuple and the index.

Some examples of referencing tuple elements:

{{< highlight scala >}}
val tupleTweet = ("johhnny", 531523L, "Hello, Mom!")
val username = tupleTweet._1
val id = tupleTweet._2
println(username + ": " + tupleTweet._3 )
// johhnny: Hello, Mom!
{{< / highlight >}}

## Smart usage

Let's say we have a function that returns three values in a tuple: 

{{< highlight scala >}}
def getTweetData(id: Long):(String, Int, String) = {
  // should get data from database,
  // instead a dummy solution
  if (id == 5) {
    ("angie", 30, "It's my birthday!")
  }
  if (id == 7) {
    ("tony", 11, "Rainbows! :)")
  }
  ("zoe", 13, "More rainbows! :)")
}
{{< / highlight >}}

And then, where we call this function, we want to give the elements from the tuple separate value names.

The first solution that we may think of is with using indices, but it's quite clumsy. Instead,
we can simply list the desired variable names on the left side of the assingment operator, like in this example: 

{{< highlight scala >}}
val(name, age, msg) = getTweetData(8)
println("Name is: " + name + ", age:" + age)
{{< / highlight >}}

Moreover, if you don't care about some values (for example, the age is not important), then you can use 
a wildcard operator, an underscore (again) in its place:

{{< highlight scala >}}
val(name, _, msg) = getTweetData(8)
println("Name is: " + name + ", message is: " + msg)
{{< / highlight >}}

Then you'll get only two new values after the assignment in the first line, instead of three.


You can find more examples on [TutorialsPoint](http://www.tutorialspoint.com/scala/scala_tuples.htm) 
and in [Alvin Alexandes's blog](http://alvinalexander.com/scala/scala-tuple-examples-syntax).

_Note n+1_ : Until I set up a comments section somehow here, feedback is welcome via [Twitter](https://twitter.com/adorster) :)




