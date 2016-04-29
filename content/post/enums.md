+++
categories = ["intro", "enums"]
date = "2016-04-29T17:30:00+02:00"
title = "Enums in Scala"

+++

# Enumerations - what are they for?

Generally in programming, enumerations (a.k.a. enums)
are light-weight means to create a very simple model within our code, for
representing a custom type with a limited set of possible values with readable 
names.
This description might sound a bit too abstract, so 
let's see an example instead.

## Example: days of week

Let's introduce an enum for representing the days of week.
In Scala, you have to create an _object_ for this, which 
needs to extend Scala's _Enumeration_ trait (we'll learn more about objects 
and traits later).

{{< highlight scala >}}
object DayOfWeek extends Enumeration {
  val Sun, Mon, Wed, Thu, Fri, Sat = Value
}
{{< / highlight >}}

As you can see, it's almost as easy as listing the possible values,
separated by commas. But don't forget the "val" from the beginning and 
the " = Value" part from the end of the value list, because without them, 
your shiny new enum will not work.

After defining this new enum in our code
we can start using days of week (after importing them!) as in the
following example:
{{< highlight scala >}}
import DayOfWeek._

override def main(args: Array[String]): Unit = {
  println(Mon)
}
{{< / highlight >}}

And this tiny program will print the string "Mon" to the screen. Try it!

It's also easy to loop over all possible values of an enum:

{{< highlight scala >}}
override def main(args: Array[String]): Unit = {
  DayOfWeek.values.foreach { day => println(day) }
}
{{< / highlight >}}

That's it!

In the next post, we'll see how to use enum values when using pattern matching in Scala.


