# Level One: Ajax Basics

### 1.3 Ajax 
* In the Try jQuery course, we learned how to slideDown() content based on a mouse click event
* But that was for content that was already loaded in the HTML
* Now, let's refactor that code to fetch and show the content using Ajax

* To get started, make an $.ajax request for the /photos.html URL inside the existing event handler
* Don't worry about handling the success or error cases yet

```sh
$(document).ready(function () {
    $('#tour').on('click', 'button', function () {
        $.ajax('/photos.html', {})
    });
});
```

### 1.4 Ajax with Response 

Now that we're making an Ajax request to the server, we need to do something with the response.
Add a success callback handler to the $.ajax call that will take the .photos element and insert the contents of the response into the html() method. 
Then call fadeIn() on it so that it will appear on the screen.


```
$(document).ready(function () {
    $('#tour').on('click', 'button', function () {
       $.ajax('/photos.html', {
            data: {location: $('#tour').data('location')},
            success: function (response) {
                $('.photos').html(response).fadeIn();
            }});
    });
});
```


 ### 1.5 $.get Shorthand 
* There's an easier way to write this code using the jQuery $.get shorthand method. 
* Refactor this code to use $.get instead of $.ajax.

```sh
$(document).ready(function () {
    $('#tour').on('click', 'button', function () {
        $.get('/photos.html', function (response) {
            $('.photos').html(response).fadeIn();
        })
    });
});
```


### 1.6 Ajax Data 
* You've decided you only want to get photos of london. 
* Use the data option of the $.ajax function to pass a location option. 
* Get the location from the data-location on the #tour element using the data method.

```sh
$(document).ready(function () {
    $('#tour').on('click', 'button', function () {
        $.ajax('/photos.html', {
            data: {location: $('#tour').data('location')},
            success: function (response) {
                $('.photos').html(response).fadeIn();
            },
            error: function () {
                $('.photos').html('<li>There was a problem fetching the latest photos. Please try again</li>');
            }
        })
    })
});
```

### 1.8 Ajax with Errors 
* Sometimes things go wrong. 
* Maybe our server went down, or the traveler visiting our page lost their internet connection and can no longer access our site.
* Let's account for this case by adding an error callback that will set the contents of the .photos element to a message in an li element letting the traveler know that something went wrong and to try again. 
* You can write whatever you'd like for this message.

```sh
$(document).ready(function () {
    $('#tour').on('click', 'button', function () {
        $.ajax('/photos.html', {
            data: {location: $('#tour').data('location')},
            success: function (response) {
                $('.photos').html(response).fadeIn();
            },
            error: function () {
                $('.photos').html('<li>There was a problem fetching the latest photos. Please try again</li>');
            },
          	timeout: 3000
        })
    })
});
```

### 1.9 Setting a Timeout 250 PTS
* We've been hearing reports from our travelers that sometimes they'll click on this button 
and nothing will happen 
* Then a minute later they'll get a message saying "There was a problem fetching the latest photos. 
Please try again."

* Update the $.ajax request to timeout in 3 seconds to prevent this.

```sh
$(document).ready(function () {
    $('#tour').on('click', 'button', function () {
        $.ajax('/photos.html', {
            data: {location: $('#tour').data('location')},
            success: function (response) {
                $('.photos').html(response).fadeIn();
            },
            error: function () {
                $('.photos').html('<li>There was a problem fetching the latest photos. Please try again</li>');
            },
            timeout: 3000,
            beforeSend: function () {
                $('#tour').addClass('is-fetching');
            },
            complete: function () {
                $('#tour').removeClass('is-fetching');
            }
        })
    })
});
```

### 1.10 More Ajax Callbacks

* Things are working fine, but we could make it better. 
* While the server is responding, the traveler has no indication that anything is happening.
* Our designers have added some special styling to account for this. 
* Before the ajax command is sent, add a class of is-fetching to our #tour element,
* then remove this class after the request is complete.

```sh
$(document).ready(function () {
    function showPhotos() {
        $(this).find('span').slideToggle();
    }

    $('.photos').on('mouseenter', 'li', showPhotos)
        .on('mouseleave', 'li', showPhotos);

    var el = $('#tour');
    el.on('click', 'button', function () {
        $.ajax('/photos.html', {
            data: {location: el.data('location')},
            success: function (response) {
                $('.photos').html(response).fadeIn();
            },
            error: function () {
                $('.photos').html('<li>There was a problem fetching the latest photos. Please try again.</li>');
            },
            timeout: 3000,
            beforeSend: function () {
                $('#tour').addClass('is-fetching');
            },
            complete: function () {
                $('#tour').removeClass('is-fetching');
            }
        });
    });
});
```

### 1.11 Event Delegation 

* One other thing we did in Try jQuery was make the labels show up over the photos when we moused over them. 
* For some reason these are no longer working.
* It looks like we're trying to define our mouseover events when the DOM loads, but since we're loading them with Ajax it's not finding them.
* Update these to use event delegation, ensuring they'll work if we load them via Ajax.

```sh
$(document).ready(function() {
  function showPhotos() {
    $(this).find('span').slideToggle();
  }

  $('.photos').on('mouseenter', 'li', showPhotos)
              .on('mouseleave', 'li', showPhotos);

  var el = $("#tour");
  el.on("click", "button", function() {
    $.ajax('/photos.html', {
      data: {location: el.data('location')},
      success: function(response) {
        $('.photos').html(response).fadeIn();
      },
      error: function() {
        $('.photos').html('<li>There was a problem fetching the latest photos. Please try again.</li>');
      },
      timeout: 3000,
      beforeSend: function() {
        $('#tour').addClass('is-fetching');
      },
      complete: function() {
        $('#tour').removeClass('is-fetching');
      }
    });
  });
});
```
