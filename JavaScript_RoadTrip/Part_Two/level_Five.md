# Level Five: The Array Archipelago

### 5.2 Adjusting Array Contents I

In the following array, set one value of the array so that it will be a list of numbers in order.

```sh
var list = [1, 2, 3, 7, 5, 6, 7, 8, 9];

list [ 3 ] =  4 ;
```

### 5.3 Array Functions I

Using the specific array function that adds data to the back end of the array, add the next number to your newly corrected list.

```sh
var list = [1, 2, 3, 4, 5, 6, 7, 8, 9];

list.push(10);
```

### 5.4 Array Functions I
Create an array called values that contains the following contents in order:

a String
a Number
a Boolean

```sh
var values = [ " Hello World " , 2017 , true ];
```

### 5.5 Array Functions II

Now using the specific array function that takes a piece of data off the back of an array, remove the last entry from your values array and
store the result in a variable called bool.

```sh
var bool =  values.pop ();
```

### 5.6 2D Arrays I

Check out the following setup. Enter a line of code that declares a variable called infant and accesses the word "Baby" from eightiesMovies without making any changes to either element inside the array.

```sh
var movie1 = [16, "Candles"];
var movie2 = [3, "Men", "and", "a", "Baby"];
var eightiesMovies = [movie1, movie2];

var infant = eightiesMovies [ 1 ] [ 4 ];
```

### 5.7 2D Arrays II

Now alert a string with the full title of the first movie in the eightiesMovies array, but only using the eightiesMovies variable to access the correct values. Use the concatenation operator to unite the words into one string, and remember to be attentive to necessary whitespace!

```sh
var movie1 = [16, "Candles"];
var movie2 = [3, "Men", "and", "a", "Baby"];
var eightiesMovies = [movie1, movie2];

Alert (eightiesMovies [ 0 ] [ 0 ] +  "  "  + eightiesMovies [ 0 ] [ 1 ]);
```


### 5.9 Iteration over Array Contents

Build out the numStrings function using a for loop that counts all of the strings in the array parameter called list.

- Inside the function, set up a count variable
- initialize it to a value of 0. 
We can use this variable to keep track of the number of strings.
- Use a for loop to loop through the list array.
- If the typeof the current array index value is equal to "string", then increment the count variable.
- Outside the for loop, return the count variable with the total amount of strings found.

```sh

function numStrings(list) {
  var stringCount = 0;
  for (var i = 0; i < list.length; i++) {
    if (typeof(list[i]) == "string") {
      stringCount++;
    }
  }
  return stringCount;
}
```

