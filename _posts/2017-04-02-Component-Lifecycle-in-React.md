---
  layout: post
  title: Component Lifecycle in React
  tags:
  categories:
---

**HELLO!**

Today I would like to go through React Component Lifecycle Methods or `hooks`. These are methods that are called when an event happens to/in a React Component.

`render`
Firstly this is the only required method in a Component. This method is responsible for manipulating the DOM. In here you basically define your view. For this post let's use a timer that gets passed seconds and counts down to zero. Consider the following examples

```javascript
render(){
    return (
        <div>
          <div>
          </div>
        </div>
    );
  }
```
Please note render can only return one root element/doc or it will throw an error.
Here you can see I simply define a `div` that contains my element which we shall later update to show the data.

`constructor`
This method is called before a component is mounted. Consider using this method for initialization of your component and the elements within it. You can also set your initial state here. I intend to keep track of the remaining seconds in my application so I shall set up a state element for that it would also be nice to show a message when the countdown is over.

```javascript
constructor(props) {
    //always call super as this.props will be undefined
    super(props);
    //initialize state
    this.state = {
      timeLeft: 0,
      message: ''
    };
  };
```
The constructor takes in `props` provided to the Component. Ensure to always call super here or else `this.props` will be undefined! As you can see here I initialize two state elements that I will use later. `state` Is a component property and you can manipulate it in various ways.

`componentDidMount`
This method is called right after a component is mounted. It is advisable to do long computation work here e.g stuff such as network requests and resource manipulation. Consider our timer

```javascript
componentDidMount() {
  //this is called directly after the app starts
  //lets reduce the seconds
  this.setState({timeLeft:this.props.seconds});
  //set up a one second interval
  this.timerID = setInterval(() => this.setState({
    timeLeft: this.state.timeLeft - 1
  }), 1000);
}
```
As you can see here I take in the props that I get and use this to start my timer that deducts a second for every  1000 milliseconds this being equal to 1 second. You can see here that we are manipulating state in a way that is a little different instead of setting it directly we are using another hook. Which we shall explore later

`componentDidUpdate`
This method is invoked right after a Component receives props and gets updated. You can manipulate the DOM here and do some clean up if desired. In our sample we shall check if the countdown is done. Stop the interval and show a message to the user.

```javascript
componentWillUpdate(nextProps, nextState) {
    if(nextState.timeLeft <= 0) {
      clearInterval(this.timerID);
    }
  }
```
You see this method takes in nextProps and nextState. Here I check if the time left is more than 0 to check whether I need to keep counting. If I dont I simply clear my timer.

`componentWillUnmount`
This method is invoked as a component is destroyed and you can take this chance to clear any computation you were doing for this component say clearing things like subscriptions and location watchers would be ideal here also things like cancelling network requests.

```javascript
componentWillUnmount() {
    clearInterval(this.timerID);
  }
```
As you can see for our trivial example all I do is clear my Interval Timer.

`shouldComponentUpdate`
Say I would like to make my timer update only on even seconds so I will show 30, 28, 26  and so on and so forth. Lets use this hook to implement this.
```javascript
shouldComponentUpdate(nextProps, nextState) {
    if(nextState.timeLeft % 2 == 0) {
      return true;
    } else {
      return false;
    }
  }
```
Please note that if this returns false `render`, `componentWillUpdate` and `componentDidUpdate` will not be triggered.

`componentWillMount`
This is the only Lifecycle hook that is triggered when doing server side rendering this is called before render and I will touch on it in a different post.


`setState`
This is a hook used to update any data that the component is persisting. Notice we do this instead of calling `this.state` as that method should only be used for initializing avoid setting state directly as much as possible.

```javascript
//lets reduce the seconds
this.setState({timeLeft:this.props.seconds});
```
As you can see I pass in an object with the values I would like updated that is being persisted this hook can also take a function as such `this.setState((state, props) => newState)`.

`state`
This is a hook used to initialize state items for a component. We do this in our constructor.

```javascript
this.state = {
    timeLeft: 0,
    message: ''
  };
```
You can see here I pass in an object with the values I would like to initialize being timeLeft and message.


**Component Properties**

`DefaultProps`
 We can  use this outside the class definition of our Component to set the default props for a component.
```javascript
//set our default values
Main.defaultProps = {
  seconds: 0
};
```
This helps with your component not running into undefined values when initialized with wrong props. Use this as a failsafe

`PropTypes`
We declare this outside the class definition and we use this to do typechecking for the props we receive.
Say I want to receive a number for the seconds that I receive. I shall do it as follows.

```javascript

//declare default Props expected by app
Main.propTypes =  {
  seconds: PropTypes.number
};
```

To see all this in action take a look at [my project](https://github.com/zacck/React-BoilerPlate)
I may have not covered every single Lifecycle hook in this post any thoughts and suggestions are welcome have fun hacking!!

Queries? Suggestions? PR?

Back To Code! &#x1f61d;
