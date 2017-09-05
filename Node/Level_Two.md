# Level Two: Events


## 2.2 Chat Emitter
- Create a new EventEmitter object and assign it to a variable called 'chat'.
- Next, let's listen for the 'message' event on our new chat object. Remember to add a callback that accepts the message parameter.
-Log the message to the console using console.log().

```sh
var events = require('events');
var EventEmitter = events.EventEmitter;
var logger = new EventEmitter();
logger.on('message', function(message){
  console.log("ERR: " + message);
});
```

## 2.3 Emitting Events

- On the chat object, emit the 'join' event and pass in a custom message as a string.
- Now emit the 'message' event on the chat object. Just like before, remember to pass in a custom message as a string.

```sh
var events = require('events');
var EventEmitter = events.EventEmitter;

var chat = new EventEmitter();
var users = [], chatlog = [];

chat.on('message', function(message) {
  chatlog.push(message);
});

chat.on('join', function(nickname) {
  users.push(nickname);
});

// Emit events here
chat.emit('join', "Hello");
chat.emit('message', "Message:");
```

## 2.4 Request Event
- Add an event listener on the server variable that listens to the request event. The event listener should take a callback function with two arguments, request and response.
- Move the logic for handling the request from the http.createServer() callback to your new 'request' event listener. Remember to remove the http.createServer() callback once the code has been moved.
- Remove the original request callback

```sh
var http = require('http');

var server = http.createServer();
server.on('request', function(request, response){
  response.writeHead(200);
  response.write("Hello, this is dog");
  response.end();
});


server.listen(8080);
```

## 2.5 Listening Twice

- Add a second 'request' handler to the HTTP server.
- From inside of the new handler, log the message "New request coming in..." using console.log().

```sh
var http = require('http');

var server = http.createServer();
server.on('request', function(request, response) {
  response.writeHead(200);
  response.write("Hello, this is dog");
  response.end();
});
  server.on('request', function(request, response){
  console.log("New request coming in...");
});

server.listen(8080);
```

## 2.6 Listening for Close

- Listen for the 'close' event on the server. The event listener should take a callback function that accepts no arguments.
- Inside the 'close' callback, log the message "Closing down the server...".

```sh
var http = require('http');
var server = http.createServer();

server.on('request', function(request, response) {
  response.writeHead(200);
  response.write("Hello, this is dog");
  response.end();
});

server.on('request', function(request, response) {
  console.log("New request coming in...");
});

server.on('close', function(){
  console.log("Closing down the server...");
});


server.listen(8080);
```
