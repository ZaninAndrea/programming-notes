# Week 1
<!-- toc -->
## Lecture
- You an use an online IDE at [cs50.io](cs50.io)
- On the ide you can use the cs50 library for many abstractions (string, get_int,...) while you are still learning, later on you'll implement them yourself

```c
#include <cs50.h>
```
- to print a string containing a varibale you can use this syntax

```c
printf("here is some text and then a variable: text %s %i", stringVariable, intVariable);
```
The %-word indicates the type of the variable, the parameters following the first are the variables themselves (they have to be in order as they are in the text)
Here is a handy table of the %-words and meaning of the type:

|word|type|meaning|
|---|---|---|
|%c|char|a single character|
|%s|char*|string|
|%i|int|integer number|
|%f|float|floating point number|
|%d|double|32 bit float|
|%lld|long long|64 bit integer|

- if you divide 2 integers it will return the quotient
- to make **c** understand that a number is a float instead of int you can add `.0` like in `float x = 5.0`
- you can get the size of a variable through the method `sizeof(type)`
- when yourun out of space to store value in a number-type variable it will overflow (numbers will not be counted as expected and bugs will happen)
- the computer can be imprecise in representing numbers, for example in base 10 the number $$\frac{1}{3}$$ is not representable in a finite amount of digits, similarly in base 2 the number $$\frac{1}{10}$$ can't be represented in a finite amount of digits
- a function has to be declared before you can invoke it, sometimes it can be useful  to declarate the function at the top of the code and implementit later like this

```c
#include <stdio.h>
#include <cs50.h>

void print_name(string name);

int main(void){
    string s = get_string()
    print_name(s);
}

void print_name(string name){
    printf("hello %s\n", name);    
}
```

- a function that takes no argument has to be declaared with void as argument

```c
int return3(void){
    return 3;
}
```
- steps took by the pc to go from source code to running problam:
    - preprocessing: run preprocessing commands (like `#include <stdio.h>` to copy and paste the content of *stdio.h* in that point ofthe code)
    - compiling: from source code to assembly
    - assemble: from assembly to binary
    - linking: replacing methods with their implementation?

## Short: Command Line
- commands:
    - **ls**: lists the files in the current directory. Files marked with * are executables
    - **cd *destination***: change directory to the one passed e.g. `cd pset1`
        - `.` is the current directory
        - `..` is the upper directory
        - `~` for absolute path
    - **pwd** returns the name of the current directory
    - **mkdir *name***: create a new directory e.g. `mkdir workspace/newfolder`
    - **cp *source* *destination***:  copy sourcefile to destination
        - destination can both be a directory or a file, if it's a directory and you are copying a file the file will have the same name as source
        - use flag `-r` to copy a folder
    - **rm *file***: to remove a file
        - use flag `-f` to avoid making the warn appear
        - use flag `-r` to remove a directory
    - **mv *origin* *destination* **: to move or rename a file/directory
    - other commmands to explore: chmod, ln, touch, rmdir, man, diff, sudo, clear, telnet