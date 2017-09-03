# CoffeeScript Level Four




### 4.1 coffee on the range

Create an array with numbers 1 until 10 using the inclusive (two dot) range syntax.

```sh
range = [1..10]
```

#### Live javaScript

```sh
var range = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```


 ### 4.2 coffee on the range II

Create an array with numbers 1 through 10 using the exclusive range syntax.

```sh
range = [1...11]
```

#### Live javaScript
```sh
var range = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### 4.3

Create a variable named coffee which is an object with a name property set to 'Russian', a level property set to 2 and 
an isRussian property which holds a function that returns true. 
Use an object literal.

```sh
coffee =
    name: 'Russian'
    level: 2
    isRussian: -> true
```

#### Live javaScript

```sh
var coffee;
coffee = {
    name: 'Russian',
    level: 2,
    isRussian: function () {
        return true;
    }
};
```

### 4.4 for in loop

Using the for element in collection loop, iterate over the people collection and 
print the names of people over 18 years old (person.age > 18).
Use the console.log function to print the person.name.

```sh
for person in people
    console.log person.name if person.age > 18
```

#### Live javaScript

```sh
var person, _i, _len;
for (_i = 0, _len = people.length; _i < _len; _i++) {
    person = people[_i];
    if (person.age > 18) {
        console.log(person.name);
    }
}
```

### 4.5 list comprehension
```sh
 for person in people
  console.log(person.name) if person.age > 18

 Modify the loop to use a list comprehension.
for person in people
```

```sh
console.log(person.name) if person.age > 18

console.log(person.name) for person in people when person.age > 18
```

#### Live javaScript

```sh
var person, _i, _len;
for (_i = 0, _len = people.length; _i < _len; _i++) {
  person = people[_i];
  if (person.age > 18) {
    console.log(person.name);
  }
}
```

4.6 List Comprehension II

```sh
for coffee in coffeeList
    if not coffee.isRussian?()
        addCoffee(coffee)
```

Refactor the code to make use of list comprehension

```sh
addCoffee(coffee) for coffee in coffeeList when not coffee.isRussian?()
```

#### Live javaScript
```sh
var coffee, _i, _len;
for (_i = 0, _len = coffeeList.length; _i < _len; _i++) {
    coffee = coffeeList[_i];
    if (!(typeof coffee.isRussian === "function" ? coffee.isRussian() : void 0)) {
        addCoffee(coffee);
    }
}
```

4.7 Splat Arguments

```sh
displayTopPicks = (bestCoffee, suggested) ->
  alert('Top #1 ' + bestCoffee)
  alert('Suggested: ' + suggested)
```
Change the displayTopPicks function to accept a variable number of suggested coffees by using the splat operator. Use suggested.join(", ") to alert all of the suggested coffees.

```sh
displayTopPicks = (bestCoffee, suggested...) ->
    alert('Top #1 ' + bestCoffee)
    alert('Suggested: ' + suggested.join ", ")
```

 #### Live javaScript
 ```sh
    var displayTopPicks;
var __slice = Array.prototype.slice;
displayTopPicks = function() {
  var bestCoffee, suggested;
  bestCoffee = arguments[0], suggested = 2 <= arguments.length ? __slice.call(arguments, 1) : [];
  alert('Top #1 ' + bestCoffee);
  return alert('Suggested: ' + suggested.join(", "));
};
```
