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
Declaring the functions at the top of the code allows you toinvoke a function from another one implemented upper in the code.
To declare a function without inputs write `void` in place of the argument list

## Schort: Variables and Scope
Global variables are useful, because they are **passed by value** to methods, instead that passing a copy.