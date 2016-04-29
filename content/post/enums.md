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

## Enums in scala: first example

{{< highlight scala >}}
object DayOfWeek extends Enumeration {
  val Sun, Mon, Wed, Thu, Fri, Sat = Value
}
{{< / highlight >}}

After defining this new enum in our code (and importing it!) 
we can start using days of week as:
{{< highlight scala >}}
import DayOfWeek._ 
{{< / highlight >}}
WIP

## Improved enum of days of week

## Second example: Favouite colors


[Beware...](http://underscore.io/blog/posts/2014/09/03/enumerations.html)
