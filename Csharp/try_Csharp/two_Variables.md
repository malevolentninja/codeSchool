
# LEVEL 2: Variables
Explore data types as well as declare, store, and retrieve variables.

### 2.2 Using Variables 

Let's practice declaring some variables and setting their values. Then, we'll use our new variables to print an announcement to the console.


- Declare a string variable named venue. On the same line, set this variable's value to "C's Blues".
- Declare an int variable named bands. On the same line, set this variable's value to 4.
- Use Console.WriteLine with the venue and bands variables to print the following announcement text to the console:

C's Blues will have 4 bands performing tonight!

```sh
using System;

class Program
{
    static void Main(string[] args)
    {
        string venue = "C's Blues";
        int bands = 4;
        Console.WriteLine(venue + " will have " + bands + " bands performing tonight!");
    }
}

```

### 2.3 Explicit Conversion 
Select the appropriate way to set an int value to the instruments variable using the string value from guitars.

```sh
in instruments = int.Parse(guitars);
```

### 2.4 DataType Int 
Which of the following statements about int is correct?

int can hold whole number values, including both positive and negative values
