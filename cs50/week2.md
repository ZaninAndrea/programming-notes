# Week 2
<!-- toc -->
## Lecture
- debugging
    - `<cs50.h>` library includes the method `eprintf()` to printf a string only when debugging
    - in the cs50 IDE there is a debugger called debug50, you can use it through cli `debug50 executableFile`, you can use breakpoints by clicking the line number
    - rubber duck technique: try to explain your code and your error
- cryptography
    -secret key cryptography: to decrypt you reverse the input and the output, but keeping the key
- string
    - actually they are only characters array
    - are null terminated with `\0`
    - `<ctype.h>` contains various function, e.g. `toupper()`
- for loop
    - I can declare multiple variables in the for declaration: just separe the declarations with commas
- typecasting
    - `(type) var` converts **var** to type **type**
    - char and int can be implicitly casted
- main
    - main arguments through command line: `int main(int argc, string argv[])` argc is the number of arguments and argv contains every argument. The first argument is always the command called (your program).
   - we can return an exit code (by default 0 is returned) e.g. `return 2`
       - to see this exit code use `echo $?`
       
## Short: Functions
Declaring the functions at the top of the code allows you to invoke a function from another one implemented upper in the code.
To declare a function without inputs write `void` in place of the argument list

## Short: Variables and Scope
Global variables are useful, because they are **passed by value** to methods, instead that passing a copy. CHECK THIS

## Short: Arrays
Arrays are blocks of contiguous space in memory that are partitioned into identically-sized elements. All elements have the same type and can be accessed by an index (starting from 0)

**One-dimensional**
Declaration: `type name[size]`
Instantiation: `type name[size]={elem1, elem2, ... elemN}`, specifying size is optional
Accessing: `name[index]`

**Multi-dimensional**
Declaration: `type name[sizeX][sizeY][sizeZ]`
Accessing: `name[indexX][indexY][indexZ]`

In C you can't assign an array to another array, so the following code is NOT legal
```
int foo[5]={1,2,3,3,10};
int bar[5];

bar=foo;
```

Array are **passed by reference**

## Short: Command-line arguments
You can declare `main` as requirind an `int` and an `array` as inputs, which are usually called `argc` (argument count) and `argv` (argument vector).

```
int main(int argc, string argv[]){

}
```

## Short: Magic numbers
Avoid using magic numbers in your code, i.e. having constants appear in the code without being clear why they have to be fixed to that value.

Use a **preprocessor directive** instead: `#define NAME REPLACEMENT`, at compile time the preprocessor will replace `NAME` with `REPLACEMENT`. Typically we name those constants all upper-case to avoid confusing them with variables.