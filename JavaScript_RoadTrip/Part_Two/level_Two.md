# Level Two: Conditional Canyon 

### 2.2

The Hoover Dam has 19 generators of multiple types. For simplicity, let’s say that the first 4 of these generators output 62 megawatts, and the other 15 output 124 megawatts. In hooverDam.js, the Dam Rangers have asked you to design a system of two loops that turns each generator on in progression, and prints the new total of megawatts generated.

They’d like the first loop to be a while loop handling the first 4 generators. Then, they’d like the second loop to be a for loop that handles the other 15 generators. Each output line should resemble the following lines, with adjusted values for the currentGen and totalMW:

" Generator #1 is on, adding 62 MW, for a total of 62 MW!"
" Generator #2 is on, adding 62 MW, for a total of 124 MW!"

```sh
// Create the base variable first

var currentGen = 1;
var totalGen = 19;

// Why this global variable start with 0? because we want to change this variable numbers in the while loops and in the for loop

var totalMW = 0;

// Build the while loop,  make a statement that the GLOBAL variable currentGen is less or equal than 4, do the loop

while(currentGen <= 4) {

  // Modify the variable totalMW
  totalMW += 62;

  // Print the first loop
  console.log("Generator #" + currentGen + " is on, adding 62 MW, for a total of " + totalMW + " MW!");

  // After printing the first loop, we want to increment the currentGen
  currentGen += 1;

}

// Since we have modified the GLOBAL variable of currentGen, the value change into 5, because when the GLOBAL variable of currentGen reach 5, the while loop is stop
//check by console.log(currentGen);

// We can write for(currentGen; currentGen < totalGen; currentGen +=1) but for details info, we write with basic knowledge
for(var i = currentGen; i < totalGen; i++){

  // The same as the GLOBAL variable currentGen,
  // The GLOBAL variable of totalVariable have change with the last value from the while loop
  // We just need to add the new number according to the instruction

  totalMW += 124;
  console.log("Generator #" + currentGen + " is on, adding 124 MW, for a total of " + totalMW + " MW!");

}
```

### 2.3 Using Boolean Flags in Conditionals

The Badlands National Park would like to print specific messages depending on whether the park is open or closed.

They’ve asked you to modify their badlands.js file to print one of the following messages depending on the boolean value (true or false) of the variable parkIsOpen. We’ve already established for you the status of the variable for today.

Add a pair of conditional statements to print one of the following messages to the console based on the parkIsOpen variable:

"Welcome to the Badlands National Park! Try to enjoy your stay."

OR

"Sorry, the Badlands are particularly bad today. We're closed!"

```sh
var parkIsOpen = true;

if (parkIsOpen = true) {
    console.log("Welcome to the Badlands National Park! Try to enjoy your stay.");
} else {
    console.log("Sorry, the Badlands are particularly bad today. We're closed!");
}
```


### 2.5 Problem solving with conditionals

Back at Death Valley, scientists could see that the Sheep Situation would quickly get out of control. 
- They have decided that, for any month the population climbs above 10000, half of the sheep will be sent away to other regions.

Inside our for loop, insert an if statement that:
- Removes half of the sheep population if the number of sheep rises above 10000.
- Prints the number of sheep being removed to the console 

Need the following format:
- Removing <number> sheep from the population
Note: To complete the challenge, you only need to insert the if statement
You do not need to create an else statement or change any of the provided code.

```sh
var numSheep = 4;
var monthsToPrint = 12;
for (var monthNumber = 1; monthNumber <= monthsToPrint; monthNumber++) {

  if (numSheep >= 10000) {
   numSheep *= .5;
      console.log("Removing " +numSheep+ " sheep from the population.");
  }

  numSheep *= 4;
  console.log("There will be " + numSheep + " sheep after " + monthNumber + " month(s)!");
}
```

### 2.7 Too Many Sheep!

We’ve made a significant difference, but there are still too many sheep for the fragile Death Valley ecosystem. 
The Rangers would like you to implement the following new plan for population reduction:
- If the month is a multiple of 4, then find 75% of the sheep population. 
- Log that value to the console in the format below. 
- Then, remove that value from the total number of sheep.
- Otherwise, if the population is above 10000, find half of the sheep population. Log that value to the console in the format below. 
- Then, remove that value from the total number of sheep.

Use this format for logging sheep reduction:

- Removing <number> sheep from the population.
Note: To complete the challenge, you only need to insert an if statement and an else if statement. You do not need to create an else statement at the bottom or change any of the provided code.

```sh
var numSheep = 4;
var monthsToPrint = 12;

for (var monthNumber = 1; monthNumber <= monthsToPrint; monthNumber++) {

  if (monthNumber % 4 == 0) {
    var sheepToRemove = numSheep * .75;
    console.log("Removing " + sheepToRemove + " sheep from the population.");
    numSheep = numSheep - sheepToRemove;
  } else if (numSheep > 10000) {
    var sheepToRemove = numSheep * .5;
    console.log("Removing " + sheepToRemove + " sheep from the population.");
    numSheep = numSheep - sheepToRemove;
  }

  numSheep *= 4;
  console.log("There will be " + numSheep + " sheep after " + monthNumber + " month(s)!");
}
```



### 2.8
Some Dam Complex Conditionals!

The people at the Hoover Dam have called you back, and would like a program that shows what happens when only the even numbered turbines are turned on. And they want it all in just one for loop.

With a set of complex conditional statements inside the loop, construct a way to only turn on even numbered turbines. 

Remember our power output situation:
- Generators 1 through 4 produce 62 MW.
- Generators 5 through 19 produce 124 MW.
- The output should follow this format:

"Generator #1 is off."
"Generator #2 is on, adding 62 MW, for a total of 62 MW!"
We’ve given you some starting variables to use in your build. 

Consider the possible scenarios when building your conditions:
- The Generator provides 62 MW of power.
- The Generator provides 124 MW of power.
- The Generator is off.

```sh
var totalGen = 19;
var totalMW = 0;

for (var currentGen = 1; currentGen <= totalGen; currentGen++) {
    if (currentGen % 2 == 0) {
        if (currentGen <= 4) {
            totalMW += 62;
            console.log("Generator #" + currentGen + " is on, adding 62 MW, for a total of " + totalMW + " MW!");
        } else {
            totalMW += 124;
            console.log("Generator #" + currentGen + " is on, adding 124 MW, for a total of " + totalMW + " MW!");
        }
    } else {
        console.log("Generator #" + currentGen + " is off.");
    }
}
```
