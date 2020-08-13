# C-Cheat-Sheet

## Table of Contents

- [Intro](#intro)
- [Include](#include)
- [Functions](#functions)
- [Strings](#strings)
- [Numbers](#numbers)
- [Boolean](#boolean)
- [Pointers](#pointers)
- [Struct](#struct)
- [Linked List](#linked-list)

## Intro
The C language is designed to create small, fast programs. It’s lower-level than most other languages; that means it creates code that’s a lot closer to what machines really understand. C is used where speed, space, and portability are important. Most operating systems are written in C. Most other computer languages are also written in C. And most game software is written in C.

## Include
C is a very, very small language and it can do almost nothing without the use of external libraries. You will need to tell the compiler what external code to use by including header files for the relevant libraries. The header you will see more than any other is stdio.h. The stdiolibrary contains code that allows you to read and write data from and to the terminal.

```c
#include <stdio.h>
```
File names between <angle brackets> are headers from the C standard library.
For your own headers, use double quotes instead of angle brackets:

```c
#include "my_header.h"
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

Each character is stored in the computer’s memory as a character code. And that’s just a number. So when the computer sees A, to the computer it’s the same as seeing the literal number 65 (the ASCII code for A).

If C is going to display a string on the screen, it needs to know when it gets to the end of the character array. And it does this by adding a sentinel character.

The sentinel character is an additional character at the end of the string that has the value \0. Whenever the computer needs to read the contents of the string, it goes through the elements of the character array one at a time, until it reaches \0. 

Strings end in a sentinel character so we have to allow for an extra character in the array. For example, a string that would only ever have one or two characters would have an index of 3:

```c
char card_name[3];
```

const char * is used for strings that you don’t want to change. That means it’s often used to record string literals.

```c
const char *my_str = "This is my very own string literal";
```
  
## Numbers

### Int
If you need to store a whole number, you can generally just use an int. The exact maximum size of an int can vary, but it’s guaranteed to be at least 16 bits. In general, an int can store numbers up to a few million.

```c
int x_int = 0;
```

### Short
Why use an int if you just want to store numbers up to few hundreds or thousands? That’s what a short is for. A short number usually takes up about half the space of an int. 

```c
short x_short = 0;
```

### Long
Yes, but what if you want to store a really large count? That’s what the long data type was invented for. On some machines, the long data type takes up twice the memory of an int, and it can hold numbers up in the billions. But because most computers can deal with really large ints, on a lot of machines, the long data type is exactly the same size as an int. The maximum size of a long is guaranteed to be at least 32 bits.

```c
long x_long = 0;
```

### Float
Float is the basic data type for storing floating-point numbers. For most everyday floating-point numbers—like the amount of fluid in your orange mocha frappuccino—you can use a float. 

```c
float x_float = 0.0f; // 'f' suffix here denotes floating point literal
```

### Double
If you want to perform calculations that are accurate to a large number of decimal places, then you might want to use a double. A doubletakes up twice the memory of a float, and it uses that extra space to store numbers that are larger and more precise. 

```c
double x_double = 0.0;
```

### Unsigned
The number will always be positive. Because it doesn’t need to worry about recording negative numbers, unsigned numbers can store larger numbers since there’s now one more bit to work with. So an unsignedint stores numbers from 0 to a maximum value that is about twice as large as the maximum number that can be stored inside an int. There’s also a signed keyword, but you almost never see it, because all data types are signed by default.

```c
unsigned short ux_short;
unsigned int ux_int;
unsigned long long ux_long_long;
```

### strstr()

The strstr() function will search for the second string in the first string. If it finds the string, it will return the address of the located string in memory.

```c
strstr("dysfunctional", "fun")
```

If nothing is found, it returns the value 0 (false). 

```c
char s0[] = "dysfunctional";
char s1[] = "fun";
if (strstr(s0, s1))  
    puts("I found the fun in dysfunctional!");
```

## Boolean
In C, boolean values are represented by numbers. To C, the number 0 is the value for false. Anything that is not equal to 0 is treated as true. So there is nothing wrong in writing C code like this:

```c
int people_moshing = 34;
if (people_moshing)    
  take_off_glasses();
```

## Pointers
A pointer is the address of a piece of data in memory. Instead of passing around a whole copy of the data, you can just pass a pointer. You can have two pieces of code to work on the same piece of data rather than a separate copy.

Every time you declare a variable, the computer creates space for it somewhere in memory. If you declare a variable inside a function like main(), the computer will store it in a section of memory called the stack. If a variable is declared outside any function, it will be stored in the globals section of memory. 

If you want to find out the memory address of the variable, you can use the & operator:

> %p is used to format addresses. 

```c
printf("x is stored at %p\n", &x);
```

The address of the variable tells you where to find the variable in memory. That’s why an address is also called a pointer, because it points to the variable in memory.

But once you’ve got the address of a variable, you may want to store it somewhere. To do that, you will need a pointer variable. A pointer variable is just a variable that stores a memory address. When you declare a pointer variable, you need to say what kind of data is stored at the address it will point to:

```c
int *address_of_x = &x;
```

When you have a memory address, you will want to read the data that’s stored there. You do that with the * operator:

```c
int value_stored = *address_of_x;
```

The * and & operators are opposites. The & operator takes a piece of data and tells you where it’s stored. The * operator takes an address and tells you what’s stored there. Because pointers are sometimes called references, the * operator is said to dereferencea pointer. 

If you have a pointer variable and you want to change the data at the address where the variable’s pointing, you can just use the *operator again. But this time you need to use it on the left side of an assignment:

```c
*address_of_x = 99;
```
## Struct
If you have a set of data that you need to bundle together into a single thing, then you can use a struct. The word struct is short for structured data type. A struct will let you take all of those different pieces of data into the code and wrap them up into one large new data type, like this:

```c
struct fish {  
    const char *name;  
    const char *species; 
    int teeth;  
    int age;
   };
   
   struct fish snappy = {"Snappy", "Piranha", 69, 4};
   printf("Name = %s\n", snappy.name);
```

C allows you to create an alias for any struct that you create. If you add the word typedefbefore the structkeyword, and a type nameafter the closing brace, you can call the new type whatever you like: 

```c
typedef struct cell_phone {  
    int cell_no;  
    const char *wallpaper;  
    float minutes_of_charge;
    } phone;
    
phone p = {5557879, "sinatra.png", 1.35};
```
typedefs can shorten your code and make it easier to read. 

If you want a function to update a struct variable, you can’t just pass the struct as a parameter because that will simply send a copy of the data to the function. Instead, you can pass the address of the struct: 

```c
void happy_birthday(turtle *a)
   {
    a->age = a->age + 1;  
    printf("Happy Birthday %s! You are now %i years old!\n",         
        a->name, a->age);
   }
```

## Linked List
To store a flexible amount of data, you need something more extensible than an array. Linked lists allow you to store a variable amount of data, and they make it simple to add more data.

### Create a recursive structure
Each one of the structs in the list will need to connect to the one next to it. A struct that contains a link to another struct of the same type is called a recursive structure.
 
```c
typedef struct island {  
    char *name;  
    char *opens;  
    char *closes;  
    struct island  *next; // Store a pointer to the next island in the struct.
   } island;
   
island amity = {"Amity", "09:00", "17:00", NULL};
island craggy = {"Craggy", "09:00", "17:00", NULL};
island isla_nublar = {"Isla Nublar", "09:00", "17:00", NULL};
island shutter = {"Shutter", "09:00", "17:00", NULL};
amity.next = &craggy;
craggy.next = &isla_nublar;
isla_nublar.next = &shutter;
island skull = {"Skull", "09:00", "17:00", NULL}
;isla_nublar.next = &skull;
skull.next = &shutter;
display(&amity);
```
