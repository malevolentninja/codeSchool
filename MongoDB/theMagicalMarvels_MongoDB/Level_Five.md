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

