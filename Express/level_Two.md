# Level 2: Middleware(8)
Understanding middleware and building a custom logger.

### 2.2 Mounting Middleware
Given an application instance is set to the app variable, which of the following function calls would you use to mount a middleware called logger ?
```sh
app.use(logger)
```

### 2.3 Default Middleware
What is the only middleware that's shipped with Express 4?
```sh
express-static
```

### 2.4 Express Static
Change the code in app.js to use the express-static middleware instead of the response.sendFile() function.

- Remove our app.get() containing the root '/' route.
- Mount the static middleware and serve files under the public directory

app.js
```sh
var express = require('express');
var app = express();

app.use(express.static('public'));

app.get('/cities', function(req, res){
  var cities = ['Lotopia', 'Caspiana', 'Indigo'];
  res.send(cities);
});
app.listen(3001);
```

### 2.5 Script Tags
Add some client side javascript

- Within index.html, include jquery.js using a <script> tag.
- Within index.html, include client.js using a <script> tag
- Now in the client.js file, complete the code for the $.get function so that it calls the /cities URL path, and then runs the appendToList function.

client.js
```sh
$(function(){

  $.get('/cities', appendToList );

  function appendToList(cities) {
    var list = [];
    for(var i in cities){
      list.push($('<li>', { text: cities[i] }));
    }
    $('.city-list').append(list);
  }
});
```

index.html
```sh
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Cities</title>
</head>
<body>
  <h1>Cities</h1>

  <ul class='city-list'></ul>
    <script src="jquery.js"></script>
    <script src="client.js"></script>
</body>
</html>
```

### 2.7 logging Middleware

- On the response object, listen to the event that's emitted when the response has been handed off from Express to the underlying Operating System.
- Inside of the finish callback, calculate the duration of the request by subtracting the startTime from a new Date object. Store the duration in the duration variable, which has already been declared for you.
- Using the stream object, which holds a reference to standard out, write the following message: "This request took ____ ms", where ____ is the duration for the request.
- If we run the code as is, the request will be stuck in our middleware. Call the function that moves processing to the next middleware in the stack.


logger.js
```sh
module.exports = function (request, response, next) {
  var startTime = +new Date();
  var stream = process.stdout;
  var duration = null;

  response.on('finish', function () {
      duration = +new Date() - startTime;
    var message = "This request took "+duration+" ms";
    stream.write(message);
  });
  next();
};
```

### 2.8 Add Logging Middleware

- In the following code in app.js, we require our new middleware and assign it to a variable called logger.
```sh
var express = require('express');
var app = express();

var logger = require('./logger');

//TODO: mount middleware

app.listen(3000);
```

What function should we call in order to mount the middleware and add it to the stack?
```sh
app.use(logger)
```

### 2.9 only GET
Build a middleware that ensures only GET requests are allowed to go through.
- First, in the only_get.js file, create an anonymous function that uses the middleware signature and assign it to module.exports. Remember, the Express middleware function signature takes three arguments.
- Use the request object to check if the HTTP method used is 'GET' and if it is, then call the function that moves processing to the next middleware in the stack.
-If the HTTP method is not 'GET', then complete the request by sending back a message that says 'Method is not allowed'.

only_get.js
```sh
module.exports = function(request, response, next){
  if(request.method == "GET"){
      next();
  }else {
    response.end("Method is not allowed");
  }
};
```

### 2.10 Buildings
```sh
var express = require('express');
var app = express();

app.use(function(request, response, next){
  if (request.path === "/cities"){
    next();
  } else {
    response.status(404).json("Path requested does not exist");
  }
});

app.get('/cities', function(request, response){
  var cities = ['Caspiana', 'Indigo', 'Paradise'];
  response.json(cities);
});

app.listen(3000);
```
issue a GET request to the /buildings endpoint:

A 404 response with 'Path requested does not exist'
