- boolean algebra: `&&`, `||`, `not`
- equality and inequality: `==`, `/=`
- strictly typed, but with type inference
- declaring a function e.g.
```haskell
doubleMe x = x + x  
```
- function are called in a cli-like manner: function name followed by paramaters separated by a space, you can use parenthesis
    - infix function: a function taking two parameters can be invoked writing the function name between the two parameters and surrounding his name in backticks <pre> 92 `div` 10 </pre>
- in the if statement the else is mandatory and is an expression, so it returns a value and you can use inside assignements
```haskell
x = if x > 100  
    then x  
    else x*2 
```
- lists
    - contain items of the same type
    - strings are lists
    - `++` to append a list to another, needs to loop through all the list
    - `item:list` to put an item at the beginning of the list, instantanious
    - `list !! index` to retrieve an element from the list