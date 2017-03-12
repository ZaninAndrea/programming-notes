# Haskell basics
<!-- toc -->
## Various
* boolean algebra: `&&`, `||`, `not`
* equality and inequality: `==`, `/=`
* strictly typed, but with type inference
* declaring a function e.g.
  ```haskell
  doubleMe x = x + x
  ```
* function are called in a cli-like manner: function name followed by paramaters separated by a space, you can use parenthesis
  * infix function: a function taking two parameters can be invoked writing the function name between the two parameters and surrounding his name in backticks 
    ```haskell
    92 `div` 10
    ```
  * explicit typing: `functionName :: types` types has to be separated by `->` and the last type is the return type, whereas all the others are parameter types e.g.
    ```haskell
    addThree :: Int -> Int -> Int -> Int  
    addThree x y z = x + y + z
    ```
* in the if statement the else is mandatory and is an expression, so it returns a value and you can use inside assignements
  ```haskell
  x = if x > 100  
    then x  
    else x*2
  ```
* `:t var` to return _var_'s type
* `Int` and `Integer` types both express numbers, but `Integer`is unbounded, so you can represent infinitely long integers. E.g. big factorials
  ```haskell
  factorial :: Integer -> Integer
  factorial n = product [1..n]  
  factorial 100
  ```
* type `Ordering` is a type that can have value `LT`,`GT`,`EQ` meaning greater than, lesser than and equal, respectively
* to write multiple expressions in the same line separate them with `;`
## Lists
* contain items of the same type
* strings are lists
* `++` to append a list to another, needs to loop through all the list, it's much more expensive than `:`
* `item:list` to put an item at the beginning of the list, instantanious
* `list !! index` to retrieve an element from the list
* `head` function returns the first element
* `tail` function returns a list containing every element but the first
* `last` function returns the last element
* `init` function returns a list containing every element but the last
* `length` return list length
* `null` check if the list is empty
* `reverse` reverses a list
* `take x list` return a list containing the first _x_ items
* `drop x list` returns a list containig all the items but the first _x_
* `maximum` and `minimum` functions return the maximum value and the minimum value contained in the list
  * works with string too using ascii
* `elem` function checks if the element is contained in the list, usually called like an inifix function 
  ```haskell
  4 `elem` [3,4,5,6]
  ```
* `[x..y]` returns a list of all the numbers between _x_ and _y_, works with numbers, chars, also in reverse order \(`[20..1]`\)
  * `repeat elem` same as cycle, but with a single element
  * `cycle list` takes a list and returns it repeated infinitely many time, use `take` when displaying
  * `[a, b..z]`: same as before, but every time increasing by `b-a`, works only with numbers
  * you can use `[x..]` to create an infinite list
* `map function list` returns a list where all the elements are replaced with the result of passing them to _function_ e.g. return a list with all the elements increased by one
```haskell
map (+1) [1..10]
```
* `filter predicate list`: return the list of elements that satisfied the predicate (a predicate is a function checking a condition and returning a boolean). Filter doesn't work on infinite lists
* `takeWhile predicate list` returns a list with all the elements up to the one that didn't satisfy the predicate, then stops. Works with infinite lists too
 
### List comprehension
* `[outputFunction | inputSet]`, inputSet's expressions have to be separated by commas and can be conditions \(`x /=5`\) or predicates which draw elements from a list \(`elem <- list`\) e.g. _all numbers from 50 to 100 whose remainder when divided with the number 7 is 3_
    ```haskell
    [ x | x <- [50..100], x `mod` 7 == 3]
    ```

* you can use `_` instead of a variable name if you will never use it e.g.
      ```haskell
      length' xs = sum [1 | _ <- xs]
      ```
      
## Tuples
Tuples are similar to lists, but their type depends on the number and the type of the  items they contain, so `(1,2)` and `(1,2,3)` have different types. Furthermore they can contain items of different type
* **syntax**: elements are wrapped inside `()` and separated by commas e.g. `(1,2,3)`
* `fst` and `snd` take a pair and return the first or second item
* `zip list1 list2` takes two lists and returns a list of tuples pairing corresponding elements, the longer list gets cut off to match the length of the sorther one. e.g. `zip [1,2] ["a","b"]` returns `[(1,"a"),(2,"b")]`

## Typeclasses
* typeclasses: A typeclass is a sort of interface that defines some behavior
  * typeclass `Eq` supports equality operators `==` and `/=`
  * typeclass `Ord` supports ordering `>`,`<`,`>=` and `<=`
  * typeclass `Show` can be presented as a string
  * typeclass `Read` can be parsed from a string, when used out of context gives error, so `read "4" + 2` works fine, but `read "4"` doesn't. You can use _explicit type annotations_ like this `read "4" :: Int` and it will work
  * typeclass `Bounded` has upper and lower boundaries
    * function `maxBound` and `minBound` return those boundaries e.g. `maxBound :: Int` evaluetes to `9223372036854775807`
  * typeclass `Num` includes every type that can act as a number
  * typeclass `Integral` includes every type that can act as an integer number: `Int` and `Integer`
  * typeclass `Floating` includes every type that can act as a floating point number: `Float` and `Double`

