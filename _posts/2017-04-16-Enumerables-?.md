---
  layout: post
  title: Enumerables ?
  tags:
  categories:
---
**HELLO!**

What are Enumerables?
These are collections that can be mapped or traversed using numbers. Think of `sets`, `lists`, `arrays` in programming.

We use these quite a bit in day to day work. Imagine something like months of the year and their various uses.

`January, February, March, April, May, June, July, August, September, October, November, December.`

Here we have a collection of twelve that can be represented using an arbitrary sequence of numbers say 1 for January, 2 for February and so on and so forth.


**Task**

Lets assume we want to create system that calculates the dates of payment for customers who join an insurance platform. We can assume that the first charge will be done on a certain date of the first month. This will keep happening for as long as the user is subscribed to that plan.

```Elixir
defmodule Payments do
  def dates(term, date) do
    Stream.cycle(["January", "February", "March", "April", "May", "June", "July", "August","September", "October", "November", "December"])
    |> Enum.take(term)
    |> Enum.map(&(&1 <> " - " <> date))
  end
end
```

What is happening here?

We define a module that will handle most of payments functionalities.

Then we define a function to calculate the dates for our payment in the future so that we can debit the card provided by the user.

We use [Stream](https://hexdocs.pm/elixir/Stream.html) to produce an infinite list of `1 - 12` Tagged Month lists.

`Stream.cylce`

Then we use [Enum](https://hexdocs.pm/elixir/Enum.html).take to use collect the first `term` items to collect the appropriate amount of payments that our user will have to pay considering the term length.

`Enum.take(term)`


Finally we use the `map` method to cycle through all of the items and tag them with  the date and we finally get a result like below

```Elixir
["January - 16", "February - 16", "March - 16", "April - 16", "May - 16",
 "June - 16", "July - 16", "August - 16", "September - 16", "October - 16",
 "November - 16", "December - 16", "January - 16", "February - 16",
 "March - 16", "April - 16", "May - 16", "June - 16", "July - 16",
 "August - 16", "September - 16", "October - 16", "November - 16",
 "December - 16", "January - 16", "February - 16", "March - 16", "April - 16",
 "May - 16", "June - 16", "July - 16", "August - 16", "September - 16",
 "October - 16", "November - 16", "December - 16", "January - 16",
 "February - 16", "March - 16", "April - 16", "May - 16", "June - 16",
 "July - 16", "August - 16", "September - 16", "October - 16", "November - 16",
 "December - 16", "January - 16", "February - 16", ...]
```

These are just a few ways I can think of using and working with Enumerables.

Check out the [Enum](https://hexdocs.pm/elixir/Enum.html) protocol to learn more about this type and what you can do with it.



Queries? Suggestions? PR?

Back To Code! &#x1f61d;
