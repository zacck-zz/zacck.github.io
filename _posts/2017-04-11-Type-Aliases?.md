---
  layout: post
  title: Type Aliases?
  tags:
  categories:
---

**HELLO!**

You see I don't like typing code over and over again without understanding exactly what is going on under the hood. In a previous [post](https://zacck.github.io/2017/04/10/The-Anatomy-Of-An-Elm-Application.html), we covered the anatomy of an Elm application. One specific point stood out me was when we declare the Model for our application we use the syntax:

```Elm
type alias Model =
  Bool
```

This is obviously a very simplified version of a model. A `Todo` application for example would have a model that would be a little bit more realistic.


```Elm
type alias Model =
  { user: { name: "Zacck", height: "tall"},
    todos: [{desc: "get shorter", completed: false}]
  }
```


Lets Walk through what is  happening here:

`type alias Model`

[type aliases](https://guide.elm-lang.org/types/type_aliases.html) are meant to make your annotations in code easier to read. Here we reference to the complex `state` of our Todo application as `Model` and whenever when we need to read from or write to our state we simply call the annotation `Model`.  

Essentially we are telling our code to replace `Model` with the actual complex structure of the the data whenever than annotation comes up in our code!
When you create a type alias for some attribute, it also generates a record constructor for that attribute.

Our `Model` type alias generates this.

`Model: {height: String, name: String} -> List -> Model`

We can see here that it takes in a tuple with two strings and a list and in turn gives us back a  `Model`.

Type aliases my seem a very cosmetic - however we find they make it easier to think when writing code that has to interact with some data structure.

Have fun exploring  types in elm!!

Queries? Suggestions? PR?

Back To Code! &#x1f61d;
