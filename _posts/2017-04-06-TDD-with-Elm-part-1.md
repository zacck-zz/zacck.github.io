---
  layout: post
  title: TDD with Elm .. part 1
  tags:
  categories:
---
**HELLO!**

I am going to write a small series on this blog post on using TDD for a front end application built in elm specifically [shufflebox](https://github.com/AndelaOSP/shufflebox-frontend). I must warn you I am new to this project, I have been looking around for something built in Elm/Elixir to get stuck in with the intention of moving towards using Elm for application development.

**The Run Down:**

I chose this project for many reasons: it seems new, it's from Kenya and I 	&#x1f49c;  Kenya.
The project uses `webpack` for module bundling which is another open source project I love much.

Now seeing as the test runner had been set up and some sample tests were already passing, this seemed like low hanging fruit to tackle. To learn how to set up `elm-test`. Please checkout [this](https://github.com/elm-community/elm-test) link.

**Ok to the meat of this post.**

Lets begin by implementing a simple test that checks the sum of two numbers.
Make a new file called `Sample`, make sure that the file name begins with an uppercase letter.


Lets start by creating a new module and exposing everything from it. We should likely only export what  we need.
[Test](http://package.elm-lang.org/packages/elm-community/elm-test/latest/Test)

In this test we Import the `Test` module (we will use this as a signature later).

[Expect](http://package.elm-lang.org/packages/elm-community/elm-test/latest/Expect)

Then we import `Expect` (we use this module to do assertions later).

Awesome! Now lets make a function and give it a signature of `Test`

`sampleTest : Test`

Then we can declare the implementation of our function.

```elm
sampleTest : Test
sampleTest =
    describe "Sample 1"
    [ test "Runs new test" <|
      \() ->
        Expect.equal(3 + 3) 7]
```

Ok so what's happening here?
We first apply a description to the test we want to run, then we provide a list of tests to run. Our list contains one `test` and an expectation. This is then `piped` to [<|](http://elm-lang.org/docs/syntax#infix-operators) the results of an arrow function that asserts on the equality of a sum of two integers.

In our project lets run our test runner

`yarn test`

To see all this in action please see my fork of the project here
[project](https://github.com/zacck/shufflebox-frontend/tree/test).

Great Success!!! We have a failing test.

On the Next post we will handle testing a Component!!


Queries? Suggestions? PR?

Back To Code! &#x1f61d;
