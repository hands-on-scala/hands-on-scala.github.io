+++
categories = ["intro"]
date = "2016-07-15T17:30:00+02:00"
title = "For + yield = for-comprehension"

+++

# For-comprehensions in Scala

Looping over a collection of items and transforming the individual elements within 
is quite a common task. So it seems natural that Scala offers a nice way to solve this.

If you know some other, more "traditional", imperative programming languages, then you might have some 
assumptions about a thing that's name begins with "for". These might be useful to understand Scala's _for_ capabilities,
but you might be surprised at how powerful Scala's solution is.

## Some simple examples 

As a warm-up, let's see a couple of short examples. 

They will use the Twitter-related case classes that were used in a prevoius post
<a href='{{< relref "post/lists.md" >}}'>Lists in Scala</a>.

{{< highlight scala >}}
  case class User(name: String)
  case class TweetMsg(id: Long, user: User, msg: String)
{{< / highlight >}}

At first let's just create a list of 3 _TweetMsg_ objects and print their message strings
within a _for-comprehension_:

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

The last three lines contain the code to loop over all the tweet objects of the list that we created previously.
It's really just the _for_ keyword, plus "pushing" the collections's elements with the '<-' arrow into a temporary
value, called _tw_ in our example,
that can be used within the loop's body (that is, within the curly braces).

### Filtering

TODO

## Summary and other sources


"The for-expression is similar to loops in imerative languages, except that it builds a list of the results of all iterations"

(martin ordersky's scala course on coursera)

// side effects(imp ) vs building a new list! (scala)



Some runnable code examples are available [here](https://github.com/ador/scala-examples/tree/master/07_for_yield).


_Note n+1_ : Feedback is welcome on [Twitter](https://twitter.com/adorster) 
or on [GitHub](https://github.com/hands-on-scala/hands-on-scala.github.io/issues/4) :)
<!-- TODO create issue -->
