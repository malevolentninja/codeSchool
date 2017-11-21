# Level 1: Expressions

### Full Unless
```sh
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
if  !games.empty?
  puts "Games in your vast collection: #{games.count}"
end
```
- use unless instead of if

```sh
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
unless games.empty?
  puts "Games in your vast collection: #{games.count}"
end
```

### Inline statements
```sh
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
unless games.empty?
  puts "Games in your vast collection: #{games.count}"
end
```
- refactor to use a single line
```sh
games = ['Super Mario Bros.', 'Contra', 'Metroid', 'Mega Man 2']

puts "Games in your vast collection: #{games.count}" unless games.empty?
```

### Implied Nil
```sh
search = "Contra"
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
search_index = games.find_index(search)
if search_index != nil
  puts "Game #{search} Found: #{games[search_index]} at index #{search_index}."
else
  puts "Game #{search} not found."
end
```

- Let's implement a simple search feature - for our naive implementation, we
- search for a game by its exact title, and if it's found, we show it. Comparing
- something with nil in an if statement isn't needed in Ruby. Refactor the code
- below to run without the nil comparison.

```sh
search = 'Contra'
games = ['Super Mario Bros.', 'Contra', 'Metroid', 'Mega Man 2']

search_index = games.find_index(search)
if search_index
  puts "Game #{search} not found."
else
  puts "Game #{search} Found: #{games[search_index]} at index #{search_index}."
end
```

### Short-Circuit And
```sh
search = "Super Mario Bros."
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
matched_games = games.grep(Regexp.new(search))

# Found an exact match
if matched_games.length > 0
  if matched_games.include?(search)
    puts "Game #{search} found."
  end
end
```
- Let's clean up our code to make it search within each game title and show all the results. 
- If it's an exact match, we'll show something special. Clean up
- Short circuit the if statement.

```sh
search = 'Super Mario Bros.'
games = ['Super Mario Bros.', 'Contra', 'Metroid', 'Mega Man 2']
matched_games = games.grep(Regexp.new(search))
```

```sh
if matched_games.length > 0 && matched_games.include?(search)
  puts "Game #{search} found."
end
```


# Conditional Assignment
```sh
search = "" unless search
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
matched_games = games.grep(Regexp.new(search))
puts "Found the following games..."
matched_games.each do |game|
  puts "- #{game}"
end
```
- If no search is entered, we'll display all games. 
- Notice the first line where we're setting search to an empty string? 
- Change this to use

conditional assignment.rb
```sh
search ||= ''
games = ['Super Mario Bros.', 'Contra', 'Metroid', 'Mega Man 2']
matched_games = games.grep(Regexp.new(search))
puts 'Found the following games...'
matched_games.each do |game|
  puts "- #{game}"
end
```

# Conditional Return 1
```sh
search = "Contra"
games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
search_index = games.find_index(search)
if search_index
  search_result = "Game #{search} found: #{games[search_index]} at index #{search_index}."
else
  search_result = "Game #{search} not found."
end
puts search_result
```sh

- Clean up the code  to only set search_result once 
- Use a conditional return on the if statement.

conditional_return.rb
```sh
search = 'Contra'
games = ['Super Mario Bros.', 'Contra', 'Metroid', 'Mega Man 2']
search_index = games.find_index(search)

search_result = if search_index
  "Game #{search} found: #{games[search_index]} at index #{search_index}."
else
  "Game #{search} not found."
end

puts search_result
```

# Conditional Return II
```sh
def search(games, search_term)
  search_index = games.find_index(search_term)
  search_result = if search_index
    "Game #{search_term} found: #{games[search_index]} at index #{search_index}."
  else
    "Game #{search_term} not found."
  end
  return search_result
end

games = ["Super Mario Bros.", "Contra", "Metroid", "Mega Man 2"]
puts search(games, "Contra")
```

- One of the most common places to use conditional returns is within methods.
- Refactor the code, removing the search_result variable all together.

Refactored.rb
```sh
def search(games, search_term)
  search_index = games.find_index(search_term)
  if search_index
    "Game #{search_term} found: #{games[search_index]} at index #{search_index}."
  else
    "Game #{search_term} not found."
  end
end
```

# Short-Circuit Evaluation
```sh
def search_index(games, search_term)
  search_index = games.find_index(search_term)

  if search_index
    search_index
  else
    "Not Found"
  end
end
```
- Using Short-Circuit Evaluation can clean up your code a great deal. Update
- the following method to use short circuit evaluation. While you're at it,
- why not try reducing the entire method to one line?

Evaluation.rb
```sh
def search_index(games, search_term)
  games.find_index(search_term) || "Not Found"
end
```
