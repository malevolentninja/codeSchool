# Level 1 Methods

### 1.2 Declaring a method
Let's create a new method at the bottom of the Program class that takes the name of a venue as a string argument and returns a formatted announcement.
- Below the Main method, create a new static string method called Announce. This method should accept a single string parameter named venue.
     - Inside the method, return the provided venue parameter concatenated with " will have bands performing tonight." appended to the end.
- At the end of the Main method, create another call to Console.WriteLine.
     - The argument for this should be the string returned by calling Announce with the variable venue as its argument.
```sh
using System;

public class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("What is the name of your venue?");
        string venue = args[0]; // Sets the venue based on the command-line argument. We'll cover arrays in Level 3!
        Console.WriteLine(Announce(venue));
    }

    static string Announce(string venue)
    {
        return venue + " will have bands performing tonight.";
    }
}
```

### 1.3 Void Return Type

Let's move our console announcement from the Main method into our Announce method. 
      - We'll need to make changes to Announce since it will no longer need to return a value.
- First, remove Console.WriteLine from the bottom of the Main method and leave only the call to Announce(venue).
- Next, we need to change our return type for the Announce method so it does not return a value. 
      - Then replace the return statement in the Announce method to instead use a Console.WriteLine call with the existing concatenated string as its argument.

```sh
using System;

public class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("What is the name of your venue?");
        string venue = args[0];
        Announce(venue);
    }

    static void Announce(string venue)
    {
        Console.WriteLine(venue + " will have bands performing tonight.");
    }
}
```
