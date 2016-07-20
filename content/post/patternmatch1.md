+++
categories = ["intro", "patternmatching"]
date = "2016-05-06T17:30:00+02:00"
title = "Basic pattern matching in Scala"

+++

# Introduction to pattern matching in Scala

Pattern matching is a quite commonly used "programming pattern" in functional languages, because it 
fits nicely into the "functional way of thinking", and it is quite powerful and handy as a tool.

<!--more-->

It's somewhat similar to a sequence of _if / else_ statements or to the _switch_ statement
of Java or C, but it is much more powerful, because it lets you form more complex 
conditions for matching, even for the inside of an object. 

In some cases
<!-- (when dealing with objects of _case classes_ for example; we'll learn about them a bit later in more detail) -->
Scala can automatically _decompose_ an object that you want to match and look inside it to check
if its structure matches your expectations.

<!--This means 
that you can apply rules based on the object's type or inner structure without having 
to manually disassemble the object into its parts.-->

But, before going too deep, let's see some examples.

## Example 1: matching value

Here the object what we match to patterns is _x_, an integer.
{{< highlight scala >}}
object MatchTest1 extends App {
  def matchTest(x: Int): String = x match {
    case 1 => "one"
    case 2 => "two"
    case _ => "many"
  }
  println(matchTest(3))
}
{{< / highlight >}}
Fairly simple, isn't it? Just use the _match_ keyword after the name of the
thing you'll want to match, and list your cases within curly braces.
The match expression in our case will return the value that appears on the right side of the '=>' arrow, corresponding
to the first matching case. So the order of the _case_s will matter if there is some overlap among the left sides of the arrows!

One importatnt thing to note is the last case where an underscore is used: this is Scala's notation
for "match anything". Without this line, we would get a "scala.MatchError" because we called 
the _matchTest()_ function with the value 3, which is not covered by the other _case_ branches.

So the main point to remember from here is that you should be sure to cover all
possible options when using a _match_ expression if you want to avoid ugly errors.
The fail-safe option usually is to use the underscore as the last _case_.
It will define a default path for the program flow for "all other cases".

(Note: I just copied this example from the
[official documentation](http://docs.scala-lang.org/tutorials/tour/pattern-matching.html)).

## Example 2: matching type

If we want to write a function that behaves differently for different input _types_, we can write something like:
{{< highlight scala >}}
def getType(x: Any): String = {
  x match {
    case x: String => "String"
    case x: Integer => "Int"
    case _ => "I don't know"
  }
}
{{< / highlight >}}
The main difference from the previous example is that now we used _"x: Type"_ instead of a specified value on the left side
of the arrow, after the _case_ keyword. It's still simple :)

Note 1: "_Any_" is a general type in Scala, similar to the "_Object_" of Java, which is an ancestor of all other types.

Note 2: You don't need to use the same value name in the cases, because each 
case has its own scope with regards of the incoming
object to be matched. Just be sure to use the same name on both sides of the arrow within a case line.
{{< highlight scala >}}
  def getType2(x: Any): String = {
    x match {
      case a: String => "String: " + a
      case b: Integer => "Int: " + b
      case _ => "I don't know"
    }
  }
{{< / highlight >}}


## Example 3: using guards

Let's say we need some extra conditions to be true before applying the right side of a _case_.
Scala lets us perform these additional checks within any of the cases independently, as in the 
following example:
{{< highlight scala >}}
def getType3(x: Any): String = {
  x match {
    case a: String if a.startsWith("He") => "String with 'He'"
    case b: Integer if b > 0 => "Positive integer"
    case _ => "I don't know"
  }
}
{{< / highlight >}}
These additional conditions before the cases' arrows are called "guards". 
If they are evaluated to false, then 
the corresponding case branch is considered not matching, so the next case will be tried.


## Example 4: matching structure

I promised in the first paragraph that in some cases we will be able to
"automatically _decompose_ an object" to look inside it and check
if its structure matches our expectations.

How does it work in Scala, and what are the prerequisites?

The answer is: _case classes_! My next blog post will cover them in more detail.
For now let's think about a case class as a composite object with some 
auto-magic: automatically generated constructors and getters, for example.

For the more curious, here are
[some nice and short explanations](http://stackoverflow.com/questions/2312881/what-is-the-difference-between-scalas-case-class-and-class%29), and the official (quite dense) [description of case classes](http://docs.scala-lang.org/tutorials/tour/case-classes.html).

So, for an example of automatic decomposition, at first we need a
case class. We'll write one, representing a tweet message, that has three parts:

- an identifier (_id: Long_)
- an author (_author: User_, that itself could be a complex case class, now it only contains one String, a name)
- a message (_msg: String_)

Defining these new types (_User_ and _TweetMsg_) in Scala takes only two fairly short lines:

{{< highlight scala >}}
case class User(name: String)
case class TweetMsg(id: Long, user: User, msg: String)
{{< / highlight >}}

And now a function can match a tweet's inners like this:

{{< highlight scala >}}
def processTweet(tweet: TweetMsg) = tweet match {
  case TweetMsg(id, _, _) if id < 0 => "Invalid (negative) tweet id!"
  case TweetMsg(_, user, _) if user.name == "adorster" => "Hello, " + user.name + "!"
  case _ => "Just another tweet"
}
{{< / highlight >}}


Example codes with tests are available at [my scala-examples github repo](https://github.com/ador/scala-examples/tree/master/02_pattern_match_app).

_Note n+1_ : Until I set up a comments section somehow here, feedback is welcome via [Twitter](https://twitter.com/adorster) :)
