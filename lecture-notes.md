# CS1010 Programming Methodology - Lecture Notes
*By Seojin*

<details>

<summary> Table of contents</summary>

* [CS1010 Programming Methodology - Lecture Notes](#cs1010-programming-methodology---lecture-notes)
    * [Admin matters](#admin-matters)

* [L0: Introduction](#l0-introduction)
    * [0.0 Programming](#00-programming)
    * [0.1 Basic Program](#01-basic-program)
    * [0.2 Variables and data storage](#02-variables-and-data-storage)
        * [0.2.1 Variables](#021-variables)
        * [0.2.2 Format Specifiers](#022-format-specifiers)
    * [0.3 Arithmetic Operators](#03-arithmetic-operators)
    * [0.4 Assignment Operators](#04-assignment-operators)
    * [0.5 Ternary Operators](#05-ternary-operators)

* [L1: Conditionals and Functions](#l1-conditionals-and-functions)
    * [1.1 Abstraction I: Functions](#11-abstraction-i-functions)
    * [1.2 Conditional Statements](#12-conditional-statements)
        * [1.2.1 If/else constructs](#121-ifelse-constructs)
        * [1.2.2 Comparison and logical operators](#122-comparison-and-logical-operators)
        * [1.2.3 Boolean operators](#123-boolean-operators)

* [L2: Abstractions, Structs, and the Stack](#l2-abstractions-structs-and-the-stack)
    * [2.1 Abstraction II: Functions](#21-abstraction-ii-functions)
        * [2.1.1 Abstraction of Behavior: Functions](#211-abstraction-of-behavior-functions)
        * [2.1.2 Abstraction of Data: Structs](#212-abstraction-of-data-structs)
    * [2.2 The Stack and Block Scoping](#22-the-stack-and-block-scoping)
        * [2.2.1 Stack Frames](#221-stack-frames)
        * [2.2.2 Local variables](#222-local-variables)

* [L3: To be updated](#l3-to-be-updated)

</details>

### Admin matters:

**Instructors**:
- Dr. Eldon Chung
- Dr. Sriram Sami

**Schedule**:
| Activity | Time | Venue |
| -------- | ---- | ----- |
| Lecture | Monday 4pm-6pm | I3-LT38 |
| Tutorial | Wednesday 9am-10am | COM1-0120|
| Lab | Thursday 4pm-6pm | COM1-0120 |

**Exams**:
| Activity | Date | Time |
|--------- | ---- | ---- |
| Practical Exam | Tue, 15 Sep | 6pm-9pm |
| Midterm | Mon, 5 Oct | 4pm-6pm |
| Practical Exam | Tue, 13 Oct | 6pm-9pm |
| Practical Exam | Tue, 10 Nov | 6pm-9pm |
| **Final** | Wed, 25 Nov | 9am-11am |

**More info**:
[CS1010 website](https://cs1010.org)

# L0: Introduction

## 0.0 Programming

*Program*
: is a set of instructions that a computer runs.

*Programming*
: is writing code that is used to create a program.

More specifically,
1. The **CPU** (Central Processing Unit) reads information from the computer memory.
2. The CPU then writes information to the *Program Code*. The program code that we make is stored in the memory.
3. The Program stores data (Program data) for intermediate steps. These are also stored in memory.
\\
- We write in a higher-level programming language like C to create instructions that the CPU has to execute. A **compiler** (e.g. `clang` or `gcc`) takes the C code and produces assembly code.
- We use high-level language and compilers so that our code is *portable*; we leave lower level details to be handled by the compiler.
- We also leave hardware level optimisations to be hadnled by compilers.

**C**
: is a *compiled* progrmaming lanugage.

*Compiler*
: has to take C code written to produce assemlby instructions that the CPU will execute.

| Pros | Cons |
| ---- | ---- |
| lots of control: imperative, low level | More work required by programmer |
| Simple language | Many footguns |
| little to no overhead | |

Nevertheless, C is:
- Low-level enough for hardware (firmware)
- Widely supported across embedded systems
- Pervasive in system code
- Good starter language.

## 0.1 Basic Program
Anatomy:
```c
#include <stdio.h>
int main(void) {
    printf("Hello world!\n");
    return 0;
}
```
1. `#include <stdio.h>` makes the C "standard input/output" header file available to this program.
2. `int main(void) {` declares the main function, and code **starts** executing from within `main`. The `void` means that the function does not take any input arguments. the opening brace `{` means the the start of the code within `main`.
3. `    printf("Hello world!\n");` Creates a string `"Hello world!"` and a new line character `\n` and  passes the argument to `printf`, which is sent to the standard output of the program
4. Semicolon `;`  indicates the end of the statement.
5. Closing brace `}` ends the code within `main`. 

**Procedure**:
1. Create file with extension .c, (*e.g.*  `hello.c`)
2. Write C code inside.
3. Compile C code to an executable program\\
```bash
clang -o hello hello.c
```
4. Run if no errors.
```bash
./hello
```

## 0.2 Variables and data storage

### 0.2.1 Variables

Variables:
| **Type name(s)** | **Min value** | **Max value** | **Size (bytes)** |
| ------ | ------- | -------- | ------ |
| `char` | -128 | +127 | 1 (8 bits) |
| `unsigned char` | 0 | +255 | 1 (8 bits) |
| `int` | -32768 (-$2^{15}$) | +32767 ($2^{15}-1$) | 2 |
| `unsigned int` | 0 | +65535 ($2^{16}-1$) | 2 |
| `long` | -2147483648 ($2^{31}$) | +2147483647 ($2^{31}-1$) | 4 |
| `unsigned long` | 0 | +4294967295 ($2^{32}-1$) | 4 |
| `unsigned long long` | 0 | $2^{64}-1$ | 8 |
| `float` | 6-7 d.p. | 6-7 d.p. | 4 |
| `double` | 15-17 d.p. | 15-17 d.p.  | 8 |

*When to use which type*
- `char` for ASCII characters
- `int` for default integral types
- `unsigned int` if integer > 0
- `float` if you want to save memory and use decimals.
- `double` if your values might be more precise decimal. Use double and instead of float, unless with good reason.

*Initialization*
You can also initialize a variable without declaring its value.

```c
int a;
int b;
a = 372;
b = a - 200;
``` 

**Overflow**
If you have an `unsigned int` number at 255, and you increment it, you'll get 256 in return. As expected. If you have an `unsigned char` number at 255, and you increment it, you'll get 0 in return. It resets starting from the initial possible value.

If you have a `unsigned char` number at 255 and you add 10 to it, you'll get the number 9:

```c
#include <stdio.h>

int main(void) {
    unsigned char j = 255;
    j = j + 10;
    printf("%u", j); /* 9 */
}
```
If you don't have a signed value, the behavior is undefined. It will basically give you a huge number which can vary, like in this case:

```c
#include <stdio.h>

int main(void) {
    char j = 127;
    j = j + 10;
    printf("%u", j); /* 4294967177 */
}
```
In other words, C does not protect you from going over the limits of a type. You need to take care of this yourself. However, if you initialize a variable with a wrong value, you will likely receive a warning:

```c
#include <stdio.h>

int main(void) {
    char j = 1000;
    char i;
    i = 9999;
    // This will give warning.
}
```

However, incrementing the number will not give a warning and overflow.
```c
#include <stdio.h>

int main(void) {
    char j = 0;
    j += 1000;
}
```

**ASCII table:**
| Dec | Symbol | Dec | Symbol | Dec | Symbol | Dec | Symbol | Dec | Symbol |
|----:|:------:|----:|:------:|----:|:------:|----:|:------:|----:|:------:|
| 48 | 0 | 63 | ? | 78 | N | 93 | `]` | 108 | l |
| 49 | 1 | 64 | @ | 79 | O | 94 | ^ | 109 | m |
| 50 | 2 | 65 | A | 80 | P | 95 | _ | 110 | n |
| 51 | 3 | 66 | B | 81 | Q | 96 | ` | 111 | o |
| 52 | 4 | 67 | C | 82 | R | 97 | a | 112 | p |
| 53 | 5 | 68 | D | 83 | S | 98 | b | 113 | q |
| 54 | 6 | 69 | E | 84 | T | 99 | c | 114 | r |
| 55 | 7 | 70 | F | 85 | U | 100 | d | 115 | s |
| 56 | 8 | 71 | G | 86 | V | 101 | e | 116 | t |
| 57 | 9 | 72 | H | 87 | W | 102 | f | 117 | u |
| 58 | : | 73 | I | 88 | X | 103 | g | 118 | v |
| 59 | ; | 74 | J | 89 | Y | 104 | h | 119 | w |
| 60 | < | 75 | K | 90 | Z | 105 | i | 120 | x |
| 61 | = | 76 | L | 91 | `[` | 106 | j | 121 | y |
| 62 | > | 77 | M | 92 | \ | 107 | k | 122 | z |

It is possible to find the size of a variable.

**sizeof()**
```c
#include <stdio.h>
int main(void) {
    int myInt;
    float myFloat;
    double myDouble;
    char myChar;
    printf("%d\n", sizeof(myInt));
    printf("%d\n", sizeof(myFloat));
    printf("%d\n", sizeof(myDouble));
    printf("%d\n", sizeof(myChar));
    return 0;
}
```

output:
```terminal
4
4
8
1
```


### 0.2.2 Format Specifiers

*Format specifiers*
| **Specifier** | **Output** | **Example** |
| ------ | ------- | ------ |
| `d` or `i` | Signed decimal integer | `392` |
| `u` | Unsigned decimal integer | `7235` |
| `o` | Unsigned octal | `610` |
| `x` | Unsigned hexadecimal integer | `7fa` |
| `X` | Unsigned hexadecimal integer (uppercase) | `7FA` |
| `f` | Decimal floating point, lowercase | `392.65` |
| `F` | Decimal floating point, uppercase | `392.65` |
| `e` | Scientific notation (mantissa/exponent), lowercase | `3.9265e+2` |
| `E` | Scientific notation (mantissa/exponent), uppercase | `3.9265E+2` |
| `g` | Shortest representation: `%e` or `%f` | `392.65` |
| `G` | Shortest representation: `%E` or `%F` | `392.65` |
| `a` | Hexadecimal floating point, lowercase | `-0xc.90fep-2` |
| `A` | Hexadecimal floating point, uppercase | `-0XC.90FEP-2` |
| `c` | Character | `a` |
| `s` | String of characters | `sample` |
| `p` | Pointer address | `b8000000` |
| `n` | Nothing printed. Argument must be a pointer to a signed `int`; the number of characters written so far is stored there. | — |
| `%` | A literal `%` character | `%` |


Below is an example:
```c
#include <stdio.h>

int main(void) {
    int sixtyseven = 67;
    double pi = 3.1415926535897;
    char ahh = 'a';
    char pain[] = "what?"; //adding [] to the end of the variable will make it a string instead of a char
    printf("Integer: %d\n", sixtyseven);
    printf("2dp Float: %.2f\n", pi);
    printf("6dp Float: %.6f\n", pi);
    printf("Char: %c\n", ahh);
    printf("String: %s\n", pain);

    return 0;
}
```

**Integer Truncation**
When you output the value of `double` with `%d`, you will get the *floor* of the value, truncating the decimal point and leaving the integer part.
```c
int x = 5;
x = x + 0.1; // Behind the scenes: (int)((double)5.0 + 0.1)
printf("%d", x); 
```
<!-- to be updated below this line-->
## 0.3 Arithmetic Operators



## 0.4 Assignment Operators

## 0.5 Ternary Operators

# L1: Conditionals and Functions
## 1.1 Abstraction I: Functions
## 1.2 Conditional Statements
### 1.2.1 If/else constructs
### 1.2.2 Comparison and logical operators
### 1.2.3 Boolean operators  

# L2: Abstractions, Structs, and the Stack
##  2.1 Abstraction II: Functions 
### 2.1.1 Abstraction of Behavior: Functions
### 2.1.2 Abstraction of Data: Structs
## 2.2 The Stack and Block Scoping
### 2.2.1 Stack Frames
### 2.2.2 Local variables

# L3: To be updated
