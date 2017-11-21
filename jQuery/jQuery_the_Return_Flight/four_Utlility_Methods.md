# Level 4: Utility Methods

### 4.3 Using $.each() I 
Our site has a popup deals page. We need to write the javascript that will load the current available deals. Let's start out by looping over the result with the $.each() function. Within this loop, console.log() each item for now to get an idea of what the data looks like.

```sh
$('button').on('click', function() {
  $.ajax('/cities/deals', {
    success: function(response) {
      // your code goes here
      $.each(response, function(index, dealItem) {
        console.log(dealItem);
      })
    }
  });
})
```

### 4.4 Using $.each() II
Ok, now that we can see what our data looks like, lets go ahead and put the data into our html.  
- Use the index within the each loop to locate the deal DOM node to update. 
- Update the name and the price of each deal.

```sh
$('button').on('click', function() {
  $.ajax('/cities/deals', {
    success: function(response) {
      $.each(response, function(index, dealItem) {
        // Your code goes here
        var deal = $('.deal-' + index);
        deal.find('.name').html(dealItem.name);
        deal.find('.price').html(dealItem.price);
      });
    }
  });
});
```

### 4.5 Using $.each() II
Lets clean up our code a bit. 
- This AJAX call is pretty simple, and it only has a success callback
- Use the $.getJSON() function to make the call instead.

```sh
$('button').on('click', function () {
  $.getJSON('/cities/deals', function(response) {
    $.each(response, function (index, dealItem) {
      var deal = $('.deal-' + index);
      deal.find('.name').html(dealItem.name);
      deal.find('.price').html(dealItem.price);
    })
  });
});
```

### 4.6 Using $.map() I 
Someone thought it would be a great idea to have a page which shows flights that are running late. You're going to need to use the $.map() function, lets first console.log() the data being passed to the $.map() callback to see what we're dealing with.
```sh
$('.update-available-flights').on('click', function() {
  $.getJSON('/flights/late', function(response) {
    // Your code goes here
    $.map(response, function(flight, index) {
      console.log(flight);
    })
  });
});
```

### 4.7 Using $.map() II 
Now you need to create the array of html elements. Create an array of li elements, each with the flightNumber and the time from the ajax result. Insert the resulting array into the .flight-times unordered list element.

```sh
$('.update-available-flights').on('click', function() {
  $.getJSON('/flights/late', function(result) {
    var flightElements = $.map(result, function(flightItem, index){
      // Your code goes here
      var flights = $("<li></li>");
      $('<p>Flight Number: ' + flightItem.flightNumber + '</p>').appendTo(flights);
      $('<p>Time: ' + flightItem.time + '</p>').appendTo(flights);
      return flights;
    });
    $('.flight-times').html(flightElements);
  });
});
```

### 4.8 detach() 
Let's take a minute to make our previous code a bit more efficient. 
- Use the .detach() method to remove the .flight-times list element from the DOM 
- Before you insert the new list items with html(flightElements). 
- Then, append the .flight-times element back into the $('.flights') element.

```sh
$('.update-available-flights').on('click', function() {
  $.getJSON('/flights/late', function(result) {
    var flightElements = $.map(result, function(flightItem, index){
      // Your code goes here
      var flights = $("<li></li>");
      $('<p>Flight Number: ' + flightItem.flightNumber + '</p>').appendTo(flights);
      $('<p>Time: ' + flightItem.time + '</p>').appendTo(flights);
      return flights;
    });
    $('.flight-times').detach().html(flightElements).appendTo('.flights');
  });
});
```
