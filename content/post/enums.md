+++
categories = ["intro", "enums"]
date = "2016-04-29T17:30:00+02:00"
title = "Enums in Scala"

+++

# Enumerations - what are they for?

Generally in programming, enumerations, or for short, enums,
are a easy means to create a very simple model within our code, for .
representing a type with a limited set of possible values with readable 
names.
This description might sound a bit too abstract, so 
let's see two examples instead.

## Example: days of week

Let's introduce an enum for tha days of week.
In Scala, you have to create an "object" for this, which 
needs to extend Scala's Enumeration trait (more about objects 
and traits later...).

{{< highlight scala >}}
object DayOfWeek extends Enumeration {
  val Sun, Mon, Wed, Thu, Fri, Sat = Value
}
{{< / highlight >}}

After defining this new enum in our code
we can start using days of week (after importing it!) as here, for example:
{{< highlight scala >}}
import DayOfWeek._

override def main(args: Array[String]): Unit = {
  println(Mon)
}
{{< / highlight >}}

And this tiny program will print the string "Mon" to the screen.

It's also easy to loop over all possible values of an enum:

{{< highlight scala >}}
override def main(args: Array[String]): Unit = {
  DayOfWeek.values.foreach { day => println(day) }
}
DayOfWeek.values.foreach { day -> println(day) }
{{< / highlight >}}

That's it!

In the next post, we'll see how to use enum values when using pattern matching in Scala.

// TODO: add some links for more reading

//## Improved enum of days of week

//## Second example: Favourite colors


//[Beware...](http://underscore.io/blog/posts/2014/09/03/enumerations.html)
// is it still the case??
