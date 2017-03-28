---
  layout: post
  title: Send Promises for Weather
  tags:
  categories:
    - node
    -
---

I have been working on quite an amount of **asynchronous** Javascript lately and I felt the need to work some more on Promises and other threading structures in node.

What we are going to do today i build a small terminal app to fetch the weather for your's truly as I pretend to be a surfer who uses the cli a lot

**Assumptions**

* Familiarity with basic Javascript
* Interest in es6/es2015


Ok lets go;

**I**. First lets make an entry file called `app.js` and two other files `location.js` , `weather.js` we will use these two later to do the actual work of fetching our location and the weather thereof.

**II**. Lets begin by finding the users location (later we can use GPS but lets use a placename for now e.g Paris, New York, Nairobi). Add the following to `location.js`;
```javascript
//guestimate the users location
var url = 'http://ipinfo.io/';
var request = require('request');
module.exports =  () => {
  return new Promise((resolve, reject) => {
    //lets use request to fetch  a guestimate of the location using ip
    request({url: url, json: true}, (error, response, body ) =>{
      if(error) {
        reject(`${error.message} occured`)
      } else {
        //lets resolve our promise with the data
        resolve(body);
      }
    });
  });
}
```
What happens here is we make a new promise that fetches the contents of the ininfo for our location information and incase an error occurs it will `reject` with that error or `resolve` with our wanted data. For the purposes of this sample we shall use [request](https://yarnpkg.com/en/package/request)
to fetch our url data feel free to use other methods here AJAX, axios, fetch  maybe even a promise!

**III**. Now lets fetch the weather since we have the location of the user. In `weather.js` lets proceed to add a call to the openweathermap to fetch the current weather of the found location. Lets define out promise to get weather:
The name, weather, high and low are values from the json we get back from [openweathermap](http://openweathermap.org).

```javascript
  const weatherGetter =  () => {
    return new Promise(function(resolve, reject) {
       request({url: cityUrl, json: true}, function(error, response, body ) {
       if(error) {
         reject(`error.message, occured`)
       } else {
         const name  = body.name;
         const weather = body.weather[0].main;
         const high = body.main.temp_max;
         const low = body.main.temp_min;
         //console.log(JSON.stringify(body, null, 4))
         resolve(`${name} weather today is ${weather} with highs of ${high} celcius and lows of ${low} celcius`)
       }
     });
    });

  }
```

**IV**. To string all this together we can add some more code in `weather.js` check out the full sample here [weather.js](https://github.com/zacck/async-js-/blob/master/weather.js)

```javascript
if(location.length > 0) {
  console.log(`Checking Weather for ${location} >>>`);
  city = location
  cityUrl = `${unitUrl}&q=${city}`;
  weatherGetter();
} else {
  console.log('Finding Location >>')
  //lets call location
  loc().then((data) => {
    console.log(`Checking Weather for ${data.city} >>>`);
    city = data.city;
    cityUrl = `${unitUrl}&q=${city}`;
    weatherGetter().then((data) => {
      console.log(data);
    })
  }, (locationErr) => {
    //incase our promise rejects
    console.log(`Error ${locationErr} occured`)
  })
}
```

**V**. Finally lets add some desert! Let's enable `app.js` capability my allowing `cli` options, for this we are going to use [yargs](https://yarnpkg.com/en/package/yargs)

```javascript
var weather = require('./weather.js')
//set up arguments we want
var argv =  require('yargs')
  .command('get', 'get the weather', (yargs) => {
    yargs.options ({
      location: {
        alias: 'l',
        description: 'provide your current location e.g Paris, Nairobi',
        type: 'string'
      }
    })
    .help('help') //enable --help
  })
  .help('help')
  .argv;
var command= argv._[0];

if(command === 'get') {
  weather(argv.location)
}
```

In here we can see we are using the yargs package to allow a command line flag `get` and that it accepts the name of your current location we then proceed to import weather and find the weather from it to see a all the code working together take a look here [app](https://github.com/zacck/async-js-)

For any questions or suggestions add some issues or [tweet](https://twitter.com/noob_developer) me!

Back to code :D
