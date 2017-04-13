---
  layout: post
  title: Implementing Reduce In Elixir
  tags:
  categories:
---

**HELLO!**

Let's explore functional recursion by Implementing a reduce function. What do I mean by a reduce function - A function that applies a function against an accumulated value and reduce them to a single value.



```Elixir
defmodule MyList do
    def sum(list) do
      # call do_sum with an initial sum of 0
      do_sum(list, 0)
    end

    #private edge case
    defp do_sum([]) do
      #incase we get an empty array return an atom
      :empty
    end

    #an empty array and sum will trigger this edge canse
    defp do_sum([], res) do
      # return sum
      res
    end
    #id array isn't empty lets call the adder
    defp do_sum([h|t], res) do
      # update value of result
      res = h + res
      # call userselves
      do_sum(t, res)
    end
end
```

What is happening here?

We are using the sum function to showcase `reduce` here you see we get a sum by adding the head of the list to the result thats initialized as 0.

We can consider a number of edge cases

1. Is the array empty?
If it is you can see we return an atom `:error`
2. Has the array been emptied and do we have a result?
If this case is triggered we return the `res` passed to us.

Otherwise the 3rd `do_sum` method will keep calling itself till it  has emptied it's contents.

Have fun trying this out!

Queries? Suggestions? PR?

Back To Code! &#x1f61d;
