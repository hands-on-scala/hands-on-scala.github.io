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
have a List that keeps things of different types. 

So, the types from the above code snippet will be:
{{< highlight scala >}}
myIntList:  List[Int]
myStrList:  List[String]
myNumList:  List[Double]
myAnyList:  List[Any]
{{< / highlight >}}


Note that if you dont't specify the type of your list,
then the Scala engine (interpreter or compiler) will  infer the type for you. It will search the closest
common ancestor type of the elements of the list, and assign that as the type of the list.
( We'll learn more about the Scala type hierarchy later.)


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

We can concatenate two existing lists with the _concat_ method of _List_, or with the triple cons operator:

{{< highlight scala >}}
val list1 = List(1,2,3)
val list2 = List(4,5,6)
val all1 = List.concat(list1, list2)
val all2 = list1:::list2   // will be the same as 'all1'
{{< / highlight >}}

And this is how you mimic appending a new element at the end of an immutable list: you create a new list, 
which is a concatenation of the original and a new list with only one element:

{{< highlight scala >}}
val list3 = List(1,2,3,4)
val extendedList = list3:::List(5)
{{< / highlight >}}

## Basic operations on Lists

I'll just show a handful of basic functions: how to get the _length_ of a list, that is, the number of its elements; and how to 
check if it's empty, or if it contains an element, and at which position.

{{< highlight scala >}}
val list4 = List(1,2,3,4)
println(list4.length)   // prints '4'
println(list4.isEmpty)  // prints 'false'
val fromPosition = 0
println(list4.indexOf(2, fromPosition))   // prints '1'
{{< / highlight >}}

## Other operations on Lists

These built-in functions highlight some very useful capabilities of lists in Scala. 
I won't explain them one by one, because their names are quite descriptive; but lets's see the examples
as part of a runnable App.
I insert a bit longer code snippet, but I hope it's easy to follow.

{{< highlight scala >}}
object ListExamples extends App {

  case class User(name: String)
  case class TweetMsg(id: Long, user: User, msg: String)

  def isIdPositive(tw: TweetMsg) : Boolean = {
    return (tw.id > 0L)
  }
  
  def printUserAndMsg(tw: TweetMsg) : Unit = {
    println(tw.user + " tweeted: " + tw.msg)
  }
  
  override def main(args: Array[String]): Unit = {
    val user1 = new User("adri")
    val user2 = new User("adorster")
    val user3 = new User("stern")
    val t1 = new TweetMsg(94432L, user1, "hello data")
    val t2 = new TweetMsg(513454L, user2, "hello science")
    val t3 = new TweetMsg(-68435L, user3, "hello data science")

    val tweetList1: List[TweetMsg] = List(t1, t2 ,t3) 

    // filter
    val filteredList = tweetList1.filter(isIdPositive)
    println("Filtered list is: " + filteredList)  

    // forall
    val trueOfFalse1 = tweetList1.forall(isIdPositive)
    println("All id numbers positive? " +  trueOfFalse1)
    val trueOfFalse2 = List(t1,t2).forall(isIdPositive)
    println("All id numbers positive? " +  trueOfFalse2)
    
    // foreach
    tweetList1.foreach(printUserAndMsg)

    // intersect
    val tweetList2: List[TweetMsg] = List(t3, t2) 
    val intersectList = tweetList1.intersect(tweetList2)
    println("Intersected list is: " + intersectList)

    // distinct
    val tweetList3: List[TweetMsg] = List(t3, t2, t2, t3, t1, t3, t2) 
    val distinctList = tweetList3.distinct
    println("Distinct list is: " + distinctList)
  }
}

{{< / highlight >}}

More operations are listed [here](http://www.tutorialspoint.com/scala/scala_lists.htm).

If you want  to play with the code examples above, you can clone my git repo from [GitHub](https://github.com/ador/scala-examples/tree/master/03_lists).


## Summary and what's coming next

In the next post we'll cover tuples.

If you're very impatient, check out [collections in Twitter's Scala School](https://twitter.github.io/scala_school/collections.html)

If you are curious about the more advanced topic of the _performance_ characteristics of these types, 
[see a summary here](http://docs.scala-lang.org/overviews/collections/performance-characteristics.html).


_Note n+1_ : Until I set up a comments section somehow here, feedback is welcome via [Twitter](https://twitter.com/adorster) :)
