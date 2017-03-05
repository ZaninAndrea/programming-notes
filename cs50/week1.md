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
```
int return3(void){
    return 3;
}
```



