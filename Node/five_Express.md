
# Level 5: Express

### 5.2 Express Routes
- Create a GET route for '/tweets' and give it the proper callback. The callback function should accept two arguments: the request and the response.
- Send back the file tweets.html, which lives under the project's root path. Remember to use __dirname to locate tweets.html.
- Finally, have the express app listen on port 8080.

twitter.html
```sh
<html>
  <ul>
    <li>Real Time Web with Node.JS Launched!</li>
    <li>Node.js Rules!</li>
  </ul>
</html>
```


app.js
```sh
var express = require('express');
var app = express();
app.get('/tweets', function(request, response){
    response.sendFile( __dirname + '/tweets.html');
}).listen(8080);
```

### 5.3 Route Params

- Start by creating a GET route for '/quotes' that takes a name parameter as part of the URL path.
- Now, use the name parameter from the URL to retrieve a quote from the quotes object and write it out to the response. Note: No piping here, just write the quote string to the response like you did in previous levels (and then close the response).

app.js
```sh
var express = require('express');
var app = express();

var quotes = {
  'einstein': 'Life is like riding a bicycle. To keep your balance you must keep moving',
  'berners-lee': 'The Web does not just connect machines, it connects people',
  'crockford': 'The good thing about reinventing the wheel is that you can get a round one',
  'hofstadter': 'Which statement seems more true: (1) I have a brain. (2) I am a brain.'
};

app.get('/quotes/:name', function(req, response){
  response.end(quotes[req.params.name]);
});

app.listen(8080);
```

### 5.4 Rendering

Instead of just writing out the quote to the response, let's try using an EJS template to render the response.
- First, render the quote.ejs template to the response.
- Next, make the name and the quote data available to the template.
- Inside quote.ejs, add the code needed to render the data you passed to the template.

app.js
```sh
var express = require('express');
var app = express();

var quotes = {
  'einstein': 'Life is like riding a bicycle. To keep your balance you must keep moving',
  'berners-lee': 'The Web does not just connect machines, it connects people',
  'crockford': 'The good thing about reinventing the wheel is that you can get a round one',
  'hofstadter': 'Which statement seems more true: (1) I have a brain. (2) I am a brain.'
};

app.get('/quotes/:name', function(req, res) {
  var quote = quotes[req.params.name];
   res.render('quote.ejs', {
    name: req.params.name,
    quote: quote
  });

});

app.listen(8080);
```

vews/quote.ejs
```sh
<h2>Quote by <%= name %></h2>

<blockquote>
  <%= quote %>
</blockquote>
```

### 5.5 URL Building
create a page which calls the Twitter search API and displays the last few results for Code School. The first step is to construct the proper URL, which is all you need to do in this challenge.

- Add the protocol attribute to options
- Add the host attribute to options.
- Add the pathname attribute to options
- Add an attribute which takes an object of query parameters, in this case we only need q to search Twitter

app.js
```sh
var url = require('url');

options = {
  // add URL options here
  protocol: 'http:',
  host : 'search.twitter.com',
  pathname : '/search.json',
  query: {q:'codeschool'}
};

var searchURL = url.format(options);
console.log(searchURL);
```


### 5.6 Doing the Request
- To start, require the request module and assign the return function to a variable.
- Next, issue a request to searchURL. Remember, the callback function for the request function takes three arguments: error, response and body.
- Finally, log the response body to the console using console.log()

app.js
```sh
var url = require('url');

var options = {
  protocol: "http:",
  host: "search.twitter.com",
  pathname: '/search.json',
  query: { q: "codeschool"}
};

var searchURL = url.format(options);
var request = require('request');
request(searchURL, function(error, response , body){
    console.log(body);
});
```

### 5.7 Express Server
create an Express server which queries out for the search term and then returns the JSON

- Require the express module
- Create the Express server and name it app
- Create a route for GET requests to / (root path). Remember, the callback function takes two arguments: a request req and a response res
- In our new route, issue a request to searchURL and pipe the results into the response.
- Finally, tell app to listen on port 8080

app.js
```sh
var url = require('url');
var request = require('request');
var express = require('express');
var options = {
  protocol: "http:",
  host: "search.twitter.com",
  pathname: '/search.json',
  query: {
    q: "codeschool"
  }
};

var searchURL = url.format(options);

var app = express(); // Create server here
app.get('/', function(req, res){
    request(searchURL).pipe(res);
}).listen(8080);
```
