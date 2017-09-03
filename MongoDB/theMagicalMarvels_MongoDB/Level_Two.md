
# The magical Marvels of MongoDB

## Level Two: Mystical Modifications

### 2.2 Oblitero Wand I
"While Merlin was looking through our wand information, 
he suddenly began to panic about a wand named the "Doom Bringer" and he ran out screaming. 
We should probably get rid of that wand if it scares a great wizard like Merlin."

- Write the command to remove the wand with the name of "Doom Bringer" from our wands collection.

```sh
db.wands.remove({"name" : "Doom Bringer"})
WriteResult({ 'nRemoved' : 1 })
```

### 2.3 Oblitero Wand II
"When we removed the "Doom Bringer" wand, we noticed that it had a power of "Death", 
and we don't want any wands like that in our database.
To be safe, let's remove any wands containing that in their powers."

```sh
 db.wands.remove({"powers" : "Death"})
```


### 2.4 Wand Reductions
"The makers of the "Devotion Shift" wand have decided to reduce its price
since no one is showing interest in their luxury wand."

- Write the command to update the wand with a name of "Devotion Shift" and set the price to 5.99.

```sh
db.wands.update({"name": "Devotion Shift"}, { "$set": {"price" : 5.99}})
```


### 2.5 Magical Regulations
"The Grand House of Magic recently passed a law that all wands with "Fire" in their list of powers must increase their level_required field by 2. We need to update all wands that have been affected by the new law."

- First, let's add the query parameter to find all wands that include "Fire" in their powers.
- Great! Now add an update parameter to increment the level_required by 2.
- Now that we have a working update command, change it so that the update will apply to all documents that match the query.

```sh
db.wands.update( {"powers" : "Fire"}, {"$inc": {"level_required" : 2}}, {"multi": true}

)
```
2.6 User Chronicles

"We'd like to see which wands users are looking at most. 
To do this, we'll use the logs collection that contains documents that record the name a
and count for each wand."

- First, let's add the query parameter to find a wand with the name of "Dream Bender".
-  Great! Now add the update parameter to increment the count field by 1.
- Add the option that will create a new document if none match the query or update an existing document.

```sh
db.logs.update(
  {"name": "Dream Bender"},
  {"$inc" : {"count": 1}},
  {"upsert" : true}
)
```



2.8 Smelly Wands

" A few of the old wands included a smell field,
and we're not exactly sure why anyone thought that would be a relevant field.
Let's get rid of it!"

- Add the update parameter that will remove the smell field from all documents.

```sh
db.wands.update(
  {},
  {"$unset" : {"smell": ""}},
  {"multi": true}
)
```


### 2.9 Disgruntled Wand Makers
"We've been getting some complaints from wand makers that the term "creator" doesn't properly convey the true nature of their craft. 
To make them happy, we need to change the field creator to maker."

- Add the update parameter that will rename the creator field to "maker" for all documents.
```sh
db.wands.update(
  {},
  {"$rename" : {"creator": "maker"}},
  {"multi": true}
)
```

