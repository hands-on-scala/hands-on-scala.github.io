+++
categories = ["intro"]
date = "2016-06-16T17:30:00+02:00"
title = "Scala collections - part 3"

+++

# Basic data structures in Scala: Maps

After _Lists_ and _tuples_, let's have a look at _Maps_. 

They are sometimes called "hashtables", "hashes", or "dictionaries" in other programming languages.

Maps are a bit more complex than what we've seen before. They come handy 
when you need to store associated pairs of data, or when 
you need to easily look up a value corresponding to another value (which we will call the _key_).

It does matter (as with Lists) what kind of objects you want to store as _keys_ and as _values_.
You can pick a type for each.


## Creating a Map

Scala offers a simple syntax to create an immutable Map filled with some key-value pairs:

{{< highlight scala >}}
val tweetMap = Map(
      414 -> "#scaladays are coming to Berlin!",
      435 -> "Scala is the new golden child", 
      506 -> "#scaladays Scaladex: scala package index")
    
val justAMap = Map(11 -> "hello", 13 -> 3.56)

val notValidMap: Map[Int, Double] = Map(63 -> 6.3, 19 -> "hello")

val emptyMap = Map()
{{< / highlight >}}
As usual, Scala will infer the type of the maps, if those are not defined. The inferred type
will be "Map[Int, String]" in _tweetMap_'s case, 
and "Map[Int, Any]" in the second example, called _justAMap_.

The third example above will give an "_error: type mismatch_", 
because we specified that we want to stores Ints
and Doubles in the map, but we tried to stuff in a String as a value.
Scala doesn't let that happen.

## Looking up a value for a key

If you are coming from the Java world, your instinct might tell you to call a _get(key)_ function
on the map to access the corresponding value. It works, but probably in a bit different way than 
you would expect.

{{< highlight scala >}}
tweetMap.get(414)
// will return:
// Some("#scaladays are coming to Berlin!")
{{< / highlight >}}

The _get(key)_ function returns an _Option_ which is a special type, that I will explain in 
the next post.

For now, let's use another, simpler way to access the value that belongs to a key:
{{< highlight scala >}}
tweetMap(414)
// will return the String:
// "#scaladays are coming to Berlin!"
{{< / highlight >}}
Nice, isn't it? One downside of this method is that we will get a "key not found" error,
more precisely, a "NoSuchElementException" if we try to query a key that is not in our map.

## Using mutable Maps

Until now we had maps that were immutable. Because Scala, by default, imports
"scala.collection.immutable.Map" as "Map".

But if we want to extend, or otherwise modify the contents of a map, we will need a mutable Map.
And we have to import it by:

{{< highlight scala >}}
import scala.collection.mutable.Map
{{< / highlight >}}
After this import, a "Map" will mean a mutable map, insted of an immutable map.
 
If you want to use both kinds of maps, then you can import both, and give them your own names like this:
{{< highlight scala >}}
import scala.collection.immutable.{Map => ImmuMap}
import scala.collection.mutable.{Map => MuMap}
 
val todoMap: MuMap[Int, String] = MuMap()
todoMap += (1 -> "think")
todoMap += (2 -> "write")
todoMap += (3 -> "publish")

{{< / highlight >}}

In the example above we created a MuMap, which was empty at first, but then we added three pairs
using the "+=" operator and specifying the key-value pairs (those were separated by simple arrows: "->").


## Iterating over all elements of a Map

For this we can either use an _iterator_:

{{< highlight scala >}}
val mIter = todoMap.iterator
while (mIter.hasNext) { println(mIter.next) }
{{< / highlight >}}

This will print the tuples:

{{< highlight scala >}}
(2,write)
(1,think)
(3,publish)
{{< / highlight >}}

Or, we could use the _foreach_ method of the Map:

{{< highlight scala >}}
todoMap.foreach(kv => println("key: " + kv._1 + ", value: " + kv._2))
{{< / highlight >}}

To see this output:
{{< highlight scala >}}
key: 2, value: write
key: 1, value: think
key: 3, value: publish
{{< / highlight >}}


## Summary and other sources

[This page](http://www.tutorialspoint.com/scala/scala_maps.htm) of TutorialsPoint lists more operations on Scala Maps.

Scala offers more Map implementations, with different trade-offs regarding mutability, speed of operations, ordering, etc. 
If you need advice on which one to choose, 
[this guide](http://alvinalexander.com/scala/how-to-choose-map-implementation-class-sorted-scala-cookbook)
might help.

Some runnable code examples are [here](https://github.com/ador/scala-examples/tree/master/05_maps).

Next time I'll briefly cover Scala's special collection-like tool: _Option_.

_Note:_ If you want to learn about Scala's "map()" function, with which you can simply apply a 
function on each element of a list, then you have to wait for a yet-to-come post. Alternatively,
read [this](http://www.brunton-spall.co.uk/post/2011/12/02/map-map-and-flatmap-in-scala/).


_Note n+1_ : Feedback is welcome on [Twitter](https://twitter.com/adorster) 
or on [GitHub](https://github.com/hands-on-scala/hands-on-scala.github.io/issues/2) :)
