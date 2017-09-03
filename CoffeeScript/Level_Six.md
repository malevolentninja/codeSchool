# CoffeeScript Level Six: Object Orientation

### 6.1 Classes Part 1

``` sh 
coffee =
  name: 'Russian'
  level: 2
  isRussian: -> @name is 'Russian'
```

Create a Coffee class that will produce coffee objects. In that class, create a constructor that takes name and level as arguments and sets them as instance variables. Also, make sure you create a function called isRussian.
``` sh 
class Coffee
    constructor: (name, level) ->
        @name = name
        @level = level
    isRussian: -> @name is 'Russian'
```

#### Live javaScript

``` sh 
var Coffee;
Coffee = (function() {
  function Coffee(name, level) {
    this.name = name;
    this.level = level;
  }
  Coffee.prototype.isRussian = function() {
    return this.name === 'Russian';
  };
  return Coffee;
})();
```

### 6.2 Classes - Part II

For an already existing Coffee class, create a new coffee object passing in your name (string) and any number (as the level), then assign it to a variable named coffee.
``` sh 
coffee = new Coffee('Preigile', 6)
```

#### Live javaScript

``` sh 
var coffee;
coffee = new Coffee('Preigile', 6);
```

### 6.3 property arguments

``` sh 
class Coffee
  constructor: (name, level) ->
    @name = name
    @level = level or 0

  isRussian: -> @name is 'Russian'
```
Refactor the constructor to use property arguments. Also, set @level to be an optional argument by setting its default value to 0.

``` sh 
class Coffee
    constructor: (@name, @level=0) ->
    isRussian: -> @name is 'Russian'
```

#### Live javaScript

``` sh 
var Coffee;
Coffee = (function () {
    function Coffee(name, level) {
        this.name = name;
        this.level = level != null ? level : 0;
    }

    Coffee.prototype.isRussian = function () {
        return this.name === 'Russian';
    };
    return Coffee;
})();
```

### 6.4 class inheritance

``` sh 
class Coffee
  constructor: (@name, @level=0) ->
```

Make the Coffee class inherit from Drink and override the serve method to return false if @sleeve is false, otherwise invoke the superclass method.

``` sh 
Firstly added drink class:
Class  Drink
    sleeve :  null
    serve :  - >
        alert ( ' Pouring drink ' )
```

Then moved on to creating the conditions required
``` sh 
class Coffee extends Drink
    constructor: (@name, @level=0) ->
    serve: ->
        return false if @sleeve is not on
        super()
```

#### Live javaScript

``` sh 
var Coffee;
var __hasProp = Object.prototype.hasOwnProperty, __extends = function (child, parent) {
    for (var key in parent) {
        if (__hasProp.call(parent, key)) child[key] = parent[key];
    }
    function ctor() {
        this.constructor = child;
    }

    ctor.prototype = parent.prototype;
    child.prototype = new ctor;
    child.__super__ = parent.prototype;
    return child;
};
Coffee = (function () {
    __extends(Coffee, Drink);
    function Coffee(name, level) {
        this.name = name;
        this.level = level != null ? level : 0;
    }

    Coffee.prototype.serve = function () {
        if (this.sleeve === !true) {
            return false;
        }
        return Coffee.__super__.serve.call(this);
    };
    return Coffee;
})();
```

### 6.5 classes with jquery

``` sh 
class DrinkLink
  watchClick: ->
```

On the DrinkLink class  implement the watchClick method so that when any link is clicked, its color is changed to #F00.
``` sh 
class DrinkLink
    watchClick: ->
        $(a).click ->
            $(@).css('color: #F00')
```

#### Live javaScript
``` sh 
var DrinkLink;
DrinkLink = (function () {
    function DrinkLink() {
    }

    DrinkLink.prototype.watchClick = function () {
        return $(a).click(function () {
            return $(this).css('color: #F00');
        });
    };
    return DrinkLink;
})();
```

### 6.6 Watch those @'s

``` sh 
class DrinkLink
  constructor: (@linkClicked=false) ->
  watchClick: ->
    $('.drink a').click (event) ->
      $(event.target).css('color', '#F00')
      @linkClicked = true
```
Fix the bug on the code, which is causing the @linkClicked variable to not be properly set when a link is clicked.

``` sh 
class DrinkLink
    constructor: (@linkClicked=false) ->
    watchClick: ->
        $('.drink a').click (event) =>
            $(event.target).css('color', '#F00')
            @linkClicked = true
```
#### Live javaScript

``` sh 
var DrinkLink;
var __bind = function (fn, me) {
    return function () {
        return fn.apply(me, arguments);
    };
};

DrinkLink = (function () {
    function DrinkLink(linkClicked) {
        this.linkClicked = linkClicked != null ? linkClicked : false;
    }

    DrinkLink.prototype.watchClick = function () {
        return $('.drink a').click(__bind(function (event) {
            $(event.target).css('color', '#F00');
            return this.linkClicked = true;
        }, this));
    };
    return DrinkLink;
})();
```
