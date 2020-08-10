# C-Cheat-Sheet

## Table of Contents

- [Intro](#intro)
- [Include](#include)
- [Functions](#functions)
- [Strings](#strings)
- [Boolean](#boolean)



## Intro
The C language is designed to create small, fast programs. It’s lower-level than most other languages; that means it creates code that’s a lot closer to what machines really understand. C is used where speed, space, and portability are important. Most operating systems are written in C. Most other computer languages are also written in C. And most game software is written in C.

## Include
C is a very, very small language and it can do almost nothing without the use of external libraries. You will need to tell the compiler what external code to use by including header files for the relevant libraries. The header you will see more than any other is stdio.h. The stdiolibrary contains code that allows you to read and write data from and to the terminal.

```c
#include <stdio.h>
```

## Functions
All C code runs inside functions. The most important function you will find in any C program is called the main() function. The main()function is the starting point for all of the code in your program.

The computer will start running your program from the main()function. The name is important: if you don’t have a function called main(), your program won’t be able to start.

The main() function has a return type of int. So what does this mean? Well, when the computer runs your program, it will need to have some way of deciding if the program ran successfully or not. It does this by checking the return value of the main() function. If you tell your main() function to return 0, this means that the program was successful. If you tell it to return any other value, this means that there was a problem. 

```c
int main()
{    
    int decks;    
    puts("Enter a number of decks");    
    scanf("%i", &decks);    
    if (decks < 1) {        
      puts("That is not a valid number of decks");        
      return 1;    
    }   
    printf("There are %i cards\n", (decks * 52));   
    return 0;
 }
 ```
 
### Void Functions
Most functions in C have a return value, but sometimes you might want to create a function that has nothing useful to return. It might just do stuff rather than calculate stuff. Normally, functions always have to contain a return statement, but not if you give your function the return type void:

```c
void complain() 
{  
    puts("I'm really not happy");
}
```

In C, the keyword void means it doesn’t matter. As soon as you tell the C compiler that you don’t care about returning a value from the function, you don’t need to have a return statement in your function.

 ## Strings
The C language doesn’t support strings out of the box. C is more low-level than most other languages, so instead of strings, it normally uses something similar: an array of single characters.

If C is going to display a string on the screen, it needs to know when it gets to the end of the character array. And it does this by adding a sentinel character.

The sentinel character is an additional character at the end of the string that has the value \0. Whenever the computer needs to read the contents of the string, it goes through the elements of the character array one at a time, until it reaches \0. 

Strings end in a sentinel character so we have to allow for an extra character in the array. For example, a string that would only ever have one or two characters would have an index of 3:

```c
char card_name[3];
```

## Boolean
In C, boolean values are represented by numbers. To C, the number 0 is the value for false. Anything that is not equal to 0 is treated as true. So there is nothing wrong in writing C code like this:

```c
int people_moshing = 34;
if (people_moshing)    
  take_off_glasses();
```
