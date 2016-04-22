+++
categories = ["intro", "setup"]
date = "2016-04-15T16:30:00+02:00"
title = "Short intro to Scala"

+++

# Welcome!

You're probably here because you've heard that Scala is a cool programming language
that you'd like to learn. Because, hey, it's object-oriented and functional at the same time!

I'll show you something very basic at first: a bit more "personal" version
of the famous 
["Hello World" program](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program).
The following little Scala program will ask for your name and then it'll print "Hello, <You>!" to the console.

{{< highlight scala >}}
object WordApp extends App {
  val name = scala.io.StdIn.readLine("What's your name? \n")
  println("Hello " + name + "!")
}
{{< / highlight >}}

In case this is really your very first Scala program, 
you might ask: how do I make the above example _App_ come alive?
Well, you have more than one option. (Btw, you'll have to get used to this in the world of Scala -- usually there is more than one way to do things. I admit that this fact is not very
beginner-friendly, but later it will come handy.) 

At first let's not complicate things with IDEs and GUIs, let's just use the
console tools available. Another post will show you how to use Eclipse or IntelliJ IDEA for
Scala development.

## Setting up our first Scala project with SBT
SBT stands for the ["Scala Build Tool"](http://www.scala-sbt.org/). It's like 'gradle' or 'maven' for Java.
If you are not familiar with build tools, then consult the Internet :)

### Installing SBT
Check the latest install documentation here:
[http://www.scala-sbt.org/release/docs/Setup.html](http://www.scala-sbt.org/release/docs/Setup.html)

### Creating the "Hello" project
It won't be as painful as it might seem at first :)

It's really just two steps writing the source files to an appropriate location,
and give some hints to SBT about how it should do its work.

#### The source tree

SBT expects the source Scala files (and tests, but we won't have any for now) to be
in a specific folder. So, let's go ahead and create them (I'm assuming you have
soma basic experience with the Linux command line):

{{< highlight bash >}}
mkdir -p src/main/scala
mkdir -p src/test/scala
{{< / highlight >}}

Within these two directories we'll usually have somewhat parallel sub-directories
with packages for our main source files and tests. Now we won't have any packages or tests,
for simplicity.

The source file we'll edit must be in the "src/main/scala/" folder. Let's name it
"App.scala". (You can use another name, but it wouldn't be a good idea to change
the ".scala" extension.) 
And its contents, as above:
{{< highlight scala >}}
object WordApp extends App {
  val name = scala.io.StdIn.readLine("What's your name? \n")
  println("Hello " + name + "!")
}
{{< / highlight >}}
So, just save this into a file "src/main/scala/App.scala".


#### The "build.sbt" file

This little confg-like file will set some useful settings for your project,
and also contains a list of dependencies.

It should be saved to the top-level directory of your project, next to the "src" folder.

And its contents:

{{< highlight scala >}}
name := "01_grader_app"

version := "0.1"

exportJars := true

scalaVersion := "2.11.8"
{{< / highlight >}}

Note the empty lines! Looks stupid, but they are actually necessary, if you are 
using an older SBT version, prior to 0.13.7.
([Here](http://stackoverflow.com/questions/21780787/why-does-sbt-version-%E2%89%A4-0-13-6-require-blank-lines-between-settings-in-sbt-fil) is an explanation.)

To check which version you have, run:
{{< highlight bash >}}
sbt 'inspect sbtVersion'
{{< / highlight >}}

With newer versions (from 0.13.7 up) you don't need the empty lines.

[More help with SBT](http://scalatutorials.com/beginner/2013/07/18/getting-started-with-sbt/)

### Let's run it already!

Standing in the root of your project, just say:
{{< highlight bash >}}
sbt run
{{< / highlight >}}

I hope it works for all of you now! :)

### More things to read
 - The official Scala site: [www.scala-lang.org](http://www.scala-lang.org/)
 - SBT: [www.scala-sbt.org](http://www.scala-sbt.org/)



