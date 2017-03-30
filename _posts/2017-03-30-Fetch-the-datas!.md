---
  layout: post
  title: Fetch the datas!
  tags:
  categories:
---

**HELLO!**

Really quick one today...
In the past week we have seem how to do some async actions in our code and we have learnt how to wait for processes to finish before going on.
However most of us still would like a simple way of collecting remote data and in flies `fectch` to our rescue [fetch](https://developer.mozilla.org/en/docs/Web/API/Fetch_API) is a new Api supported as of Chrome 42, Edge 14, Firefox 39, Opera 29 and Safari 10.1

Please note as of the moment fetch does not work on node js browserless environments for those making embedded apps and running in other envs.

Ok to the steak of this article how do we collect some data using `fetch`
```javascript
const getData = fetch('https://jsonplaceholder.typicode.com/posts')
.then((response) => { //here we fetch  contents of our url
  if(response.ok) {
    return response.json(); //if we get the content we return it  as a json object
  }
  throw new Error('Nework response broke'); //if response not ok lets throw an error
})
.then((respJson) => {
  console.log(respJson); //consume the data
})
.catch((err) => {
  console.log(err); //if an error occured show it
});

console.log(getData);
```

What is happening here?

We create a variable with our fetch call, you dont have to do this I did so i could log as I wasn't using this particular code with any other.

`fetch` takes on mandatory parametere this is the path to the resource you want and returns a [promise](https://zacck.github.io/node/2017/03/28/Send-Promises-for-Weather.html).

 1. We can deal with it as a normal promise
 2. We define our first `then` here we collect the data and watch for any issues.
 3. After collecting and checking we call `then` again isnt this a little chain? here we use the result from the `fetch` promise.
 4. We add a `catch` call to let us know if any issue occured during our calls.

Queries? Suggestions? PR?

Back To Code!:P
