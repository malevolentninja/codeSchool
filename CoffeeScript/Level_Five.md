# CoffeeScript Level Five: Applied jQuery II

### 5.1 jQuery and Object notation

``` sh 
# jQuery(function($){
#   $('.drink a').click(function(){
#     var newStyle = {
#       'color': '#F00',
#       'font-weight': 'bold'
#     };
#     $(this).css(newStyle)
#   });
# });
```

Convert jQuery code to coffescript

``` sh 
$ ->
    $('.drink a').click ->
        newStyle =
            'color': '#F00'
            'font-weight': 'bold'
        $(@).css newStyle
```

### 5.2 jQuery and Object notation part 2

``` sh 
$('.drink a').click (e) ->
  e.preventDefault()
  alert $(@).text()
```

Wrap the  code into an init function that belongs to a new object named coffeeList. After defining coffeeList, invoke the coffeeList.init function.

``` sh 
coffeeList =
    init: ->
        $('.drink a').click (e) ->
            e.preventDefault()
            alert $(@).text()

coffeeList.init()
```

#### Live javaScript
``` sh 
var coffeeList;
coffeeList = {
  init: function() {
    return $('.drink a').click(function(e) {
      e.preventDefault();
      return alert($(this).text());
    });
  }
};
coffeeList.init();
```

### 5.3 jQuery and objection notation part 3

``` sh 
# $.ajax({
#   url: '/coffeeList',
#   method: 'GET',
#   success: function(results) {
#     var i = null
#       , coffee = null;
#     for (i = 0; i < results.length; i++) {
#       coffee = results[i];
#       if (coffee.level > 3) {
#         $('ul.drink').append("<li>" + coffee.name + "</li>")
#       }
#     }
#   },
#   error: function(results) {
#     alert("failure " + results);
#   }
# });
```

Convert the existing JavaScript code to CoffeeScript. Make sure you replace the for loop with a list comprehension.

``` sh 
$.ajax
  url: '/coffeeList'
  method: 'GET',
  success: (results) ->
    $('ul.drink').append("<li>#{coffee.name}</li>") for coffee in results when coffee.level > 3
  error: (results) ->
    alert "failure #{results}"
```

#### Live javaScript
    
``` sh     
$.ajax({
  url: '/coffeeList',
  method: 'GET',
  success: function(results) {
    var coffee, _i, _len, _results;
    _results = [];
    for (_i = 0, _len = results.length; _i < _len; _i++) {
      coffee = results[_i];
      if (coffee.level > 3) {
        _results.push($('ul.drink').append("<li>" + coffee.name + "</li>"));
      }
    }
    return _results;
  },
  error: function(results) {
    return alert("failure " + results);
  }
});
```
