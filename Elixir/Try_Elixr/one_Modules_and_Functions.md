# Level 1: Modules & Functions
- Get started in the world of functional programming with Elixir by learning how to work with named functions.

### 1.2 Calculating Investment
Let’s write a simple function that calculates how much money we've made from our recent investment of $1,000.00 at a 0.01% rate of return.
- Define a new module named Account.
- Inside the new module, define a function named investment_return. This function should accept two arguments: initial and interest.
- Fill in the body of the function with the following operation: initial + (initial * interest)

```sh
defmodule Account do
  def investment_return(initial, interest) do
    initial + (initial * interest)
  end
end
amount = Account.investment_return(1000, 0.0001)
IO.puts "Investment return: $#{amount}"
```

### 1.3 About Elixir
Which one of the following statements is true?

- In Elixir, there are no classes or objects, just modules and functions.


### 1.4 Programming Paradigm
Complete the following statement.

- In functional programming languages like Elixir, computation is treated as transformation of data through functions.

### 1.5 Running the Code

Elixir is a compiled language. What is the result of running Elixir source code through the Elixir compiler?
```sh
Bytecode
```
