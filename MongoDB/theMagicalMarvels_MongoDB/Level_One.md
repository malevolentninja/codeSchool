# The magical Marvels of MongoDB

## Level One

### 1.2 Dispelling the Database

We've inherited a database that stores information about magic wands.

* A MongoDB shell has been started, so write the command that will set the current database to wandRecorder.
* Remember, if you ever forget a command, you can use help

<code>  use wandRecorder </code>

### 1.3 Conjuring Collections 
The wandRecorder database has wands already loaded inside of a collection named wands. 

* Write a command to find all of the documents in that collection.

<code> db.wands.find(all) </code>

### 1.4 Waving the Wand 

We're proud of the shiny new wand we've just purchased, so let's add it to the wands collection. 

* Our wand's name is "Dream Bender" and its creator is "Foxmond".

* Write a command to insert our wand into the wands collection.

<code> db.wands.insert(
 {
    "name": "Dream Bender",
    "creator": "Foxmond"
 }
)
</code>


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


