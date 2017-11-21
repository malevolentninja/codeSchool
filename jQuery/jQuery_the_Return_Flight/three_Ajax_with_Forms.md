# Level Three: Ajax With Forms
Learn about how to send data to the server and work with JSON

### 3.3 Form Submit Event 
Here's a form we used in Try jQuery. 
* As you change the number of nights, we show the updated estimate of the trip cost.
* Let's go ahead and add a listener for submit on the form which will run a function. 
* This function should accept one parameter - the form submission event. 
* Call preventDefault on this event to stop the browser from following the form submission. 
* We'll write the ajax call in this event handler later.

application.js
```sh
$(document).ready(function() {
  $('form').on('submit', function(event) {
    event.preventDefault();
  });
});
```

### 3.4 $.ajax with POST
* We're all set to start handling this form submission using Ajax
* Within the event handler, we'll need to do a few things
* Make an ajax request to the /book URL on the server of type POST
* Also pass in the contents of the form as the form data using serialize


AJAX result
```sh
<p>You have successfully reserved a spot on your trip for 7 nights.</p>
```

application.js
```sh
$(document).ready(function() {
  $('form').on('submit', function(event) {
    event.preventDefault();
    $.ajax('/book', {
      type: 'POST',
      data: $('form').serialize()
    })
  });
});
```

### 3.5 Success Callback 

We check our server and we can see that the form is submitting successfully right now. 
Unfortunately, we're not showing the traveler anything yet!

Add a callback for success that will handle this case. 
Set the html of the .tour element as the result from the ajax request.

application.js
```sh
$(document).ready(function() {
  $('form').on('submit', function(event) {
    event.preventDefault();
    $.ajax('/book', {
      type: 'POST',
      data: $('form').serialize(),
      success: function(response) {
        $('form').remove();
        $('.tour').hide().html(response).fadeIn()
      }
    });
  });
});
```

### 3.7 The JSON Switch 
* Our form is working now! We're able to submit and see a response message from the server. 
* We'd like to tweak this message a little bit, but since we're getting HTML back from the server, it wouldn't be easy. 
* Luckily, we know that our server can also respond with a JSON version of this same response.

* Update our existing $.ajax call to make the request:
* setting the dataType to json
* update the success callback to set the HTML of the .tour element to a message of your choice using:
* the descriptio
* price
* number of nights
* confirmation number



```sh
$(document).ready(function() {
  $('form').on('submit', function(event) {
    event.preventDefault();
    $.ajax('/book', {
      type: 'POST',
      data: $('form').serialize(),
      dataType: 'json',
      success: function(response) {
        $('.tour').html("Description: " + response.description + ". Price: " +
                        response.price + ". Number of Nights " + response.nights +
                        ". Confirmation Number: " + response.confirmation );
      }
    });
  });
});
```

### 3.8 Don't Repeat Yourself 
* Right now we're hardcoding the URL of the form action in two places - in the HTML of the form, and in our $.ajax call.
* Let's update our $.ajax call to use whatever URL the form specifies. 
* Also, update the type of the ajax request to use the method attribute of the form.


```sh
$(document).ready(function() {
  $('form').on('submit', function(event) {
    event.preventDefault();
    $.ajax($('form').attr('action'), {
      type: $('form').attr('method'),
      data: $('form').serialize(),
      dataType: 'json',
      success: function(response) {
        $('.tour').html('<p></p>')
                  .find('p')
                  .append('Trip to '         + response.description)
                  .append(' at $'            + response.price)
                  .append(' for '            + response.nights + ' nights')
                  .append('. Confirmation: ' + response.confirmation);
      }
    });
  });
});
```

#### html
```sh
<div class="tour" data-daily-price="357">
  <h2>Paris, France Tour</h2>
  <p>$<span id="total">2,499</span> for <span id="nights-count">7</span> Nights</p>
  <form action="/book" method="POST">
    <p>
      <label for="nights">Number of Nights</label>
    </p>
    <p>
      <input type="number" name="nights" id="nights" value="7">
    </p>
    <input type="submit" value="book">
  </form>
</div>
```

#### reference.js
```sh

$(document).ready(function() {
  $('#nights').on('keyup', function() {
    var nights = +$(this).val();
    var dailyPrice = +$(this).closest('.tour').data('daily-price');
    $('#total').text(nights * dailyPrice);
    $('#nights-count').text($(this).val());
  });
  $('#nights').on('focus', function() {
    $('#nights').val(7);
  });
});
```
