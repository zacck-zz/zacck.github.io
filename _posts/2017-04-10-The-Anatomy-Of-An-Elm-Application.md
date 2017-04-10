---
  layout: post
  title: The Anatomy Of An Elm Application
  tags:
  categories:
---

**HELLO!**

I am currently working on a [series](https://zacck.github.io/2017/04/06/TDD-with-Elm-part-1.html) on how to use TDD with Elm to make simple and powerful applications. I thought it best to review the usual parts of an elm application module.
Lets take a look at the widely acclaimed [Elm Archtecture](https://guide.elm-lang.org/architecture/), This as described in the docs is a simple pattern for designing and building webapps in elm. It's particularly useful when going for modularity, code resuse and testing(I like testing!!).

Please note this architecture seems to be a consequence of the design of Elm itself and it seems to emerge naturally in Elm.


**OK To the Meat!!**

The Basic pattern observed in this can be broken into three separate pieces.

**Model**

This is a representation of the current state of your application. State being the data you are persisting and observing.

```elm
-- MODEL
-- This is our application model we can use this for the data layer
type alias Model =
    Bool
```

Above is a rather simplistic state representation let's assume that our application/module needed to watch a boolean and react accordingly. Here you can see we declare a `Model` and [alias](https://guide.elm-lang.org/types/type_aliases.html) it to a type of `Bool`.

**Update**

This contains the methods or ways you would use to update your state so on our case we can have a couple of functions that react to user's inputs and proceed to update the state as necessary.

```elm
-- UPDATE
-- this function will be called by Html.program each time a message is received
-- it responds to messages updating the model and returning commands as needed
update : Msg -> Model -> ( Model, Cmd Msg )
update msg model =
    case msg of
        Expand ->
            ( True, Cmd.none )

        Collapse ->
            ( False, Cmd.none)
```

Ok some stuff just came out of the woodwork here! The `Msg` you see here is a type of `action` we have in our application if you are familiar with redux consider the `Update` a dispatcher and `Msg` to be an action. If you are not think about it this way; Messages are activities specific to our application. A Todo Application would have something like `AddTodo`, `CompleteTodo`, `DeleteTodo` Consider them functions that update the state in a specific way, Update being the vehicle we use to run the change on data/model.


**VIEW**

This is a rendering of your applications UI depending on your state. If you want to update the UI in your application it is best to do this by changing the state or a piece of it.

```elm
-- VIEW
-- This is a function that renders an Html element using our application model
-- the type signature Html Msg means this will produce messages tagged with Msg
view : Model -> Html Msg
view model =
    div []
        [ text model ]
    if model then
        div []
            [button [onClick Collapse] [text "Collapse"]
            , text "Widget"
            ]
    else
        div []
            [button [onClick Expand][text "Expand"]]
```

Here we can see the that our view function takes in the state of the application and depending on the state in our case a simple boolean it will render a different view if state in false it will render a button with the `Expand` text else it will render a button with `Collapse` text and a test widget next to it. You can see here that each button has an onClick with a message  this is the message that we pass to update that leads to state modification which in turn modifies the UI.

Phewks! That was a lot to cover!

If you want to see all of this in action togetheter in a simple elm app see my [TDD Project](https://github.com/zacck/ElmWebApp) here.

I felt it was necessary to cover this before diving into testing components/modules in elm.

Queries? Suggestions? PR?

Back To Code! &#x1f61d;
