---
  layout: post
  title: Express Middleware Huh ?
  tags:
  categories:  
---

**HELLO!**

Lets talk about writing custom middleware in this case specifically for [Express JS](https://expressjs.com/).

Please note we shall assume you have expressjs installed on your node project

I use express alot I use it to serve most if not all of my nodejs applications and If you use it this much you must have encountred the term `middleware`.

What is middleware: middleware is a general term for software that serves to **"glue together"** separate, often complex and already existing, programs.

Lets say we have a stock express app that tells us 'Hello' when we load the page. Yeah Generic much ? `app.js`could look as follows.

```javascript
var express = require('express');
var app  = express();
const PORT = process.env.PORT  || 3000;
app.get('/', (req, res) => {
  res.send('Hello and Welcome!');
});

app.listen(PORT, () => {
  console.log(`express listening on port ${PORT}`);
});
```

Now if we ran `node app.js` we would get a log on our console saying the app has started and if we open `http://localhost:3000` on your browser you should see 'Hello and Welcome'.


Ok now for what you came for! Let's make a file name `middleware.js` in the same directory as `app.js`,
**remember to add `var middleware = require('middleware')` in your app.js file!**

Say we had a secret path on our express server such as `/secrets` when this path is hit we would like our server to log that our secrets have been read. Lets build a piece of middleware that watches that route and logs in `middleware.js` add the following.

```javascript
module.exports = {
  secretlogger: (req, res, next) => {
    //note with this we get the full request and response objects  for our reques
    const date = new Date().toString();
    console.log(`Request ${req.method}  ${req.originalUrl} ${date}`);
    next();
  }
}
```

What happens here is we are exporting a function that takes some parameters from the url and does some computing then lets the user go on using the `next` param or not! You can cancel the response and send back one of your own. Using something like
`res.status(404).send('Don't come here you are not allowed!)`

Now to tie all this together lets go back to `app.js` and add the following.

```javascript
//check the route
//add middelware
app.get('/secrets',  middleware.secretlogger, (req, res) => {
  res.send('You cheeky secret Reader!');
});
```

To see all this in action you can checkout my [expressjs codelab](https://github.com/zacck/express-js-lab).

Use all teh middlewares!

Queries? Suggestions? PR?

Back To Code!:P
