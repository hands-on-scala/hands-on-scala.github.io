+++
categories = ["intro", "testing"]
date = "2016-05-13T17:30:00+02:00"
title = "Testing our Scala code"

+++

# Why test our code?

This is a more 'practical' topic, and I'm sure that many would argue
that learning how to use a unit testing framework is not strictly necessary
for newcomers. But according to my experience, getting into the
habit of writing tests regularly quickly pays off.

Why? It's nicely summarized [here](http://blog.xebia.com/5-reasons-why-you-should-test-your-code/), I'm
just listing here the main points:

1. Regression Testing
2. Improve The Implementation Via New Insights
3. It Saves Time, Really
4. Self-Updating Documentation
5. It Is Fun

# Testing frameworks for Scala

In Scala, you basically have two main-stream options if you want to write unit tests for your code:

- [ScalaTest](http://www.scalatest.org)
- [Specs2](https://etorreborre.github.io/specs2/)

We'll explore the first one, the ScalaTest framework in this short post, through some basic examples.

## A simple test with ScalaTest

To use ScalaTest we need to add it as a dependency to our _build.sbt_ file in the root of our 
sbt project. (Note: If you don't know how to set up a Scala project with SBT, you can find help [here]({{< relref "setup.md" >}}))

We'll need to extend our initial _build.sbt_ with a new _libraryDepencencies_ part.
(_Note:_ If you already had dependencies in the libraryDependencies section, then just add a new line
to let SBT know that we want to use the ScalaTest framework. But be careful, 
all, but the last line within the _Seq_ should end in a comma!)
{{< highlight scala >}}
name := "my_tested_app"
version := "0.1"
exportJars := true
scalaVersion := "2.11.7"
libraryDependencies ++= {
  Seq(
    "org.scalatest"       %%  "scalatest" % "2.2.6" % "test"
  )
}
{{< / highlight >}}
In the above example, we tell SBT that we want to use the ScalaTest framework, version 2.6.6, so it 
will download all the necessary things at the first subsequent _'sbt build'_ or _'sbt run'_ or _'sbt test'_ command.

### Where do we put our test codes?

Usually another directory with the name _'test'_ is created next to the _'main'_ source folder
within the project's _'src'_ folder, that contains all the source codes. Inside these, a parallel directory
structure is used to hold the _packages_ which group together our scala files. (More about packages in a later post.)

[See an example here.](https://github.com/ador/scala-examples/tree/master/02_pattern_match_app/src)

If you use this standard layout for your source codes, then SBT will automatically explore 
your tests, and you'll be able to run all of them simply via the _'sbt test'_ command. But we jumped a bit ahead :)

At first let's write a test. We need to create a new file within the _'test'_ directory.
{{< highlight scala >}}
import org.scalatest.FlatSpec

class MyTest extends FlatSpec {

  "This example test" should "pass" in {
    assert(2 == 1 + 2)
  }
}
{{< / highlight >}}

Let's save it as _'src/test/scala/MyFirstTest.scala'_ within your project folder.

### Running our tests

And now let's see if it works: type into the console, while in the root of your SBT project:
{{< highlight bash >}}
sbt test
{{< / highlight >}}

Of course, the above test will fail: 

{{< highlight bash >}}
...
[info] *** 1 TEST FAILED ***
[error] Failed tests:
[error] 	MyTest
[error] (test:test) sbt.TestsFailedException: Tests unsuccessful
[error] Total time: 4 s, completed May 13, 2016 6:00:22 PM
{{< / highlight >}}

Because... oh yes, 1+2 does not equal to 2. I just wanted to show a failing test at first. Now let's fix it, and maybe add another test:
{{< highlight scala >}}
import org.scalatest.FlatSpec

class MyTest extends FlatSpec {

  "This example test" should "pass" in {
    assert(3 == 1 + 2)
  }

  "This second example test" should "also pass" in {
    assert(3 > 2)
  }
}
{{< / highlight >}}

After re-running _'sbt test'_:
{{< highlight bash >}}
[info] MyTest:
[info] This example test
[info] - should pass
[info] This second test
[info] - should also pass
[info] Run completed in 216 milliseconds.
[info] Total number of tests run: 2
[info] Suites: completed 1, aborted 0
[info] Tests: succeeded 2, failed 0, canceled 0, ignored 0, pending 0
[info] All tests passed.
[success] Total time: 5 s, completed May 13, 2016 6:08:34 PM
{{< / highlight >}}

This is it! 

[Another example](https://github.com/ador/scala-examples/blob/master/02_pattern_match_app/src/test/scala/pmatching/MatcherTest.scala),
related to the last example of [the previous post]({{< relref "patternmatch1.md" >}}).

_Note n+1_ : Until I set up a comments section somehow here, feedback is welcome via [Twitter](https://twitter.com/adorster) :)
