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

