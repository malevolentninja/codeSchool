# Level 2 Classes

### 2.2 Declaring a Class
Let's create a new Venue class that will contain a Name variable and an Announce method that will write our venue announcement message to the console.

- Declare a class named Venue.
- Inside the Venue class, add an instance variable of data type string called Name.
- Create a method named Announce() that won't return any data and doesn't accept any parameters. This method should use Console.WriteLine to print the Name of the venue followed by " will have several bands playing tonight!".

```sh
using System;
class Venue
{
    string Name;

    void Announce()
    {
        Console.WriteLine(Name + " will have several bands playing tonight!");
    }
}
```


### 2.3 Access Modifiers
Let's make our Venue class and its contents accessible to other classes.
- Change the access modifier for the Venue class, the Name variable, 
- the Announce method to make them available to other classes.
```sh
using System;

public class Venue
{
    public string Name;

    public void Announce()
    {
        Console.WriteLine(Name + " will have several bands playing tonight!");
    }
}
```

### 2.4 Calling a Class Method

Now that we have our Venue class in Venue.cs, we can instantiate and use it in our Program.cs file.

- Declare a variable venue of type Venue and set it to a newly instantiated instance of the Venue class
- Assign the string "The Jazz Hut" to the Name property of the venue object
- Using our venue variable, call our Venue class's Announce method

Program.cs
```sh
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("What is the name of your venue?");
        Venue venue = new Venue();
        venue.Name = "The Jazz Hut";
        venue.Announce();
    }
}
```
