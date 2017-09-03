# CoffeeScript Level One


### 1.1 Variable assignment

Assign your name as a string value to a variable named person.

``` sh 
person = 'Rick'
```

live javaScript file
``` sh 
var person;
person = 'Rick';
```


### 1.2 Functions

Define a function named greet that takes no argument and alerts 'Hello CoffeeScript'
``` sh 
greet = ->
    alert 'Hello CoffeeScript'
```

live javaScript file
``` sh 
var greet;
greet = function() {
  return alert('Hello CoffeeScript');
};
```

### 1.3 Function II

``` sh 
greet = ->
  alert "Hello CoffeeScript"

Given the greet function, change it so that it accepts a single argument and prints out the value inside the alert.

greet = (message) ->
    alert message

live js
var greet;
greet = function(message) {
  return alert(message);
};
```

### 1.4 Functions III

``` sh 
greet = (message) ->
  alert message
```

Given the code, change the greet function so that it accepts two arguments instead of just one. It should alert both arguments, separated by a single white space.

``` sh 
greet = (message, other) ->
    alert message + ' ' answer
```

live JavaScript file
``` sh 
var greet;
greet = function(message) {
  return alert(message);
};
```

### 1.5 Functions IV

``` sh 
greet = (name) -> alert name
```

Change the greet function so that it uses a default value of 'Stranger' for the name parameter
``` sh 
greet = (name='Stranger') -> alert name
```

live javaScript file
``` sh 
var greet;
greet = function(name) {
  if (name == null) {
    name = 'Stranger';
  }
  return alert(name);
};
```

### 1.6 Functions V

``` sh 
greet = (name='Stranger') ->
  "Hello, " + name  
```

Change the greet function so that it uses CoffeeScript-style string interpolation.
``` sh 
greet = (name='Stranger') ->
    "Hello, #{name}"
```


live js
``` sh 
var greet;
greet = function(name) {
  if (name == null) {
    name = 'Stranger';
  }
  return "Hello, " + name;
};
```

### 1.7 Sum Function
Create a function named sum that takes two numbers as arguments and returns the sum of those numbers
``` sh 
sum = (num1, num2) ->
    num1 + num2

```

live javaScript file

``` sh 
var sum;
sum = function(num1, num2) {
  return num1 + num2;
};
```
