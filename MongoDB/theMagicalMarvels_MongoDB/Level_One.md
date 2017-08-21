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


