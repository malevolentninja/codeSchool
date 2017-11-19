# Level 3: User Params(8)
Reading user-submitted parameters.

### 3.2 City search
- Create a new route for GET requests to '/cities'. The second argument should be a callback function which takes request and response.
- From inside of our route, create an if statement that checks whether a value is set to the query string parameter search.
- Inside of the if block, call the citySearch() function, passing in the user submitted parameter for search. Then return the result of the function as a JSON response

app.js
```sh
var express = require('express');
var app = express();

var cities = ['Caspiana', 'Indigo', 'Paradise'];

app.get('/cities', function (request, response) {
  if(request.query.search){
    response.json(citySearch(request.query.search));
  }
});

function citySearch (keyword) {
  var regexp = RegExp(keyword, 'i');
  var result = cities.filter(function (city) {
    return city.match(regexp);
  });

  return result;
}

app.listen(3000);
```


### 3.3 Dynamic Route Variables

```sh
app.get('/cities/:name', function (request, response) {
  // ...
})
```
When requests come in for this route, how can we access the city name submitted by the user?
```sh
request.params.name
```

### 3.4 City Information

- Inside of our dynamic route, grab the name submitted by the user, lookup the city information on the cities object and assign it to the cityInfo variable.
- Check to see if cityInfo exists and if so, respond with the cityInfo in JSON format.
- If cityInfo does not exist, respond with a 404 HTTP status code and a JSON message that says "City not found".

```sh
var express = require('express');
var app = express();

var cities = {
  'Lotopia': 'Rough and mountainous',
  'Caspiana': 'Sky-top island',
  'Indigo': 'Vibrant and thriving',
  'Paradise': 'Lush, green plantation',
  'Flotilla': 'Bustling urban oasis'
};

app.get('/cities/:name', function (request, response) {
  var cityInfo = cities[request.params.name];
if (cityInfo) {
  response.json(cityInfo);
} else {
  response.status(404).json('City not found');
}
});

app.listen(3000);
```

### 3.6 Flexible Routes
Our current route only works when the city name argument matches exactly the properties in the cities object. This is a problem. We need a way to make our code more flexible.

- Inside our route, call the parseCityName() function passing in the name parameter. Assign the return value to the new variable called cityName.
-  Now, using the city name returned from the parseCityName() function, lookup the corresponding description using the cities object and store it in the correct variable that will make the rest of the function work as intended.

app.js
```sh
var express = require('express');
var app = express();

var cities = {
  'Lotopia': 'Rough and mountainous',
  'Caspiana': 'Sky-top island',
  'Indigo': 'Vibrant and thriving',
  'Paradise': 'Lush, green plantation',
  'Flotilla': 'Bustling urban oasis'
};

app.get('/cities/:name', function (request, response) {
  var cityName = parseCityName(request.params.name);
  var cityInfo = cities[cityName];
  if (cityInfo) {
    response.json(cityInfo);
  } else {
    response.status(404).json('City not found');
  }
});

function parseCityName(name) {
  var parsedName = name[0].toUpperCase() + name.slice(1).toLowerCase();
  return parsedName;
}

app.listen(3000);

```

### 3.7 Dynamic Routes I
Which Express function maps placeholders to callback functions, and is commonly used for running pre-conditions on Dynamic Routes?
```sh
app.param()
```

### 3.8 Dynamic Routes II
Whenever we use our name parameter we want to parse it a specific way. Let's clean up our existing code so that all routes with a name parameter get the same special handling.

-  Call app.param() to intercept requests that contain an argument called 'name'. Remember app.param() takes a callback function as its second argument, which uses the same signature as a middleware.
- Inside the app.param() callback function, call the parseCityName() function with the submitted name parameter. Set the return value to a new property in the request object called cityName.
-  Finally, call a function that moves processing to the next function in the stack.


app.js
```sh
var express = require('express');
var app = express();

var cities = {
  'Lotopia': 'Rough and mountainous',
  'Caspiana': 'Sky-top island',
  'Indigo': 'Vibrant and thriving',
  'Paradise': 'Lush, green plantation',
  'Flotilla': 'Bustling urban oasis'
};

app.param('name', function (request, response, next) {
  request.cityName = parseCityName(request.params.name);
  next();
});

app.get('/cities/:name', function (request, response) {
  var cityInfo = cities[request.cityName];
  if(cityInfo) {
    response.json(cityInfo);  
  } else {
    response.status(404).json("City not found");
  }
});

function parseCityName(name){
  var parsedName = name[0].toUpperCase() + name.slice(1).toLowerCase();
  return parsedName;
}

app.listen(3000);
```


### 3.9 Dynamic Routes III

- Call a function that intercepts Dynamic Routes with the 'year' param.
- Inside of that function, use the isYearFormat() function to check whether the year parameter is in a valid format. If so, then move processing to the next function in the stack.
-If the year parameter is not in a valid format, then respond with a 400 HTTP status code and a JSON message 'Invalid Format for Year'.

app.js
```sh
var express = require('express');
var app = express();
app.param('year', function(request, response, next) {
  if(isYearFormat(request.params.year)) {
    next();
  }
  else {
   response.status(400).json('Invalid Format for Year');
  }
});

var citiesYear = {
  5000: 'Lotopia',
  5100: 'Caspiana',
  5105: 'Indigo',
  6000: 'Paradise',
  7000: 'Flotilla'
};

function isYearFormat(value) {
  var regexp = RegExp(/^d{4}$/);
  return regexp.test(value);
}

app.get('/cities/year/:year', function(request, response) {
  var year = request.params.year;
  var city = citiesYear[year];

  if(!city) {
    response.status(404).json("No City found for given year");
  } else {
    response.json("In " + year + ", " + city + " is created.");
  }
});

app.listen(3000);
```

### 3.10 Dynamic Routes IV

```sh
var express = require('express');
  var app = express();

  app.param('year', function(request, response, next) {
    if(isYearFormat(request.params.year)) {
      next();
    } else {
      response.status(400).json('Invalid Format for Year');
    }
  });

  var citiesYear = {
    5000: 'Lotopia',
    5100: 'Caspiana',
    5100: 'Indigo',
    6000: 'Paradise',
    7000: 'Flotilla'
  };

  function isYearFormat(value) {
    var regexp = RegExp(/^\d{4}$/);
    return regexp.test(value);
  }

  app.get('/cities/year/:year', function(request, response) {
    var year = request.params.year;
    var city = citiesYear[year];

    if(!city) {
      response.status(404).json("No City found for given year");
    } else {
      response.json("In " + year + ", " + city + " is created.");
    }

  });

  app.listen(3000);
```
With the proper validations in place for the following code, what would the output be for a GET request to /cities/year/500?

400 invalid Format for Year
