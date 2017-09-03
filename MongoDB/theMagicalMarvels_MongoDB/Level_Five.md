## Level Five: Aggregation Appartitions

### 5.2 Many Makers
"Not only have we been adding wands, but our users have been adding new ones daily! 
Let's create a list of all the unique wand makers in our database."

- Write an aggregate to group wands by their maker so that we'll get a list of unique makers.

```sh
db.wands.aggregate(
  [{"$group": {"_id": "$maker", "wand": {"$sum": 5}}}]

)
```

### 5.3 Detecting Damage 
"Most of our users only care about the magic damage for their wand. 
After all, what's the point of doing awesome spells at low levels? 
Let's find out how many wands we have for each damage.magic score."


- Write an aggregate that groups wands by their damage.magic.
- Add an accumulator with a wand_count field to count the number of wands per damage.magic score.

```sh
db.wands.aggregate( [
  {"$group": {"_id": "$damage.magic", "wand_count": {"$sum": 1}}}
] )
```

### 5.4 Royal Connoisseurs
"Our site is a popular resource for wand collectors to find wands by makers they don't yet have. 
One ambitious connoisseur has asked how much it would cost to buy all the wands for each vendor. 
Let's find out!"


- Write an aggregate that groups our wands by the maker field.
- Add an accumulator with the total_cost field that sums the price for each wand per maker.

```sh
db.wands.aggregate([
  {"$group": {
    "_id": "$maker",
    "total_cost": {"$sum": "$price"}
  }

  }
])
```

### 5.5 Mischievous Makers
"They say that knowledge is power. 
Let's see what sort of interesting information we can find out based on the data we have. 
We have a slight suspicion that wand makers like to charge more for wands at "monumental levels". 
Time to prove it!"

- Write an aggregate to group wands by their level_required.
- Add an accumulator with a field named price_average to get the average price for the wands per level.

```sh
db.wands.aggregate([
  {"$group": {"_id": "$level_required",
  "price_average": {"$avg": "$price" }}}
])
```
