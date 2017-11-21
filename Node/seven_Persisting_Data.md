
# Level 7: Persisting Data

### 7.2 Simple Redis Commands
Let's start practicing using the redis key-value store from our node application.

- Require the redis module and assign it to a variable called redis.
- Create a redis client and assign it to a variable called client.
- On the client, set the name property to your name

app.js
```sh
var redis = require('redis');
var client = redis.createClient();
client.set('name', 'Answer');
```

### 7.3 Get A Key

- Use the redis client to issue a get command using the 'question' key to retrieve a value. Remember, the get function takes a callback which expects two arguments, error and data.
-Log the value retrieved with console.log.

```sh
var redis = require('redis');
var client = redis.createClient();
client.get('question', function(err, data){
  console.log(data);
});
```

### 7.4 Working with Lists 1
- Using the redis client's lpush command, insert question1 into the questions list. Then, console.log the result you receive. Remember, the lpush function takes a callback as its last argument, which expects an error and value to be passed as arguments.
- Using the redis client's lpush command, insert question2 into the questions list. Then console.log the result you receive.

app.js
```sh
var redis = require('redis');
var client = redis.createClient();

var question1 = "Where is the dog?";
var question2 = "Where is the cat?";
client.lpush('questions', question1, function(err, data){
    console.log(data);
});

client.lpush('questions', question2, function(err, data){
    console.log(data);
});
```

### 7.5 Working with Lists 2

- Use the lrange() command to return all of the items from the questions key.
- Now that we have called lrange(), use console.log to log the result from redis.

app.js
```sh
var redis = require('redis');
var client = redis.createClient();
client.lrange('questions', 0, -1, function(err, data){
  console.log(data);
});
```

### 7.6 Persisting Questions

- Use the lpush command to add new questions to the list named questions. Do this inside the listener for the 'question' event.

app.js
```sh
var express = require('express');
var app = express();
var server = require('http').createServer(app);
var socket = require('socket.io');
var io = socket.listen(server);

var redis = require('redis');
var redisClient = redis.createClient();

io.sockets.on('connection', function(client) {
  client.on('answer', function(question, answer) {
    client.broadcast.emit('answer', question, answer);
  });

  client.on('question', function(question) {
    if(!client.question_asked) {
      client.question_asked = true;
      client.broadcast.emit('question', question);
      redisClient.lpush('questions', question);// add the question to the list here

    }
  });
});
```


### 7.7 Emitting Stored Questions

-Use the lrange command to retrieve a list of questions that represent the questions list within redis.
- Inside of the lrange callback, use a forEach loop to iterate through the questions and emit() each question to the client. Remember, don't use broadcast.emit because we only want to send the questions to the client that is connecting to the server.

app.js
```sh
var express = require('express');
var app = express();
var server = require('http').createServer(app);
var io = require('socket.io').listen(server);

var redis = require('redis');
var redisClient = redis.createClient();

io.sockets.on('connection', function(client) {
  redisClient.lrange('questions', 0, -1, function(err, questions){
    questions.forEach(function(question){
      client.emit("question", question);
    });
  });
  client.on('answer', function(question, answer) {
    client.broadcast.emit('answer', question, answer);
  });

  client.on('question', function(question) {
    if(!client.question_asked) {
      client.question_asked = true;
      client.broadcast.emit('question', question);
      redisClient.lpush("questions", question);
    }
  });
});
```

### 7.8 Limiting Questions Stored

- Add a callback to lpush that will be used to limit the size of the list down to a max of 20.
- Use the ltrim command to limit the size of the list stored within redis to a maximum size of 20.


app.js
```sh
var express = require('express');
var app = express();
var server = require('http').createServer(app);
var io = require('socket.io').listen(server);

var redis = require('redis');
var redisClient = redis.createClient();

io.sockets.on('connection', function(client) {
  redisClient.lrange("questions", 0, -1, function(err, questions) {
    questions.forEach(function(question) {
      client.emit("question", question);
    });
  });

  client.on('answer', function(question, answer) {
    client.broadcast.emit('answer', question, answer);
  });

  client.on('question', function(question) {
    if(!client.question_asked) {
      client.question_asked = true;
      client.broadcast.emit('question', question);
      redisClient.lpush("questions", question, function(){
        redisClient.ltrim('questions', 0, 19);
      });
    }
  });

});
```
