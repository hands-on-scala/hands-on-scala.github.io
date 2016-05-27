+++
categories = ["intro", "dojo"]
date = "2016-05-20T17:30:00+02:00"
title = "Our first Scala dojo"

+++

# What is a coding dojo?

In short, a coding dojo is an event where a group of programmers practice their craft in an organized way, focusing on a single coding problem.

A dojo usually lasts a couple of hours, depending on the style and the task to be solved.
For more details see [CodingDojo.org](http://codingdojo.org/cgi-bin/index.pl?WhatIsCodingDojo) or
[Joe Wright's blog post about coding dojos](http://code.joejag.com/2009/the-coding-dojo.html).

We usually do a _Randori Kata_ version, where the task is solved by a team of 4-6 people, who take 5-7 minute turns in pairs.

The task and the programming language is chosen in advance by one of us, or even better by a pair of dojo organizers. 
The organizers prepare the event by:

- Determining the general goal of the dojo. It should be NOT that the team should finish the task, but learning or practicing something!
(e.g.: following strict [TDD](https://en.wikipedia.org/wiki/Test-driven_development), 
focusing on careful planning, or learning a new language feature).
- Selecting a specific programming task that fits well the above goal.
- Solving the task before the real dojo, to check the difficulty and to be able to help out during the real dojo.
- Possibly re-defining the task or giving additional hints to the task description if needed.
<!--, somewhat tailored to the skills of the team mebers
who signed up for the dojo.-->
 

## The task

For the very first Scala coding dojo, I chose a simple task, because many of us was in an early phase of learning Scala.
The team had to implement a _grader_ application, that assigns marks (from 'F' to 'A') to an integer score.

The full description is available on [GitHub](https://github.com/ador/scala-examples/tree/master/01_grader_app).


## Give it a try!

Try to solve this problem! It's the most useful if you have some team-mates to practice [pair programming](https://en.wikipedia.org/wiki/Pair_programming)
as well, but it's not a requirement, you can do it by yourself.

_Note_: the GitHub repo with the task description also holds a solution, so be careful when looking around if you don't want to cheat! :)

If you get stuck, it might help to read my
previous posts about:

- [enumerations in Scala]({{< relref "enums.md" >}})
- [testing in Scala]({{< relref "testing1.md" >}})
- [pattern matching]({{< relref "patternmatch1.md" >}})

or just use good ol' Google :) 

## The team's solution

A solution can be found in the GitHub repo mentioned above. 

## What we learned
It's really worth to take some time at the end of a dojo to review
how it worked out, did we enjoy it, what we learned?

It's probably different for each of us, but we always learn from each other.
Sometimes it's just a new keystroke-combination of the
IDE that we use for development. Other times it's a convenient feature of the programming language,
or a new approach for the task.

It also happens that we learn something more 'personal': that YX is really fun to work with, or that 
maybe YZ is afraid to go out to the whiteboard, but when working in pairs, (s)he opens up and has really brilliant ideas.

In this specific case I learned how to measure code coverage in the Eclipse-based [Scala IDE](http://scala-ide.org/), and of course, how Enumerations
can be used in Scala.

_Note n+1_ : Until I set up a comments section somehow here, feedback is welcome via [Twitter](https://twitter.com/adorster) :)

