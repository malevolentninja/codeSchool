
# Level 3: Pattern Matching

### 3.2 The Equal Symbol
The = symbol in Elixir matches values on one side against corresponding structures on the other side. This symbol is called:
The match operator.


### 3.3 String Concantenation
On the following code snippet, what value is matched with and assigned to the variable adj and printed to the console?
```sh
"Elixir is fun" <> adj = "Elixir is functional"
IO.puts adj
```


### 3.4 Pattern matching on lists
Let's use pattern matching to read individual elements from a list.
- Use pattern matching to read the individual elements from the withdrawals list so the code runs properly and prints the following text to the console:
```sh
Gym: $50.0, Cell Phone: $60.75, Netflix: $12.0

withdrawals = [50.0, 60.75, 12.0]

        [gym, cell_phone, netflix]  = withdrawals

IO.puts "Gym: $#{gym}, Cell Phone: $#{cell_phone}, Netflix: $#{netflix}"
```

### 3.5 Listing Desposits

The Account.list_deposits function below prints a list of deposits passed as an argument. 
- When called with just the list of deposits as its only argument, it should sort the deposits in ascending order. 
- There is a second version of the list_deposits function, with two clauses which take the sorting order as the second argument. This second argument is an atom that can be either :asc or :desc. 
Complete the following code so that it prints the expected result.
  - In the body of the list_deposits(deposits) function, 
  - finish the code so that it calls the clause of list_deposits which takes :asc as its second argument.
-In the body of the list_deposits(deposits, :desc) function, call the sort_desc function with deposits as its argument.
    -  Then, using the pipe operator, pass the result of this function call as the argument to the list function.

```sh
defmodule Account do
  def list_deposits(deposits) do
    list_deposits(deposits,:asc)
  end

  def list_deposits(deposits, :asc) do
    sort_asc(deposits) |> list
  end

  def list_deposits(deposits, :desc) do
      sort_desc(deposits) |> list
  end

  def sort_desc(deposits) do
    Enum.sort(deposits, &(&1 > &2))
  end

  def sort_asc(deposits) do
    Enum.sort(deposits, &(&1 < &2))
  end

  def list(sorted_deposits) do
    IO.inspect Enum.map(sorted_deposits, &("US$#{&1}"))
  end
end

Account.list_deposits([9.50,5.0,13.0,3.0,1.0])
```
