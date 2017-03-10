- boolean algebra: `&&`, `||`, `not`
- equality and inequality: `==`, `/=`
- strictly typed, but with type inference
- declaring a function e.g.
```haskell
doubleMe x = x + x  
```
- function are called in a cli-like manner: function name followed by paramaters separated by a space, you can use parenthesis
    - infix function: a function taking two parameters can be invoked writing the function name between the two parameters and surrounding his name in backticks 
```haskell
92 `div` 10
```
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
    - `head` function returns the first element
    - `tail` function returns a list containing every element but the first
    - `last` function returns the last element
    - `init` function returns a list containing every element but the last
    - `length` return list length
    - `null` check if the list is empty
    - `reverse` reverses a list
    - `take x list` return a list containing the first _x_ items
    - `drop x list` returns a list containig all the items but the first *x*
    - `maximum` and `minimum` functions return the maximum value and the minimum value contained in the list
        - works with string too using ascii
    - `elem` function checks if the element is contained in the list, usually called like an inifix function 
```haskell
4 `elem` [3,4,5,6]
``` 
    - `[x..y]` returns a list of all the numbers between *x* and *y*, works with numbers, chars, also in reverse order (`[20..1]`)
        - `[step, x..y]`: same as before, but every time increasing by *step*, works only with numbers
    - `cycle list` takes a list and returns it repeated infinitely many time, use `take` when displaying
    - `repeat elem` same as cycle, but with a single element
    