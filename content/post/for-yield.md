+++
categories = ["intro"]
date = "2016-07-15T17:30:00+02:00"
title = "For + yield = for comprehension"
+++

# For loops and for comprehensions in Scala

Looping over a collection of items and transforming the individual elements 
within is quite a common task. So it seems natural that Scala offers a nice
way to solve this.

<!--more-->

If you know some other, more "traditional", imperative programming languages,
then you might have some assumptions about a thing that's name
begins with "for". 
These can be useful to understand Scala's _for_ capabilities, but you might
be surprised at how powerful Scala's solution is.

## Some simple examples 

As a warm-up, let's see a couple of short examples. 

They will use the Twitter-related case classes that were introduced
in a previous post,
<a href='{{< relref "post/lists.md" >}}'>Lists in Scala</a>.

{{< highlight scala >}}
  case class User(name: String)
  case class TweetMsg(id: Long, user: User, msg: String)
{{< / highlight >}}

### A for loop for printing

At first let's just create a list of three _TweetMsg_ objects and print
their message strings to the screen within a _for-loop_:

{{< highlight scala >}}
def createTweetList: List[TweetMsg] = {
  val user1 = new User("ador")
  val user2 = new User("szeli")
  val t1 = new TweetMsg(9243012L, user1, "scala program")
  val t2 = new TweetMsg(9534594L, user2, "ice cream")
  val t3 = new TweetMsg(9811235L, user1, "playing with scala")
  val tweetList: List[TweetMsg] = List(t1, t2 ,t3)
  tweetList
}

val tweets = createTweetList

for (tw <- tweets) {
  println(tw.msg)
}
{{< / highlight >}}

The last three lines contain the code to loop over all the tweet objects of the
list that we created previously. It's really just the _for_ keyword, plus a
so-called _generator expression_, that "pushes" the collections's elements
with the '<-' arrow into a temporary value (called _tw_ in our example),
that can be used within the loop's body (that is, within the curly braces)
to do something with it (we just printed the message part).

This first example, strictly speaking, is just a _for loop_,
not really a _for comprehension_ yet. 
To write a real comprehension, we'll need the _yield_ keyword.

### A real for-comprehension

In the previous example we looped over a list and printed something, based on
each element of the list.

Now we'll write a single line of code where we _transform_ the incoming list of 
_TweetMsg_ objects into a new list of _String_ objects by selecting
only the message part from the tweets.

{{< highlight scala >}}
val strMsgs = for (tw <- tweets) yield tw.msg
{{< / highlight >}}

Simple, huh? :)

One big advantage of this approach (_transforming_ the data instead of
doing some "side effects", like printing) is that we stay close to 
the functional programming paradgim, and this can have nice benefits 
in many cases.

## Advanced features

### Filtering

In the next example we go one step further: we filter the resulting String list
to only contain messages that include the word "scala". We can do this 
with the so-called _guards_, that are simply booelan expressions, added
to the for comprehension like here:

{{< highlight scala >}}
val filteredMessageList = for {
  tw <- tweets
  if tw.msg.contains("scala")
} yield tw.msg
{{< / highlight >}}


<!-- _Note:_ It's not necessary but good to know, that under the hood, 
the Scala compiler will translate the for loops and comprehensions into 
a series of _flatMap()_, _map()_ and _filter()_ calls to achieve the 
intended result. So the for structure is just a "syntactic sugar"
over these functions. We'll learn about each a bit later :)
-->



### Looping over more collections

Instead of ugly nested loops, Scala's for comprehensions allow us to process
elements from more than one collection simply by adding more
generator expressions to the _for_ (before the guard(s)).

For example, let's say that we have a list of words (Strings in a list
called _words_) and we want to filter our
long list of tweets (called _tweets_) so that only those 
tweet messages remain that include any of the pre-defined words:
{{< highlight scala >}}
for {
  tw <- tweets
  word <- words
  if tw.msg.contains(word)
} yield tw
{{< / highlight >}}


<!-- TODO : maybe in another post, this is a bit more complicated,
to find a simple and meaningful example with tweets

### Using for with Options

I can't go into details here about what Scala requires from a type in order
to be able to apply for comprehensions to its objects, but the good news is:
for comprehensions work on all the usual collection types (List, Set, Vector,
etc.) and also on Option! Why is this useful?, you may ask. 

Well, let's imagine that we need to fetch some data from a database.
Or, to keep our example simle, let's just use a Map. 

If you have read 
<a href='{{< relref "post/maps.md" >}}'>
this post about Maps</a>, then you already know that with Maps, we can not be 
sure that it contains something for a given key or not, so what we receive if 
we call a _get(key)_ method on a Map then the result will be an _Option_: 
either a _Some(value)_ or a _None_.

Scala helps us to deal with the situation when we can't know beforehand 
if we will have a _Some_ or a _None_ to deal with. 

Let's see:

{{< highlight scala >}}

for {
  tw <- tweets
  word <- words
  if tw.msg.contains(word)
} yield tw
{{< / highlight >}}
 -->  


## Summary and other sources

The nice thing about Scala's _for comprehension_ is that 
you don't need to understand all the details 
(you don't have to know what the _for_ is being transformed to under the hood; 
btw. it's a series of _map_, _flatMap_ and _filter_ calls) to efficiently 
use the power of it.

<!--"The for-expression is similar to loops in imerative languages,
except that it builds a list of the results of all iterations"
(martin ordersky's scala course on coursera) -->


Code examples are available
[here](https://github.com/ador/scala-examples/tree/master/07_for_yield).


_Note n+1_ : Feedback is welcome on [Twitter](https://twitter.com/adorster) 
or on [GitHub](https://github.com/hands-on-scala/hands-on-scala.github.io/issues/4) :)
<!-- TODO create issue -->






