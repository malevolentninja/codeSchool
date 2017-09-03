## 1.2 Hello You
- First, tell the response which status it should have (a successful status is 200).
- Next, write a message to the response body in the form of "Hello, this is <your name here>".
- To finish it up, tell the response to end so the client on the other side knows it has received all the data.

```sh  
var http = require('http');
http.createServer(function(request, response) {
    response.writeHead(200);
    response.write("Hello, this is blondie");
    response.end();
}).listen(8080);     
```

## 1.3 Convert Blocking
- Start by changing the call from readFileSync() to readFile().
- Next, add a callback method to the readFile() call. This method should accept error and contents parameters.
- To finish it up, remove the contents var declaration, and move the call to console.log() inside your callback.
```sh
var fs = require('fs');
fs.readFile('index.html', function(err, contents) {
  console.log(contents);
});

var http = require('http');
var fs = require('fs');
http.createServer(function(request, response) {
  response.writeHead(200);
 fs.readFile('index.html', function(err, contents){
    response.write(contents);
    response.end();
  });}).listen(8080);
```

## 1.4 Running your code

Run that file we just created to read a file off the filesystem
```sh
node file_read.js
<html><p>Hello, this is Dog</p></html>
```

 ## 1.5 Read file in server

- After response.writeHead(200), add a call to fs.readFile() that reads index.html asynchronously. Remember to pass a callback function, that accepts an error parameter, and a contents parameter.
- Now that you have the file contents, write it to the response.
- To finish up, end the response after the file contents have been written.

```sh
var http = require('http');
var fs = require('fs');
http.createServer(function(request, response) {
  response.writeHead(200);
 fs.readFile('index.html', function(err, contents){
    response.write(contents);
    response.end();
  });}).listen(8080);
```

## 1.6 Issuing a request
- in the terminal below use curl
```sh
$ curl http://localhost:8080
```



## 1.7 Writing response headers
- take additional parameters of response.writeHead()function
```sh
var http = require('http');
var fs = require('fs');
http.createServer(function(request, response) {
  response.writeHead(200, {
    'Content-Type': 'text/html'
  });
    fs.readFile('index.html', function(err, contents) {
    response.write(contents);
    response.end();
  });
  }).listen(8080);
  ```

  ## 1.8

  - Instead of passing the content to response.write(), pass it to response.end().
  -Now, remove the call to response.write().

```sh
var http = require('http');
http.createServer(function(request, response) {
  response.writeHead(200);
  response.end("Hello, this is dog");
}).listen(8080);
```

