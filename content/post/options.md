+++
categories = ["intro"]
date = "2016-06-16T17:30:00+02:00"
title = "Options in Scala"

+++

# Handling missing values in Scala: Options

Whenever we want to use a value that is not readily available yet -- for example, when we 
call a function to compute or fetch something --
we can not be sure if things go as were planned.
What if the database connection is down? What if the user typed in an invalid string?

In the Java world, and in many other programming languages, the programmrs could 
throw an exception (or just pass further the 
'classic' NullPointerException) in these cases to signal that the requested value cold not 
be served.

But oftentimes,
using exceptions for such cases is an overkill, and only adds noise to the code.
It can even happen, that it is completely 'normal' that a function can not return 
a proper value for some reason.

## Returning something or nothing

Scala has a built-in type to help us in the situation when we are not sure that 
we can return a value: the _Option[T]_ type. The _T_ parameter means that it takes a type
inside it as well, and it will be type-safe to use.

You can think about an Option as a container that either holds a value of type _T_, or not.
If the Option is empty, it is called _None_, and if it has a value inside, then it
is an object of the class _Some[T]_.

## How to use Options

Let's see a couple of examples of how we can use Options in Scala to represent optional values.

### Returning an Option from our function

{{< highlight scala >}}
val userMap = Map(
    824 -> "Jane",
    2723 -> "Kate",
    535 -> "Zoe",
    8260 -> "Jonathan"
)

def getUserById(id: Int): Option[String] = {
  userMap.get(id)   // Map's buil-in get() returns an Option
}

println("535: " + getUserById(535))
println("538: " + getUserById(535))
{{< / highlight >}}

As you might remember, 
<a href='{{< relref "post/maps.md" >}}'>
in our previous post, about Maps in Scala</a>,  
the _get(key)_ function of a map will return an Option, which will hold the
 value corresponding to the key if the key is present in the Map. And what hppens in case of
an invalid key? If we run the above code, we will see this result:

{{< highlight scala >}}
Some(Zoe)
None
{{< / highlight >}}

So, the String value itself is wrapped with "Some()" in the first case, and we simply
got a "None" result in the second case, when we used a nonexisting id.

### Dealing with an Option

What to do when we, as a caller, receive an Option?
<!--case class TweetMsg(id: Long, user: User, msg: String,  hashtags: Option[List[String]])
case class User(userId: Int, name: String, email: Option[String]) -->

{{< highlight scala >}}
TODO
{{< / highlight >}}


## Summary and other sources

By using Options we - as developers of a certain functionality - can clearly signal that
a function might return with no real result, and Scala also helps the caller in these cases
to deal with the situation: with pattern matching.

[Daniel's post on Options](http://danielwestheide.com/blog/2012/12/19/the-neophytes-guide-to-scala-part-5-the-option-type.html) goes into more details, it's really worth reading.

Some runnable code examples WILL BE are [here](https://github.com/ador/scala-examples/tree/master/06_options).


_Note n+1_ : Feedback is welcome on [Twitter](https://twitter.com/adorster) 
or on [GitHub](https://github.com/hands-on-scala/hands-on-scala.github.io/issues/2) :)
