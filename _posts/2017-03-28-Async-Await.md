---
  layout: post
  title: Async Await
  tags:
  categories:
    - node
    - es6
    - javascript
    - async
---

Hi There I found this thing!

**Async Await**

For when you need to wait for things to happen

* Things to note this currently needs to run in a browser. You can use some other packages in nodejs to achieve this also things such as es6 Generators

**I**. Lets make a new file called `await.js`. Lets proceed to add the following code
```javascript
const waitAFewSeconds = () => {
  //lets return a promise that does serious work
  return new Promise(function(resolve, reject) {
    setTimeout(function () {
      resolve('seriousness done')
    }, 2000);
  });

}


//now lets call our function and wait for it to finish
async function wait()   {
  console.log('before await')
  console.log(await waitAFewSeconds());
  console.log('after await')
}
```

As you can see here we are making a new function that runs some serious  work and  we can use a promise to do this concurrently.

Then we proceed to run our code and when the time comes to wait for the result we run it with the keyword `await`.

And thereafter we go back to normal operations.

Queries? Suggestions? PR?

Back To Code!:P
