
# Level 4: Modules

### 4.2 Missing Exports

Add the proper exports line to have a successful high five!

high_five.js
```sh
var highfive = function() {
  console.log("smack!!");
};
module.exports = highfive;
```

app.js
```sh
var highfive = require('./high_five.js');
highfive();
```

### 4.3 Export a Function

- Move the myRequest function and the http require into my_request.js
- Export the myRequest function.
- Require the my_request.js module in app.js.

 app.js
 ```sh
 var myRequest = require('./my_request');

myRequest('Hello, this is dog.');
```

my_request.js
```sh
var http = require('http');
var myRequest = function(message) {
  var request = http.request('http://codeschool.com', function(response) {
    response.pipe(process.stdout, { end: false });
  });

  request.write(message);
  request.end();
};
module.exports = myRequest;
```

### 4.4 Exporting An object
- In the logger.js file, export the info function so we can use it in app.js by assigning it to the exports object.
- In the logger.js file, export the warn function so we can use it in app.js by assigning it to the exports object.
-In the logger.js file, export the error function so we can use it in app.js by assigning it to the exports object.

app.js
```sh
var logger = require('./logger');

logger.info('This is some information');
logger.warn('something bad is happening');
```

logger.js
```sh
exports.info = function(message) {
  console.log("Info: " + message);
};

exports.warn = function(message) {
  console.log("Warning: " + message);
};

exports.error = function(message) {
  console.log("Error: " + message);
};
```

### 4.5 Install Local Modules
install npm module underscore using npm install command
```sh
$ npm install underscore
npm http GET https://registry.npmjs.org/underscore
npm http 200 https://registry.npmjs.org/underscore
underscore@1.7.0 node_modules/underscore
```

### 4.6 Install Global Modules
```sh
$ npm install coffee-script -g
npm http GET https://registry.npmjs.org/coffee-script
npm http 200 https://registry.npmjs.org/coffee-script
npm http GET https://registry.npmjs.org/coffee-script/-/coffee-script-1.8.0.tgz
npm http 200 https://registry.npmjs.org/coffee-script/-/coffee-script-1.8.0.tgz
npm http GET https://registry.npmjs.org/mkdirp
npm http 200 https://registry.npmjs.org/mkdirp
coffee-script@1.8.0 /node_modules/coffee-script
└── mkdirp@0.3.5
```sh

### 4.7 Dependency
- Add the connect dependency to package.json
- Add the underscore dependency to package.json

package.json
```sh
{
  "name": "My Awesome Node App",
  "version": "1",
  "dependencies": {
    "connect": "2.1.1",
    "underscore": "1.3.3"
  }
}
```

### 4.8 Semantic Versioning

- Update the connect version on package.json to fetch the latest patch-level changes. All we have to do is add one character to the beginning of the version number.
- Now update the underscore version on package.json to fetch the latest patch-level changes. Again, all we have to do is add one character to the beginning of the version number.

package.json
```sh
{
  "name": "My Awesome Node App",
  "version": "1",
  "dependencies": {
    "connect": "~2.2.1",
    "underscore": "~1.3.3"
  }
}
```