## Cool syntaxes
### pattern matching
You can define a function behaviour for a specific input e.g.
```haskell
lucky :: (Integral a) => a -> String  
lucky 7 = "LUCKY NUMBER SEVEN!"  
lucky x = "Sorry, you're out of luck, pal!"   
```
- only the first declaration matching is executed, similarly to a switch statement
- always include a chatch-all statement, otherwise the function will crash for unexpected inputs
- this can also work for recursive functions
```haskell
factorial :: (Integral a) => a -> a  
factorial 0 = 1  
factorial n = n * factorial (n - 1)  
```
- patterns: Those are a handy way of breaking something up according to a pattern and binding it to names whilst still keeping a reference to the whole thing. You do that by putting a name and an `@` in front of a pattern. For instance, the pattern `xs@(x:y:ys)`. This pattern will match exactly the same thing as `x:y:ys` but you can easily get the whole list via `xs` instead of repeating yourself by typing out `x:y:ys` in the function body again. E.g. 
```haskell 
capital :: String -> String  
capital "" = "Empty string, whoops!"  
capital all@(x:xs) = "The first letter of " ++ all ++ " is " ++ [x]  
```

### guards
Guards are a way of testing whether some property of a value (or several of them) are true or false e.g.
```haskell
bmiTell :: (RealFloat a) => a -> String  
bmiTell bmi  
    | bmi <= 18.5 = "You're underweight, you emo, you!"  
    | bmi <= 25.0 = "You're supposedly normal. Pffft, I bet you're ugly!"  
    | bmi <= 30.0 = "You're fat! Lose some weight, fatty!"  
    | otherwise   = "You're a whale, congratulations!"  
```
Guards are indicated by pipes that follow a function's name and its parameters. If it evaluates to True, then the corresponding function body is used. If it evaluates to False, checking drops through to the next guard and so on
We can use the keyword `where` after the guards to calculate some variables or functions used in the guards or in the function. In defining those variables you must indent all of them equally e.g.
```haskell
    bmiTell :: (RealFloat a) => a -> a -> String  
    bmiTell weight height  
        | bmi <= skinny = "You're underweight, you emo, you!"  
        | bmi <= normal = "You're supposedly normal. Pffft, I bet you're ugly!"  
        | bmi <= fat    = "You're fat! Lose some weight, fatty!"  
        | otherwise     = "You're a whale, congratulations!"  
        where bmi = weight / height ^ 2  
              skinny = 18.5  
              normal = 25.0  
              fat = 30.0  
```

### Let bindings
The form is `let <bindings> in <expression>`. The names that you define in the let part are accessible to the expression after the in part. Let bindings are expressions themselves. E.g.
```haskell
cylinder :: (RealFloat a) => a -> a -> a  
cylinder r h = 
    let sideArea = 2 * pi * r * h  
        topArea = pi * r ^2  
    in  sideArea + 2 * topArea  
```

### Case expressions
It's about taking a variable and then executing blocks of code for specific values of that variable and then maybe including a catch-all block of code in case the variable has some value for which we didn't set up a case. The syntax is:
```
case expression of pattern -> result  
                   pattern -> result  
                   pattern -> result  
                   ...  
```
e.g.
```haskell
describeList :: [a] -> String  
describeList xs = "The list is " ++ case xs of [] -> "empty."  
                                               [x] -> "a singleton list."   
                                               xs -> "a longer list."  
```

## Lambdas
Lambdas are anonymous function, generally passed to higher order functions
To make a lambda we write `\` followed by the 
parameters then a `->` and the function body
e.g.
```haskell
oddNumbers = filter (\x -> x mod 2 /=0) [1..100]
```

## Fold
The function `foldl function accumulator array` take a binary function (2 input one output) an accumulator and an array, then it "folds" the array passing the pair accumulator first value of the array to the function and replacing the accumulator with the result, then repeats the process with the next item, until the array has ended and we have only one value. The `foldl` folds the elements starting from left and going to right
e.g.recreating the sum function
```haskell
sum' xs= foldl (+) 0 xs
```

- `foldr` is the same as `foldl`, but folds from right to left
- `foldl1` and `foldr1` work the same as their counterparts, but don't take any accumulator, they use the first or last value of the array as accumulator and start applying the function with the next one
- `scanl` and `scanr` work as their fold counterparts, but store evry accumulator state in an array and then return that array. In `scanl` the first value of the accumulator is the first in the array, while in `scanr` is the last one. E.g. `scanl (+) 0 [3,5,2,1]` returns `[0,3,8,10,11]`

## Function application with $
The `$` function has the lowest precedence and is right-associative
```haskell
($) :: (a -> b) -> a -> b  
f $ x = f x  
```
It's commonly used to avoid using many parenthesis. E.g. `sum (map sqrt [1..130])` has the same result as ` sum $ map sqrt [1..130]`, but clearer to read

Given that `$`, as all functions, can be curried we can use it to pass the same parameter to a list of functions
E.g. 
```haskell
ghci> map ($ 3) [(4+), (10*), (^2), sqrt]  
[7.0,30.0,9.0,1.7320508075688772]  
```

## Function composition
In math function composition is defined like this : $$(f \circ g)(x) = f(g(x))$$
In haskell it works pretty much the same: we use the `.` function, which is defined like this:
```haskell
    (.) :: (b -> c) -> (a -> b) -> a -> c  
    f . g = \x -> f (g x)  
```
Function composition is right-associative, so `f(g(z x))`=`(f . g . z) x`

## Modules
To import a module just use `import <module name>`, this has to be done before defining any function.
- you can import only some functions like this `import Data.List (nub, sort)`
- you can import the module except some functions we can do this `import Data.List hiding (nub, sort)`
- you can import a module as `qualified` meaning that you'll have to use it's name to recall his functions. E.g. `import qualified Data.Map` and then use `Data.Map.filter`, or `import qualified Data.Map as M` and then use `M.filter`
