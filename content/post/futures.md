+++
categories = ["intro", "patternmatching"]
date = "2016-10-24T17:30:00+02:00"
title = "Futures in Scala"

+++

# Not-yet-available values in Scala: Futures!

Whenever we want to use a value that is not readily available yet -- for example, when we 
call a function to compute or fetch something over the network --
we can not be sure if things go as were planned.
What if the database connection is down? What if the user typed in an invalid string?

<!--more-->

In the Java world, and in many other programming languages, the programmers could 
throw an exception (or just pass further the 
'classic' NullPointerException) in these cases to signal that the requested value cold not 
be served.

Maybe you have recognised: the above two introductory paragraphs are the 
same as those of <a href='{{< relref "post/options.md" >}}'>
my post on Options</a>, word by word. The reason is: these two types can be used
to handle similar use cases. But of course,  there are important differences as well.


## What does a Future know

Futures make it really easy to write multi-threaded applications.
We (usually) don't have to worry about threads, just pass around Futures to avoid
blocking of computations.

A Future can either be _completed_ or _not completed_. And after it became completed, it will 
remain completed forever (there is no way to revert it to be not completed again).

When a Future is compleded then it has two possible states: the computation was 
either _succesfully completed_ or it _failed_. 

Scala aids us in dealing with these cases in a readable and concise way.

## How to use Scala's Futures

Let's see a couple of examples of how we can use Futures in Scala to represent values that 
are not computed yet.

### Returning a Future

If your code computes something that takes a while, or is not sure to succeed,
just return a value of type _scala.util.Future_, that wraps the actual value type that
you intend to return to the caller:

{{< highlight scala >}}
def fetchTweetList: Future[List[TweetMsg]] = Future {
  val user1 = new User("ador")
  val user2 = new User("szeli")
  Thread.sleep(400)    // milliseconds
  val t1 = new TweetMsg(9243012L, user1, "scala program")
  Thread.sleep(600)
  val t2 = new TweetMsg(9534594L, user2, "ice cream")
  Thread.sleep(500)
  val t3 = new TweetMsg(9811235L, user1, "playing with scala")
  val tweetList: List[TweetMsg] = List(t1, t2 ,t3)
  tweetList
}
{{< / highlight >}}

In the example above, the _fetchTweetList_ function will take a fairly long time
(I inserted some _Thread.sleep_-s to simulate a long-running fetch over the network).

The list of tweets to be returned at the end is wrapped in a _Future{ }_ block.
This makes the code that calls this function to get a Future object as a return value very quickly, so
that the subsequent computation steps (lines of code) will not be blocked from running.
Essentially a fork happens in the execution of the code whenever a Future is involved.

Imports and a context for this code snippet can be 
found [here](https://github.com/ador/scala-examples/blob/master/08_futures/src/main/scala/futures/FutureExamples.scala). 
If you run the scala App (just say "sbt run") then you can check the order of lines that are printed to the console.

### Dealing with a Future object

What can we do if we receive a Future from a function? How do we deal with these forks of execution?

The simplest solution is to provide a "callback function" that 
will be called to process the outcome of the computation after the Future became completed:

{{< highlight scala >}}
fetchTweetList.onComplete {
  case Success(tweetList) => println("got my tweets, " + tweetList.length + " of them")
  case Failure(ex) => println("Something bad happened")
  case _ => "??" // we will never get here
}
{{< / highlight >}}

The code between the curly brackets will be run only after the _fetchTweetList_ function has finished running (in a separate thread) 
and returned its computed Future.
We are using Scala's 
<a href='{{< relref "post/patternmatch1.md" >}}'>pattern matching</a> to
un-wrap the result of the computation.

We will explore other ways to deal with Future object in some subsequent blog posts. Stay tuned!

## There is more!

This was a very short intro only, there is much more to learn about Scala's Future. 
I will write at least two more posts on this topic. 

Until I have time to write the next part, I recommend reading these:

- [Wiki page on Futures and Promises in general](https://en.wikipedia.org/wiki/Futures_and_promises)
- [Daniel's post on Scala Futures](http://danielwestheide.com/blog/2013/01/09/the-neophytes-guide-to-scala-part-8-welcome-to-the-future.html)
- [The official documentation](http://docs.scala-lang.org/overviews/core/futures.html)

Some runnable code examples are available (and will be extended) [here](https://github.com/ador/scala-examples/tree/master/08_futures).

_Note n+1_ : Feedback is welcome on [Twitter](https://twitter.com/adorster) :)

