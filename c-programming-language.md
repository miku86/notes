# The C Programming Language

## ToC

1. Introduction
1. A Tutorial Introduction
1. Types, Operators and Expressions
1. Control Flow
1. Functions and Program Structure
1. Pointers and Arrays
1. Structures
1. Input and Output
1. The Unix System Interface
1. Reference Manual
1. Standard Library

## Introduction

- C is a compiled and general-purpose programming language, closely associated with the Unix system
- the language is not tied to any one operating system or machine
- useful for writing compilers and operating system, but also to write major programs in many different domains
- C provides a variety of data types, the fundamental ones are characters, integers and floats
- in addition, there is a hierarchy of types created with pointers, array, structures and unions
- expressions are formed from operators and operands, any expression can be a statement
- provides the fundamental control flow constructions like statement grouping, decision-making (if/else, switch), looping (for, while, do) and early loop exit (break)
- provides no operations to deal directly with composites such as strings, sets, lists or arrays
- no heap or garbage collection
- no I/O facilities and no file access methods
- offers only straightforward, single-threaded control flows
- not strongly-typed, but its type checking has been strengthened

## A Tutorial Introduction

- every program must have a `main` function

```c
#include <stdio.h>

int main()
{
  printf("hello world\n");
}
```

- first, compile: `gcc hello-world.c`
- second, run: `./a.out`

- `#include <stdio.h>` // standard I/O library
- `%d` to print a variable with a digit/int type
- semicolons at the end of statement
- most used basic data types: int, float, char, short, long, double
- integer divison truncates
- `#define name value` for magic numbers, e.g. `#define MAX 300`
- text I/O is dealt with as streams of chars, a text stream is a sequence of chars divided into lines, every line ends with a newline char
- `getchar()` reads the next input char
- `putchar(c)` prints the content
