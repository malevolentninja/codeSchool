# Level 3 Groups of Objects

### 3.2 Creating an Array
Let's create an array called Bands.

- Create a public array of type Band[] called Bands and instantiate it to contain 2 new Band objects.
-  Inside the AddBand method, set the first index in the Bands array to the band object. 
      - Remember, arrays start counting from 0.
      
```sh
using System;

public class Venue
{
    public string Name;
    public Band[] Bands = new Band[2];

    public void AddBand(string name)
    {
        Band band = new Band();
        band.Name = name;
        Bands[0] = band;
    }
```

# 3.3 Creating a List

Let's create a List of type Band called Bands.
- Create a public List of Band called Bands. 
     - For this task, we'll just create the Bands variable
     - won't need to assign it a value until the next task.
- Set Bands default value to be a new List of Band.
- Inside the AddBand method, add the band object to the Bands list.

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
        Console.WriteLine(Name + " will have several bands playing tonight!");
    }
}
```
