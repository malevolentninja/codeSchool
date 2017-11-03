# Level 3: Built-In's Bluff

### 3.2 Pop-up Windows I

The Park Rangers at Badlands National Park have decided that the browser console is not a very pretty or efficient way to display their greeting to the user. 
- Change the code below to use a pop-up window that displays to the user whether or not the park is open.


```sh
var parkIsOpen = false;

if (parkIsOpen == true) {
  alert("Welcome to the Badlands National Park! Try to enjoy your stay.");
} else {
  alert("Sorry, the Badlands are particularly bad today. We're closed!");
}
```


### 3.3 Pop-up Windows II

In  below, ask the user for their age with a pop-up window function, and store the user’s response in a variable called userAge. Use the following question in the dialog box:
"What's your age, user?"

userProfile.js

```sh
var userAge = prompt("What's your age, user?");
```

###  3.4 Pop-up Windows II

With the userAge variable, we can ensure that the user has entered their age correctly. Use a pop-up window function to confirm the user entry with the following message:

"You entered <age>. Is this correct?"
Then store the result of the confirmation in a variable called ageIsCorrect. When you submit your code, enter your age in the prompt window, and then use the confirmation to select whether the entry is correct or incorrect.

Note: You do not need any loops or conditionals to complete this challenge.

userProfile.js

```sh
var userAge = prompt("What's your age, user?");
var ageIsCorrect = confirm("You entered " + userAge + ". Is this correct?");
```

### 3.5
An Entry Confirmation Loop

We’ve learned to prompt the user for their age, and then confirm that their age has been entered correctly. Now we can use a while loop to improve the way this works.

Create a while loop that will continue to execute as long as the user has not entered the correct age. Inside the loop, provide a confirmation that the age has been entered correctly:

"You entered <age>. Is this correct?"
If that confirmation statement is correct, then set ageIsCorrect to true and alert the following message:

"Great! Your age is logged as <age>."

Otherwise, the loop should continue to prompt a user to enter their age and assign that value to the userAge variable:
"What's your age, user?"


```sh
var userAge = prompt("What's your age, user?");
var ageIsCorrect = false;
while (ageIsCorrect ==  false){
   var userAge =  prompt(" What's your age user?");

  if ( confirm ( "You entered "  + userAge +  " . Is this correct? " )) {
     alert ( " Great! Your age is logged as "  + userAge +  " . " );
    ageIsCorrect =  true ;
  }
};
```
