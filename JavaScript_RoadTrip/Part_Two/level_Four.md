# Level 4: The Desert of Declarations

### 4.2
A Basic Multiplication Function

In the uniqueMath.js file, build a function declaration called multiplyTrio that takes in three parameters. Inside the function, multiply the numbers together into one product, and return the result. You may use whatever parameter and variable names you’d like.

```sh

function  multiplyTrio ( num1 , num2 , num3 ) {
     return num1 * num2 * num3;
}
```

### 4.3 Calling Functions

Call your multiplyTrio function from the console using the numbers 8, 4, and 10.

```sh
multiplyTrio ( 8 , 4 , 10 );
```

### 4.4 More Declarations

 Build a function declaration called maxOf2 that takes in two numbers and returns the greater value.
 - Be careful to think about the possibility of equality as well and return one of the numbers.


```sh
function  maxOf2 ( num1 , num2 ) {
     if (num1 >= num2) {
         return num1;
    } else {
         return num2;
    }
}
```

### 4.5 Refactoring for Efficiency and Legibility

Refactor the code in the function to include only one line that returns a value.

uniqueMath.js
```sh
function  mystery ( x , y ) {
     return ( 4  * x * y) + ( 3  * y +  5 );
}
```

### 4.7 Problem Solving with Functions I

The Park Rangers in Death Valley National Park divide up the feed responsibilities daily for the Bighorn Sheep population. Each sheep needs 2 lbs of ranger-provided food per day.

Build a function called feedPerRanger that takes in:

- The current population of sheep.
- The number of Park Rangers available during the day.
- The function should alert the amount of feed that each Park Ranger should be responsible for on that day. 
- The output should match the following format: "Each Park Ranger should load <number> lbs of feed today."

```sh
function feedPerRanger(a,b) {
var numSheep=a;
var parkRangers=b;
var dailyFeed=a*2/b;
alert('Each Park Ranger should load '+dailyFeed+' lbs of feed today.');
}
feedPerRanger(50,8);
```

### 4.8 Problem Solving with functions II

Back at the Hoover Dam, the technicians have decided they want more control of which generators are on and off. So, they’ve asked you to develop a way to adjust the total megawatts generated upon the switch-on or switch-off of a single, chosen generator.

Build a function named changePowerTotal that takes in four parameters:

- The total power generated (a number)
- The generator ID for the current generator (a number)
- The generator status (a string that says "on" or "off")
- The amount of power produced by the current generator (a number)

Your function should:

- If the current generator is set to "on", then add to the total power generated.
- Or if the current generator is set to "off", then remove from the total power generated.
- return the total power generated.
- Alert the technician in the following formats:


For switching on: "Generator #2 is now on, adding 62 MW, for a total of 62 MW!"

For switching off: "Generator #2 is now off, removing 62 MW, for a total of 0 MW!"

Note: You do not need to call the function. 
Build the function declaration without invoking it.

- note the difference between the fact that some of the values were specific to the current generator, and the first one is for the current total.
- setup a conditional based on whether the genStatus is set to "on" or "off"
- use those conditionals to add or remove to the totalPower
- add a return value
- use strings to alert all those value

```sh
function changePowerTotal(totalPower, genID, genStatus, genPower) {
  if (genStatus == "on") {
    totalPower += genPower;
    alert("Generator #" + genID + " is now " + genStatus + ", adding " + genPower + " MW, for a total of " + totalPower + " MW!");
  } else if (genStatus == "off") {
    totalPower -= genPower;
    alert("Generator #" + genID + " is now " + genStatus + ", removing " + genPower + " MW, for a total of " + totalPower + " MW!");
  }
  return totalPower;
}
```
