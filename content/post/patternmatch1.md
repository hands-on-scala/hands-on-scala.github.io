+++
categories = ["intro", "patternmatching"]
date = "2016-05-06T17:30:00+02:00"
title = "Basic pattern matching in Scala"

+++

# Why should we care about pattern matching?

Pattern matching is a quite commonly used "programming pattern" in functional languages.
It's somewhat similar to a sequence of _if / else_ statements or to the _switch_ statement of Java, but it is 
much more powerful, because it lets you _decompose_ the object to be matched on the fly. This means 
that you can apply rules based on the matched object's type or inner structure without having 
to manually disassemble the object into its parts.

But, before going too deep, let's see two very basic examples.

## Example 1: matching value

Here the object what we match against is _x_, an integer. (But of course it could be something else, a String, or anything really.)
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

One importatnt  thing to note is the last case where an underscore is used: this is Scala's notation
for "match anything". Without this line, we would get a "scala.MatchError" because we called 
the _matchTest()_ function with the value 3, which is not covered by the other _case_ branches.

So the main point to remember from here is that you should be sure to cover all
possible options when using a _match_ expression if you want to avoid ugly errors.
The fail-safe option usually is to use the underscore as the last _case_.
It will define a default path for the program flow for "all other cases".

(Note: I just copied this example from the
[official documentation](http://docs.scala-lang.org/tutorials/tour/pattern-matching.html)).

## Example 2: matching type

If we want to write a function that behaves differently for different input types, we can write something like:
{{< highlight scala >}}
def getType(x: Any): String = {
  x match {
    case x: String => "String"
    case x: Integer => "Int"
    case _ => "I don't know"
  }
}
{{< / highlight >}}
Tha main difference from the previous example is that now we used "x: Type" instead of a specified value on the left side
of the arrow, after the _case_ keyword. It's still simple :)

Note: _Any_ is a general type in Scala, similar to the "Object" of Java, which is an ancestor of all other types.

## Example 3: matching structure

I promised in the first paragraph that we will be able to "_decompose_ the object to be matched 
on the fly".  How do we use this capability of Scala in our code?

To demonstrate this, at first we need some objects that have a structure.
Here we'll have a composite object, a _case class_ (we'll learn more about case classes in another blog post) 
representing a tweet message, that has three parts:

- an identifier (_id: Long_)
- an author (_author: User_, that itself could be a complex type, now it only has a name)
- a message (_msg: String_)

{{< highlight scala >}}
case class User(name: String)
case class TweetMsg(id: Long, user: User, msg: String)
{{< / highlight >}}

And now a function can match a tweet's inners like in the following code snippet:

{{< highlight scala >}}
def processTweet(tweet: TweetMsg) = tweet match {
  case TweetMsg(id, _, _) if id < 0 => "Invalid (negative) tweet id!"
  case TweetMsg(_, user, _) if user.name == "adorster" => "Welcome, " + user.name + "!"
  case _ => "Just another tweet"
}
{{< / highlight >}}

The "if thisAndThat" parts on the left sides of the arrows are called "guards", and I should have explained them in the previous example to keep this one simpler :) W.I.P.

Example codes with tests are available at [my scala-examples github repo](https://github.com/ador/scala-examples/tree/master/02_pattern_match_app).

