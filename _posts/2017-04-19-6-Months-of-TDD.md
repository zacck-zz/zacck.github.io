---
  layout: post
  title: 6 Months of TDD
  tags:
  categories:
---

**What is TDD**

So what does the term `TDD` mean? TDD - [Test Driven Development](https://en.wikipedia.org/wiki/Test-driven_development), This is a process that relies on the repetition of a very short cycle. Where requirements are turned into specific test cases then software is implemented to pass those tests. TDD is related to the test-first concept of [extreme programming](https://en.wikipedia.org/wiki/Extreme_programming).

**How We Use TDD**

If you are going to build a non trivial application it is very likely that your code will be split up into various parts and sections. Now if we were to try and flesh out all the tests for our code before we wrote it. Well that would take quite a while and when will you ever get to write your code?

Luckily this is not how TDD works, Yes one is expected to write Tests before they write implementation but you don't need to write all your tests before you start your implementation.
Rather we are encouraged to;
1. Write a unit test.
2. Run and Watch this test fail (this is an important step).
3. Write our implementation.
4. Run our test
5. Refactor (if necessary) ... repeat

Say We had to build a `Todo` Application. In Our Application we can have a list of Todo Items. Let's consider our TodoList the unit we are testing here.

We could have a few features for our TodoList.

- Show Message when no Todos have been created.
- Show one Todo Item for each todo.

Here we would;
 1. Write the test for the TodoList Component.
 2. We could first test for the message if the Todos are empty this would fail.
 3. We would now know that our test is failing because our code isn't working and we would be assured about the lack of false positives.
 4. We would then implement the case for empty Todos and run our test again if we are lucky on our first try it will pass! Yes we can go back and clean the code if necessary rather go forward and test more stuff.

 To see an example of this in action checkout this [tests](https://github.com/zacck/ReactTODOSample/tree/master/app/tests).

**Cost and Benefits of using TDD**

For the last 6 Months I have tried to test as much of my code as I can in an effort to see how all this works:

- Yes you will have to write more code before you bring your application to production.
- Yes for TDD to work optimally and by working optimally I mean TDD will prevent 40 - 80% of your bugs from getting to production so this is 40 - 80% less time to deal with bugs.

As a developer this seems like a major win.

*Please note when tests are written after implementation they are not as efficient as when written before.*

The reason for this is, in Unit testing you use assertions to check if a result is what you would like it to be (*Tests for Correctness*) and herein lies the secret for writing tests.

When you have to **assert** on your code to check whether it works it implies you have to have thought and figured a result before you write the test code.

TDD forces you to consider the direction you are taking and why! This in turn clears out a lot of logic, syntax errors and dead code**.

Personally I find it take me 80% of my time to write a test and 20% to write the implementation of the code.


Queries? Suggestions? PR?

Back To Code! &#x1f61d;
