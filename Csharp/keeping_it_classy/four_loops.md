# Level 4 Loops

### 4.2 While Loop
Given the while loop while(repeat), which of the following options are proper ways to stop the loop from repeating?

- repeat=false;
- break;


### 4.3 Foreach loop
Let's create a foreach loop that will announce each band in our list of bands.
-  Create a foreach loop that iterates through each band in Bands.
- Inside the loop, print the announcement message for each band by invoking its Announce method.

```sh
using System;
using System.Collections.Generic;

public class Venue
{
    public string Name;
    public List<Band> Bands = new List<Band>();

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
