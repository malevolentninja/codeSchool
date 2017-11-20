
# Level 2: The Pipe Operator


### 2.2 Piping Strings
In Elixir, we can pipe strings to functions like this:
```sh
"Some string" |> SomeModule.some_function
```
In this challenge, we'll use the string "Elixir" with the String.upcase function from Elixir's standard library, which takes a string and converts its characters to uppercase.
- Change the following code snippet to use the pipe operator |> twice.


Before: 
```sh
IO.puts String.upcase("Elixir")
```

After I Added Pipe:
```sh
"Elixir" |> String.upcase |> IO.puts
```

### 2.3 Name Format
The Person.format_name function takes a full name as a single argument and returns a version of the name formatted for a specific report. The formatted version includes the last name capitalized, followed by a comma, followed by the first name. For example, it takes the string "José Valim" and returns the string "VALIM, José".
- Use the pipe operator ```sh |> ```twice to clean up our code.


Before:
```sh
defmodule Person do
  def format_name(full_name) do
    format(String.split(full_name))
  end

  def format(parts) do
    first = Enum.at(parts, 0)
    last = Enum.at(parts, 1)
    "#{String.upcase(last)}, #{first}"
  end
end 

IO.puts Person.format_name("José Valim")

```

After:
```sh
defmodule Person do
  def format_name(full_name) do
   (full_name) |>String.split |> format
  end

  def format(parts) do
    first = Enum.at(parts, 0)
    last = Enum.at(parts, 1)
    "#{String.upcase(last)}, #{first}"
  end
end 

IO.puts Person.format_name("José Valim")

```
