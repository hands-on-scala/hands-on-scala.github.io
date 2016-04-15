+++
categories = ["intro", "setup"]
date = "2016-04-15T16:30:00+02:00"
title = "Short intro to Scala"

+++

# Welcome!

I'll show you something very basic at first: a bit more personal version of the 
famous ["Hello World" program](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program) in Scala.
The following little Scala program asks for your name and then prints "Hello, <You>!" to the console.
(Of course you need to substitute "<You>" with your name.)

{{< highlight scala >}}
object WordApp extends App {
  val name = scala.io.StdIn.readLine("What's your name?\n")
  println("Hello " + name + "!")
}
{{< / highlight >}}

You might ask: how do I make the above example App come alive?
Well, you have more than one option. (Btw, you'll have to get used to this in the world of Scala -- usually there is more than one way to do things). At first let's not complicate things with IDEs and GUIs, let's just use the
console tools available. Another post will show you how to use Eclipse or IntelliJ IDEA for
Scala development.

## Setting up a Scala project with SBT
SBT stands for the ["Scala Build Tool"](http://www.scala-sbt.org/). It's like 'gradle' or 'maven' for Java.
If you are not familiar with build tools, consult the Internet :)

### Installing SBT
Check the latest documentation here:
[http://www.scala-sbt.org/release/docs/Setup.html](http://www.scala-sbt.org/release/docs/Setup.html)

### Creating a "Hello" project

(WIP)
[http://scalatutorials.com/beginner/2013/07/18/getting-started-with-sbt/](http://scalatutorials.com/beginner/2013/07/18/getting-started-with-sbt/)

Start SBT in the console with the "sbt" command

{{< highlight bash >}}
$ sbt
{{< / highlight >}}

## More things to read
 - The official Scala site: [www.scala-lang.org](http://www.scala-lang.org/)
 - SBT: [www.scala-sbt.org](http://www.scala-sbt.org/)



