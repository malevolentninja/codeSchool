# Level Two: JavaScript and jQuery
Organize your jQuery and JavaScript.

### 2.3 Refactor To Objects 

* The level1.js tab shows our code as it stood at the end of level 1, but isn't being loaded into the page.
* We have some pretty deep nesting of functions, and that makes our code a little tough to read. 
* Let's start refactoring it into a JavaScript object. For starters, create a new function named init within our tour object.
* Next, call the init method on the tour object from within the $(document).ready function.
* Lastly, move the existing code that's run on $(document).ready within level1.js into our new init method. 
* This should be functionally the same, but now our code is moved into the tour object.

```sh
var tour = {
    init: function () {
        $('#tour').on('click', 'button', this.fetchPhotos)
    },
    fetchPhotos: function () {
        $.ajax('/photos.html', {
            data: {location: $('#tour').data('location')},
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
    }
};

$(document).ready(function () {
    tour.init();
});
```

### 2.4 Event Handler Refactor 

* Well, we moved our big block of code around, but it's still tough to read. 
* Let's move our $.ajax call from within this event handler callback to a new fetchPhotos key on the tour object. 
* Also, update the call to on click to use this new fetchPhotos function.
```sh
var tour = {
  init: function() {
    $("#tour").on("click", "button", this.fetchPhotos);
  },
  fetchPhotos: function() {
    $.ajax('/photos.html', {
      data: {location: $("#tour").data('location')},
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
  }
}
$(document).ready(function() {
  tour.init();
});
```


### 2.6 Creating a Function 

* Let's get our feet wet with how functions work by creating a function which will represent a Tour. 
* Remember, this function should start with a capital letter and be defined outside of $(document).ready().
* Then, inside of $(document).ready(), create a new instance of the object created by the Tour function. 
* When that new Tour is created, log a message to the console using console.log.
```sh
function Tour() {
    console.log('A new Tour was created');
}

$(document).ready(function () {
    var newInstance = new Tour();
});
```

### 2.7 Functionality in Functions

* In order to add a bit of functionality to our Tour, let's pass in the nightly cost of the Tour when we create a new one - maybe 100 for now. 
* In the Tour function, update the declaration to accept this new price argument.
* In order to use this price, create a new function within the Tour named cost, which can be called with a number of nights.
* This cost function should console.log the number of nights multiplied by the price. We've added the call to cost within $(document).ready(), which you can uncomment once you've implemented.

```sh
function Tour(price) {
    this.cost = function (numberOfNights) {
        console.log(price * numberOfNights);
    };
}
$(document).ready(function () {
    var tour = new Tour(100);
    tour.cost(4);
});
```

### 2.8 Function Refactor 
* Up until this point we've only had 1 tour on the page at once, so we were able to hardcode a good deal of the DOM elements. 
* Let's work on refactoring our code to work with multiple tours on the page.
* We're showing our tour JavaScript object we made in the reference.js file here, but it's not being loaded into the page.
* For starters, create a new Tour function that takes in a jQuery object as a parameter. 
* Create a new instance of a Tour on document.ready, passing in a jQuery object for the #paris location.
* Within the function, call console.log with the passed in DOM element.

```sh
$(document).ready(function() {
  var paris = new Tour($('#paris'));
});
function Tour(el) {
  console.log(el);
}
```

### 2.9 Function Setup

* Now we're going to finish refactoring our code into the new Tour function. 
* To accomplish this, we'll need to do quite a few things:
* First, recreate an event listener within our Tour which will watch for clicks on
any button contained in the passed in element and run the fetchPhotos function.
* Next, set this.el to the passed in el so that we'll be able access it later on.
* For now leave the fetchPhotos function empty, but make sure it's called when the button is clicked.

```sh
function Tour(el) {
  this.el = el;
  this.fetchPhotos = function() {
  };
  el.on('click', 'button', this.fetchPhotos);
}
$(document).ready(function() {
  var paris = new Tour($('#paris'));
});
```

### 2.10 fetchPhotos Refactor

* Unfortunately, we can't just copy our existing fetchPhotos method from level 1
straight into our function - we're going to need to make a few changes in order
to make it work:
* The biggest change is that we can't query the DOM directly -- instead we'll have
to base all DOM queries off of el, the element representing the current tour.
* Update the data option to take in the data from the current tour -- tour.el. Add
a context option to the ajax call, giving it a context of tour. 
* After that, within your callbacks, you'll be able to reference the current tour element using this.el
rather than #tour. 
* Lastly, instead of finding all .photos only find .photos within the current this.el element.

```sh
function Tour(el) {
  var tour = this;
  this.el = el;
  this.fetchPhotos = function() {
    $.ajax('/photos.html', {
      context: tour,
      data: {location: $(tour.el).data('location')},
      success: function(response) {
        $(this.el).find('.photos').html(response).fadeIn();
      },
      error: function() {
        $(this.el).find('.photos').html('<li>There was a problem fetching the latest photos. Please try again.</li>');
      },
      timeout: 3000,
      beforeSend: function() {
        $(this.el).addClass('is-fetching');
      },
      complete: function() {
        $(this.el).removeClass('is-fetching');
      }
    });
  };
  this.el.on('click', 'button', this.fetchPhotos);
}
$(document).ready(function() {
  var paris = new Tour($('#paris'));
  var london = new Tour($('#london'));
});
```

### 2.11 Instances of a Function
* On load, create another instance of a Tour, this time passing in a jQuery object for the #london element.

```sh
function Tour(el) {
  var tour = this;
  this.el = el;
  this.fetchPhotos = function() {
    $.ajax('/photos.html', {
      data: {location: tour.el.data('location')},
      context: tour,
      success: function(response) {
        this.el.find('.photos').html(response).fadeIn();
      },
      error: function() {
        this.el.find('.photos').html('<li>There was a problem fetching the latest photos. Please try again.</li>');
      },
      timeout: 3000,
      beforeSend: function() {
        this.el.addClass('is-fetching');
      },
      complete: function() {
        this.el.removeClass('is-fetching');
      }
    });
  }
  this.el.on('click', 'button', this.fetchPhotos);
}
$(document).ready(function() {
  var paris = new Tour($('#paris'));
  var london = new Tour($('#london'));
});
```
