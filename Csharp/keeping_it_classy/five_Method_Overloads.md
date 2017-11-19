# Level 5 Method Overloads

### 5.2 Method Signatures
Identify the two methods that have conflicting method signatures.
```sh
string AddBand(string name)

void AddBand(string name)
```

### 5.3 Method Overload

Let's create a method overload for AddBand that accepts an array of strings and then calls the existing AddBand method for each of those strings.

- Create a new public method named AddBand with a return type void that accepts an array of strings that contain band names.
- Inside our new AddBand method, use a foreach loop to iterate through each band name string in the array and call the existing AddBand method using each band name string for its argument.
- To see our new method in action, let's switch from the Venue.cs file to the Program.cs file.

We've already created an array of strings called bandNames. Using the venue object, call our new AddBand method and pass in the bandNames array as an argument to see the results.


venus.cs
```sh
using System;
using System.Collections.Generic;

public class Venue
{
    public string Name;
    public List<Band> Bands = new List<Band>();

    public void AddBand(string[] names)
    {
        foreach(var name in names)
        {
            AddBand(name);
        }
    }

    public void AddBand(string name)
    {
        Band band = new Band();
        band.Name = name;
        Bands.Add(band);
    }

    public void Announce()
    {
        Console.WriteLine(Name + " will have " + Bands.Count + " bands playing tonight!");

        foreach(var band in Bands)
        {
            band.Announce();
        }
    }
}
```

program.cs
```sh
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("What is the name of your venue?");
        Venue venue = new Venue();
        venue.Name = "The Jazz Hut";
        string[] bandNames = {"Jazztallica", "Jazzadeth"};
        venue.AddBand(bandNames);
        venue.Announce();
    }
}
```

Band.cs
```sh
using System;

public class Band
{
    public string Name;

    public void Announce()
    {
        Console.WriteLine("Welcome " + Name + " to the stage!");
    }
}
```
