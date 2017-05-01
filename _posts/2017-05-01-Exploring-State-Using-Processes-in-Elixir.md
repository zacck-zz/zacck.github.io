---
  layout: post
  title: Exploring State Using Processes in Elixir
  tags:
  categories:
---

Interesting fact, This month one year ago I got to Cape Town. It's been a journey!

Today I would like us to explore some `state` using `processes` specifically in Elixir. As we know Elixir is an immutable language where nothing is shared by default if we want to use and share some form of state(persisting some information, say a list of todos). We can use a number of solutions Processes, ETS(Erlang Term Storage). For today I would like to explore the processes solution.

First of what are [processes](), In Elixir all code runs in `processes` these are isolated long running operations that run concurrent to one another, They communicate by way of receiving messages from each other and replying. Processes the basis for concurrency in Elixir and they provide us with means of building fault tolerant distributed systems.


**OK How do we use processes**

*Starting*

Processes can usually be started using the auto imported `spawn` macro.
Consider this

```Elixir
spawn fn ->
  IO.puts "This will be a different Process"
end
```

Here we start a process that runs a function which then outputs to the console while this is a bit trivial to be using a process for we can see clearly what a process does its input and output. This will return the `pid` (Process Identifier) for the spawned process we can use this to interact with our new process.

Note the above will start an independent process from the current on and if that crashes our current process will keep running. If you would like to stop the current process in case a spawned one fails one can always use `spawn_link`.

*Messaging*

A lot of the time we will be spawning processes with an intention of getting back some result from them. For this we can use the messaging implementations in processes.

You can send a process a message using `send()` and its pid.
Consider the following.

```Elixir
pid = spawn(fn  ->  ... end)

send pid, :message
```

Here we spawn a process which computes a long running functions and then we can call the `send` function with the `pid` for any running and attach some data as our message, All Elixir datatypes are accepted for messaging.


*Handling Messages in Process**

In order to receive messages and work on them, all processes have a mailbox and implement a  `receive` macro to handle messages in the mailbox. Processes handle one message at a time.

```Elixir
receive do
  message -> # do some stuff
end  
```

This would remove the first message in the mailbox and process it as one desires please note that pattern matching can be used to handle each message accordingly or in some cases ignore the message.

```Elixir
receive do
  {:say, msg} ->
    IO.puts(msg)
  {:think, msg} ->
    Logger.debug(msg)
  _other ->
    #default case
  end
```

Here we see our process will react differently to the message provided in the mailbox.







Queries? Suggestions? PR?

Back To Code! &#x1f61d;
