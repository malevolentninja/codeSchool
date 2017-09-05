# Level Three: Streams


## 3.2 File Read Stream

- Use the fs module to create a Readable stream for fruits.txt. Store the new stream in a variable called file.
-Next, listen to the readable event on the newly created stream and give it a callback.
- Inside the callback, read the data chunks from the stream and print them to the console using console.log() - you might want to use a while loop to do this. Don't forget to call toString() on the data before printing it.

```sh
var fs = require('fs');
var file = fs.createReadStream('fruits.txt');

file.on('readable', function(){
  while(null !== (chunk = file.read())){
    console.log(chunk.toString());
  }
});
var fs = require('fs');
```

## 3.3 File Piping

- Start by removing the code for the readable handler.
- Call file.pipe(), passing it the stream to write to


```sh
var fs = require('fs');

var file = fs.createReadStream('fruits.txt');
file.pipe(process.stdout);
```

## 3.4 Fixing Pipe

- You'll need to consult the pipe documentation to figure out the option which keeps the Write stream open and dispatches the end event.

## 3.5 Download Server

- Use pipe() to send index.html to the response.

```sh
var fs = require('fs');
var http = require('http');

http.createServer(function(request, response) {
  response.writeHead(200, {'Content-Type': 'text/html'});

  var file = fs.createReadStream('index.html');
  file.pipe(response);
}).listen(8080);
```
