+++
categories = ["intro", "enums"]
date = "2016-04-29T17:30:00+02:00"
title = "Enums in Scala"

+++

# Enumerations - what are they for?

Generally in programming, enumerations, or for short, enums,
are a simple means to create a little model within our code.
Enums are very simple and therefore limited in their modeling 
capabilities: they can only model things that can have a fixed, limited
number of different values. And under the hood, an enum type
is just something that can have any integer value out of a pre-defined 
set of integers, that were given readable names.
This description might sound a bit too abstarct, so 
let's see two examples instead in Scala.

## First example: days of week ? or second ex.?

{{< highlight scala >}}
object DayOfWeek extends Enumeration {
  val Sunday, Monday, Wednesday, Thursday, Friday, Saturday = Value
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
