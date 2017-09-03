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
