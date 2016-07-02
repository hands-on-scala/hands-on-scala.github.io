+++
categories = ["intro"]
date = "2016-07-02T17:30:00+02:00"
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

The following "getUserById()" function returns an Option 
(about Maps, see 
<a href='{{< relref "post/maps.md" >}}'>
the previous post</a>):

{{< highlight scala >}}
def getUserMap: Map[Int, String] = {
  val userMap: Map[Int, String] = Map(
    824 -> "Jane",
    2723 -> "Kate",
    535 -> "Zoe",
    8260 -> "Jonathan")
  userMap
}

def getUserById(id: Int): Option[String] = {
  val users = getUserMap
  //  Note: we could have just used 
  //  Map's buil-in get() method that returns an Option:
  // users.get(id) 
  if (users.contains(id)) { 
    Some(users(id)) 
  } else {
    None
  }
}

println("535: " + getUserById(535))
println("550: " + getUserById(550))
{{< / highlight >}}


The last two lines will print:

{{< highlight scala >}}
535: Some(Zoe)
538: None
{{< / highlight >}}

So, the String value "Zoe" itself is wrapped in "Some()" in the first case, and we simply
got a "None" result in the second case, when we used a non-existing id.

### Dealing with an Option

What can we do if we receive an Option from somewhere?

Scala offers many possibilities to handle Options, here I present 
the two simplest ones. 

#### Unwrapping an Option and defining a default value

If you simply want to unwrap the inner value from a _Some_, and 
default to something (of the same type as the wrapped value would be) in case of a _None_, just use
the "getOrElse()" function of _Option_: 

{{< highlight scala >}}
val maybeString1: Option[String] = None
println(maybeString1.getOrElse("default value"))
val maybeString2: Option[String] = Some("Hello")
println(maybeString2.getOrElse("default value"))
{{< / highlight >}}

This example will print "default value" at first, and then "Hello" to the screen.


#### Using pattern matching

Usually it seems to be an overkill to use pattern matching to handle Options,
but at least 
<a href='{{< relref "post/patternmatch1.md" >}}'>
we have already covered it here</a>. So let's see how to do this:


{{< highlight scala >}}
val result: Option[Int] = None
val toReturn: Int = result match {
  case Some(num) => num 
  case None => 0
}
println(toReturn)
{{< / highlight >}}
In the above example, "toReturn" will always hold an Int value: if the Option did not
have a proper Int value (if it is not a _Some[Int]_ but a _None_), 
then the default value of 0 will be used.
So in this exact case, "0" will be printed.

#### Other possibilities

For more smart ideas on dealing with Options, see
[Daniel Westheide's blog post](http://danielwestheide.com/blog/2012/12/19/the-neophytes-guide-to-scala-part-5-the-option-type.html).

## Summary and other sources

By using Options we, as developers of a certain functionality, can clearly signal that
our function might return without a proper result.
Scala also helps (and requires) the caller of such function 
to deal with the situation: for example, by defining a default value.

[Daniel's post on Options](http://danielwestheide.com/blog/2012/12/19/the-neophytes-guide-to-scala-part-5-the-option-type.html) goes into more details, it's really worth reading.

Some runnable code examples are available [here](https://github.com/ador/scala-examples/tree/master/06_options).


_Note n+1_ : Feedback is welcome on [Twitter](https://twitter.com/adorster) 
or on [GitHub](https://github.com/hands-on-scala/hands-on-scala.github.io/issues/3) :)
