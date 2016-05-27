+++
categories = ["intro"]
date = "2016-05-27T17:30:00+02:00"
title = "Scala collections - part 1"

+++

# Basic data structures in Scala: Lists

In the following couple of posts we'll learn about basic data structures,
and how they can be used in Scala.

_Lists_ are what their name suggests: they can keep a list of things. The order
of its elements will be kept,
and a list does not care if an element appears more than once in it.

## Creating (immutable) lists

As it can be rad in the [Scala collections overview](http://docs.scala-lang.org/overviews/collections/overview.html),
collections in Scala can either be mutable or immutable. The default is the 
immutable version, so when we say "List" or "scala.List" it will be traslated to "scala.collection.immutable.List". 

{{< highlight scala >}}
val myIntList = List(2, 324, 6, -2, 0, 45, 0)
val myStrList = List("Hello ", "Scala", "!")
val myNumList = List(5, 0.727, 61)
val myAnyList = List(7, "Hi", -42.9, 0, 38)
{{< / highlight >}}

As you can see in the third line from above, Scala allows you to 
have a List that keeps thigs of different types. 

So, the types from the above code snippet will be:
{{< highlight scala >}}
myIntList:  List[Int]
myStrList:  List[String]
myNumList:  List[Double]
myAnyList:  List[Any]
{{< / highlight >}}


<!--Actually, if you dont't specify the type of your list,
then the Scala engine (interpreter or compiler) will  infer the type for you. It will search the closest
common ancestor type of the elements of the list, and assign that as the type of the list. --> 
<!-- We'll learn more about the Scala type hierarchy later. -->


Another approach to creating lists is using the Lisp-style _cons_ operator, "::" that concatenates elements to a list,
and at the end you need to close the list with a "Nil" value.
{{< highlight scala >}}
val anotherIntList1 = 1 :: 2 :: 3 :: Nil
val anotherIntList2 = (1, 2, 3)
{{< / highlight >}}

The above two lines will created equivalent lists, that have the same elements.

### Specifying the type of the list

If you would like to direcly specify the type of your list (restrict the type of the elements it will be able to hold), you can do it as well:

{{< highlight scala >}}
val myIntList1: List[Int] = List(2, 5, 2)
val myIntList2: List[Int] = List(-6, 4.54)
{{< / highlight >}}

The creation of "myIntList2" will fail with a  _"type mismatch" error_, because we tried to put a Double
value into a List of integers, and it simply does not fit there.

## Concatenation and appending elements 

The lists we created above are _immutable_, you can not change them.

If you want to extend a list, there are operations for that, but what 
will happen under the hood is that you will be given a completely new list with the extended contents and the original
list will remain intact. This might be important when dealing with long lists and where efficiency is important.

_TODO: extend this section !_


## Other operations on Lists

I'll just show a handful of basic functions: how to get the _length_ of a list, that is, the number of its elements; and how to 
check if it contains an element, and at which position.

_TODO: extend this section !_

More operations are listed [here](www.tutorialspoint.com/scala/scala_lists.htm).


## Summary and what's coming next

In the next post we'll cover tuples and sets.

If you're very impatient, check out [collections in Twitter's Scala School](https://twitter.github.io/scala_school/collections.html)

If you are curious about the more advanced topic of the _performance_ characteristics of these types, 
[see a summary here](http://docs.scala-lang.org/overviews/collections/performance-characteristics.html).


_Note n+1_ : Until I set up a comments section somehow here, feedback is welcome via [Twitter](https://twitter.com/adorster) :)
