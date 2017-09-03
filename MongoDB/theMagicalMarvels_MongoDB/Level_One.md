# The magical Marvels of MongoDB

## Level One: Conjuring MongoDB

### 1.2 Dispelling the Database

"We've inherited a database that stores information about magic wands."

* A MongoDB shell has been started, so write the command that will set the current database to wandRecorder.
* Remember, if you ever forget a command, you can use help

```sh
use wandRecorder
```

### 1.3 Conjuring Collections 
"The wandRecorder database has wands already loaded inside of a collection named wands. "

* Write a command to find all of the documents in that collection.

```sh
db.wands.find(all)
```

### 1.4 Waving the Wand 

"We're proud of the shiny new wand we've just purchased, so let's add it to the wands collection." 

* Our wand's name is "Dream Bender" and its creator is "Foxmond".

* Write a command to insert our wand into the wands collection.

```sh
  db.wands.insert(
 {
    "name": "Dream Bender",
    "creator": "Foxmond"
 }
)
```


### 1.6 Hey, Have You Heard About Wands?

* Our friend Merlin was asking about a wand by the name of "Storm Seeker". 
* Let's check the wands collection to see if we can find information about it.

``` sh 
db.wands.find( {"name" : "Storm Seeker"})
{
  "_id": ObjectId('d0a77e57a0544ec7ad5a740b'),
  "name": "Storm Seeker",
  "creator": "Olivemist",
  "level_required": 96,
  "price": 55.99,
  "powers": [
  "Wind",
    "Static" ],
  "damage": {
    "magic": 2,
    "melee": 5
  }
}

```  


### 1.7 Expecto Mongo Wand

* Merlin must be losing his marbles, because he actually wanted us to search for any wand created by "Moonsap".

* Write a query that finds all wands where the creator is "Moonsap".

``` sh 
db.wands.find({"creator" : "Moonsap"})
{
  "_id": ObjectId('5609e753bd62caa811c9abbd'),
  "name": "Riddle Bolt",
  "creator": "Moonsap",
  "level_required": 5,
  "price": 30.99,
  "powers": [
    "Earth",
    "Isolate"
  ],
  "damage": {
    "magic": 1.4,
    "melee": 0.4
  }
}
{
  "_id": ObjectId('7aa48b7bccb84f29bdc859b4'),
  "name": "Cometfell",
  "creator": "Moonsap",
  "level_required": 10,
  "price": 150.95,
  "powers": [
    "Solar",
    "Love"
  ],
  "damage": {
    "magic": 1.7,
    "melee": 2.3
  }
}
{
  "_id": ObjectId('5404bf9eb971425e86832c93'),
  "name": "Sacred Sun",
  "creator": "Moonsap",
  "level_required": 13,
  "price": 33.99,
  "powers": [
    "Solar",
    "Bless"
  ],
  "damage": {
    "magic": 1.7,
    "melee": 2.3
  }
}
``` 

### 1.8 Wand Summoning

There's a lot more about wands than just their name and creator, so let's add a new wand with much more detailed information.

* Some wands require more experience than others. Let's record the minimum level needed to use a wand in a field named level_required. This particular wand requires level 10.

* We would never think of selling our wand, but it's fun to know how much it's worth anyway. Let's record the price of our wand in a field named price. This particular wand is worth 34.9 gems.

* Each wand can have any number of special powers, like Fire, Teleportation, or Energy. Let's record all of these power options in a field named powers. This particular wand has powers of "Fire" and "Love", which should be stored in an array.

* Magical folk are a peace-loving people, but occasionally they need to throw down, so it's a good idea to store each wand's damage capability in a field named damage. Most wands can cause 2 types of damage — magic and melee.

*The value of the damage field should be an object with 2 properties. 

*The magic property for this wand is 4, and the melee property is 2.
 
* Now that we've built out a wand with all the correct information, go ahead and insert it into the wands collection.

``` sh 
db.wands.insert ({
  "name": "Dream Bender",
  "creator": "Foxmond",
  "level_required" : 10,
  "price" : 34.9,
  "powers" : ["Fire", "Love"],
  "damage" : {"magic" : 4, "melee" : 2}
}
)
```  


### 1.9 Finding the Perfect Wand

We've upgraded our wands with data for all of the new fields. 
* Now we can write fun queries to find out — for example — which wands have "Fire" in their list of powers. 
* Try writing a query based on this.

``` sh 
db.wands.find({"powers" : "Fire"})
{
  "_id": ObjectId('f01a4524a6de4c8f98d4e8bf'),
  "name": "Journey End",
  "creator": "Foxmond",
  "level_required": 1,
  "price": 4.99,
  "powers": [
    "Molten",
    "Fire"
  ],
  "damage": {
    "magic": 0.7,
    "melee": 0.6
  }
}
{
  "_id": ObjectId('2db8f9de713b486cb6196340'),
  "name": "Destiny Fire",
  "creator": "Sageseer",
  "level_required": 2,
  "price": 24.99,
  "powers": [
    "Fire",
    "Spark"
  ],
  "damage": {
    "magic": 2,
    "melee": 2.6
  }
}
```


### 1.10 Bad Magic 
"You're doing a great job inserting and querying data from the database." 

* Occasionally, though, you may run into some bad data.

* Case in point, the following 2 documents are problematic.

``` sh
{
  "_id": ObjectId("1234567"),
  "name": "Dream Bender",
  "creator": "Foxmond",
  "level_required": 10,
  "price": 34.9,
  "powers": ["Fire", "Love"],
  "damage": {"magic": 4, "melee": 2}
},
{
  "_id": ObjectId("1234567"),
  "name": "Lightbane",
  "creator": "Elvira",
  "level_required": 4,
  "price": 4.2,
  "powers": ["Light", "Darkness"],
  "damage": {"magic": 10, "melee": 0}
}
```
Can you tell which validation they break?  
Answer: Unique_id

Explanation: Unique_id is broken because both the objects appear to have the same ObjectId, 
this is meant to be a unique set of numbers assigned to each object. It should never be the same. 



