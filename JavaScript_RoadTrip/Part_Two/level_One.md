# Level One: The Labyrinth of Loops

### 1.2

- write a basic while loop 
- prints to the console all the numbers from 10 to 1 in descending order. 
- We’ve given you a starting variable to get the wheels turning. 

countdown.js:

```sh
// Create the variable num to 10
var num = 10;

// Create a while loop that said while num bigger than 0 do this
while(num > 0) {
  //Print the num first, because we want to see the number 10
  console.log(num);

  // once the console print number 10 start counting down
  num -= 1;

  // The while loop will keep looping until the num variable reach 0 and stop the loop, because of the statement
  // must be bigger than 0 which is false
}
```
### 1.3
In the Death Valley National Park, a group of environmentalists have begun a project that will grow the population of Bighorn Sheep. Every month, the population will multiply by four! To stay on top of this explosive growth, the scientists would like a printout of how many sheep will make a new home in Death Valley.

In deathValley.js, use the three existing variables to build a while loop that prints a message for one year’s worth of time. Here’s what the first two lines of output should look like:

There will be 16 sheep after 1 month(s)!
There will be 64 sheep after 2 month(s)!
*/
deathValley.js:

```sh
// Create a based variables
var numSheep = 4;
var monthNumber = 1;
var monthsToPrint = 12;

// Create a while loop with a statement that stop the loop once it reach 1 year
while( monthNumber < monthsToPrint ) {
  numSheep *= 4;
  console.log("There will be " + numSheep + " sheep after " + monthNumber + " month(s)!");
  monthNumber ++;
}
```

FIRST THING TO DO 
- make the while loop stop, 
- so we have to increment the monthNumber

SECOND THING TO DO 
- Multiply the num of sheep straight away, 
- want the numSheep start at 16 for the first month

LAST THING TO DO 
- print with the text and the result for every loop


### 1.4
write a basic for loop that 
- prints to the console all the numbers from 10 to 1 in descending order. 
- This is the similar to one of the previous challenges, 
- but this time we’re using a for loop instead of a while loop.

countdown.js
```sh
for(var i = 10; i > 0; i--){
  console.log(i);
}
```

Variable i is 10, as long as variable i(10) bigger than 0, minus variable i with 1 for each loop


### 1.5
- Morph your previous while loop into a for loop that uses the same variable names
- Remember, you’ll still need to declare the starting number of sheep and the number of months to print outside the loop. 
- We’ve given you the starting number of sheep again, as well as the amount of months you’ll need to print out for use in the loop parameters. 

```sh
var numSheep = 4;
var monthsToPrint = 12;

for(var months = 1; months <= monthsToPrint; months++){ 
  numSheep *= 4;
  console.log("There will be " + numSheep + " sheep after " + months + " month(s)!");
};
```
- Create the base variable first
- Create a variable months inside the for loop 
- make sure the variable months is less equal to variable monthsToPrint,
- then increment variable months by 1
- Multiply the variable numSheep first, because they want to see the first multiplication within the first month
