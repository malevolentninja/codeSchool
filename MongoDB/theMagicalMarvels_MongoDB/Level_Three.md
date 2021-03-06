# The magical Marvels of MongoDB

## Level Three: Materializing Potions


### 3.2 Picky Preferences
"When it comes to wands, it's okay to be picky about which one we want."

- First, find all the wands where the maker is "Moonsap".
- Now, update the query to only retrieve wands that have a level_required of 5.

```sh
db.wands.find(
  {"maker": "Moonsap","level_required": 5}
)
```

### 3.3 Supernatural Stats 

"Believe it or not, some lower-level wands have better stats than those that are equal to our current level."


- Write a query for wands that have a level_required that is less than or equal to 5.

```sh
db.wands.find(
  {"level_required": {"$lte": 5}}
)
```

### 3.4 All You Need Is Love
"Wands can only have a few powers, so it's important to make sure your wand doesn't contain any powers you don't like."


- Write a query for wands that do not include "Love Burst" in their powers.

```sh
db.wands.find(
  {"powers": {"$ne": "Love Burst"}},
)
```

### 3.5 Marvelously Mighty Melee 

"At our current level, we can't do much magic damage yet, but we can do melee damage all the way up to 40."

- Let's find out which wands have a "damage.melee" that is greater than or equal to 30 and less than or equal to 40.

```sh
db.wands.find(
  {"damage.melee": {"$gte": 30, "$lte": 40}},
)
```

### 3.6 Bananas for Wands

"Wands come in a variety of lengths, and the magic folk use bananas for measurement.
We've added a new lengths field to each wand that contains an array of the different lengths a wand comes in.
To find a proper wand, we'll need one that fits our size."


- Write a query that will find any wands that contain lengths that are greater than or equal to 2.5 but less than 3. Remember, arrays can be tricky!

```sh
db.wands.find(
  {"lengths": {"$elemMatch":{"$gte": 2.5, "$lt": 3}}}
)
```


### 3.7 Merlin's Mythical Madness 
"Now that we're getting pretty good at finding wands, let's find the perfect wand for our friend Merlin."


- Merlin's first requirement is the wand must not be made by "Foxmond"

- Write the query to find wands that don't have "Foxmond" as the maker
- Next, Merlin's level is 75 so we'll want to add a query for a level_required that is less than or equal to 75.
- Merlin doesn't want to spend more than 50 gems. Add another query that makes sure the price is less than 50.
- Lastly, make sure the wand is 3 to 4 banana lengths. Remember, arrays can be tricky!

```sh
db.wands.find(
  {"maker": {"$ne": "Foxmond"},
  "level_required": {"$lte": 75},
   "price": {"$lt": 50},
   "lengths": {"$elemMatch": {"$gte": 3, "$lte": 4 }}

  }
);
```
