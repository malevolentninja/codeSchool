# CoffeScript Level Two



### 2.1 JavaScript to CoffeeScript Part I

```sh 
# jQuery(function($) {
#   $('#newCoffee a').click(function() {
#     alert('New coffee added');
#   });
# });
```

convert the commented jQuery code to CoffeeScript
``` sh 
$ ->
    $('#newCoffee a').click ->
        alert 'New coffee added'
```

live javaScript file

```sh
$(function() {
  return $('#newCoffee a').click(function() {
    return alert('New coffee added');
  });
});
```

### 2.2 JS to CS Part II

```sh 
# $('#newCoffee a').click(function() {
#   var name = prompt('Name of coffee:');
#   alert("New coffee added: " + name);
# })
```

Convert the commented jQuery code  to CoffeeScript and use CoffeeScript-style string interpolation.
```sh 
$('#newCoffee a').click ->
    name = prompt 'Name of coffee:'
    alert 'New coffee added: #{name}'
```

live javaScript file

```sh
$('#newCoffee a').click(function() {
  var name;
  name = prompt('Name of coffee:');
  return alert('New coffee added: #{name}');
});
```

### 2.3 JS to CS Part III

```sh 
# $('#newCoffee a').click(function() {
#   var coffee, name;
#   name = prompt('Name of coffee:');
#   coffee = $("<li>" + name + "</li>");
#   $('ul.drink').append(coffee);
# });
```

Convert the commented jQuery to CoffeeScript and use CoffeeScript-style string interpolation.

```sh 
$('#newCoffee a').click ->
    name = prompt 'Name of coffee:'
    coffee = $("<li> #{name} </li>")
    $('ul.drink').append coffee
```

live javaScript file

```sh
$('#newCoffee a').click(function() {
  var coffee, name;
  name = prompt('Name of coffee:');
  coffee = $("<li> " + name + " </li>");
  return $('ul.drink').append(coffee);
});
```

2.4 JS to CS Part IV

```sh 
# $('.drink li a').click(function(e) {
#   e.preventDefault();
#   alert($(this).text());
# });
```

Convert the commented jQuery code to CoffeeScript. Use @ instead of this.

```sh 
$('.drink li a').click (e) ->
    e.preventDefault()
    alert $(@).text()
```

live javaScript file

```sh
$('.drink li a').click(function(e) {
  e.preventDefault();
  return alert($(this).text());
});
```

### 2.5 JS to CS Part V

```sh 
# $('.drink li').mouseenter(function() {
#   $(this).find('span').show();
# });
# $('.drink li').mouseleave(function() {
#   $(this).find('span').hide();
# });
```

Convert the commented jQuery code to CoffeeScript

$('.drink li').mouseenter ->
    $(@).find('span').show()
$('.drink li').mouseleave ->
    $(@).find('span').hide()
```

live javaScript file

```sh
$('.drink li').mouseenter(function() {
  return $(this).find('span').show();
});
$('.drink li').mouseleave(function() {
  return $(this).find('span').hide();
});
```

### 2.6 JS to CS Part VI

```sh 
# $('.drink li').hover(function() {
#   $(this).find('span').show();
# }, function() {
#   $(this).find('span').hide();
# });
```

Convert the commented jQuery code to CoffeeScript


```sh
$('.drink li').hover(
  ->
   $(@).find('span').show();
  ->
   $(@).find('span').hide();
)
```

live javaScript file

```sh
$('.drink li').hover(function() {
  return $(this).find('span').show();
}, function() {
  return $(this).find('span').hide();
});
```


 
