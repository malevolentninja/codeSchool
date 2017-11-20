
### Level 3: Conditions
Discover how to use conditions to change program flow.

### 3.2 If Condition
Using int.TryParse, set bands to the parsed value of bandArgument. Set up a condition to only announce the venue and bands if TryParse returns true.

- Create an if condition that will only print our existing console announcement when TryParse returns true. Use int.TryParse to set bands to the value of bandArgument.
- In the event the first condition isn't met, create an else condition that instead announces "We were unable to determine the number of bands performing tonight, try again."

```sh
using System;

public class Program
{
    static void Main(string[] args)
    {
        string venue = args[0];
        string bandArgument = args[1];
        int bands;
        // First, create an if condition...
      if (int.TryParse(bandArgument, out bands))
{
       Console.WriteLine(venue + " will have " + bands + " bands performing tonight!");
}
        // Also, create an else condition...
        else
{
Console.WriteLine("We were unable to determine the number of bands performing tonight, try again.");
}
    }
}
```

### 3.3 Chaining Conditions 
After we announce the venue and the number of bands playing, let's print a new message about the performance(s) based on how many bands will be playing tonight.

- If the number of bands performing tonight is equal to 0, use Console.WriteLine to print the following announcement: "There will be no performances tonight."

- If the previous condition does not apply and the number of bands is equal to 1, use Console.WriteLine to print the following announcement: "It's going to be a fantastic show tonight!"

- If neither of the previous conditions apply, use Console.WriteLine to print the following announcement: "There will be plenty of thrilling performances to see tonight!"

program.cs
```sh
sing System;

public class Program
{
    static void Main(string[] args)
    {
        string venue = args[0];
        string bandArgument = args[1];
        int bands;

        if(int.TryParse(bandArgument, out bands))
        {
            Console.WriteLine(venue + " will have " + bands + " bands performing tonight!");

            if(bands == 0)
            {
                Console.WriteLine("There will be no performances tonight.");
            }
            else if(bands == 1)
            {
                Console.WriteLine("It's going to be a fantastic show tonight!");
            }
            else
            {
                Console.WriteLine("There will be plenty of thrilling performances to see tonight!");
            }
        }
        else
        {
            Console.WriteLine("We were unable to determine the number of bands performing tonight, try again.");
        }
    }
}
```
