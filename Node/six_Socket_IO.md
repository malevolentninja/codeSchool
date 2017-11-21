
# Level 6: Socket.io

### 6.2 Setting Up socket.io Server-side

So far we've created an Express server. Now we want to start building a real-time Q&A moderation service and we've decided to use socket.io.

- Using the http module, create an new http server and pass the express app as the listener for that new server.
- Using the socket.io module, listen for requests on the http server. Store the return object of this operation in a variable called io.
- Use the object stored in io to listen for client 'connection' events. Remember, the callback function takes one argument, which is the client object that has connected
- When a new client connects, log a message using console.log().
- Finally, we want to tell our http server to listen to requests on port 8080

app.js
```sh
var express = require('express');
var app = express();
var server = require('http').createServer(app);
var io = require('socket.io')(server);
io.on('connection', function(client){
    console.log(client + "has connected.");
});
server.listen(8080);
```

### 6.3 Client Socket.io Setup
In our html file, load the socket.io.js script and connect to the socket.io server.

- Load the socket.io.js script. The socket.io.js path you should use is '/socket.io/socket.io.js'. Express knows to serve the socket.io client js for this path.
- Using the global io object that's now available for us, connect to the socket.io server at http://localhost:8080.


index.html
```sh
<script src="/socket.io/socket.io.js"></script>
<script>
  // use the socket.io server to connect to localhost:8080 here
  var server = io.connect('http://localhost:8080');
</script>
```


### 6.4 Listening for Questions

- First, listen for 'question' events from the server.
- Now, have the event callback function call the insertQuestion function. The insertQuestion function is already created for you, and it's placed in its own file. It expects exactly one argument - the question.

index.html
```sh
<script src="/socket.io/socket.io.js"></script>
<script src="/insertQuestion.js"></script>

<script>
  var server = io.connect('http://localhost:8080');
server.on('question', function(data){
    insertQuestion(data);
  });
</script>
```

### 6.5 Broadcasting Questions
In the server, listen for 'question' events from clients.
-In the server, listen for 'question' events from clients.
- Now, emit the 'question' event on all the other clients connected, passing them the question data.

app.js
```sh
var express = require('express');
var app = express();
var server = require('http').createServer(app);
var io = require('socket.io')(server);

io.on('connection', function(client) {
  console.log("Client connected...");
   client.on('question', function(question){
    client.broadcast.emit('question', question);
  });

});

server.listen(8080);
```

### 6.6 Saving Client Data

eal-time Q&A app, we want to allow each client only one question at a time, but how do we enforce this rule? We can use socket.io's ability to save data on the client, so whenever a question is asked, we first want to check the question_asked value on the client.

-First, when a client emits a 'question' event, we want to set the value of question_asked to true.
- Second, when a client emits a 'question' event, we want to broadcast that question to the other clients.
- Finally, when a client emits a 'question' event, check to make sure question_asked is not already set to true. We only want to allow one question per user, so make sure that we only set the value of question_asked and broadcast the question to other clients when the value of question_asked is not already true.

app.js
```sh
var express = require('express');
var app = express();
var server = require('http').createServer(app);
var io = require('socket.io')(server);

io.on('connection', function(client) {
  console.log("Client connected...");

  client.on('question', function(question) {
    if(!client.question_asked){
      client.question_asked = true;
    client.broadcast.emit('question', question);
    }
  });
});

server.listen(8080);
```

### 6.7 Answering Questions
Clients can also answer each other's questions, so let's build that feature.

- With the client, listen for the 'answer' event from clients. This listener will have both a question and answer to broadcast so make sure to include both as function parameters.
- Now, emit the 'answer' event on all the other clients connected, passing them the question and answer data.

app.js
```sh
var express = require('express');
var app = express();
var server = require('http').createServer(app);
var io = require('socket.io')(server);

io.sockets.on('connection', function(client) {
  console.log("Client connected...");

  client.on('answer', function(question, answer){
    client.broadcast.emit('answer', question, answer);
  });

  client.on('question', function(question) {
    if(!client.question_asked) {
      client.question_asked = true;
      client.broadcast.emit('question', question);
    }
  });
});

server.listen(8080);
```

### 6.8 Answering Question Client

- Listen for the 'answer' event off of the server
- Call the answerQuestion function, passing in both the question and the answer that was broadcast from the server

app.js
```sh
<script src="/socket.io/socket.io.js"></script>

<script>
  var server = io.connect('http://localhost:8080');

  server.on('question', function(question) {
    insertQuestion(question);
  });

   server.on('answer', function(question, answer){
    answerQuestion(question, answer);
  });
  //Don't worry about these methods, just assume
  //they insert the correct html into the DOM
  // var insertQuestion = function(question) {
  // }

  // var answerQuestion = function(question, answer) {
  // }
</script>
```
