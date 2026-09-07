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
    * [0.3 Arithmetic and Assignment Operators](#03-arithmetic-and-assignment-operators)
        * [0.3.1 Arithmetic Operators](#031-arithmetic-operators)
        * [0.3.2 Unary operators](#032-unary-operators)
        * [0.3.3 Comparison Operators](#033-comparison-operators)
        * [0.3.4 Logic Operators](#034-logic-operators)
        * [0.3.5 Assignment Operators](#035-assignment-operators)
        * [0.3.6 Integer Division](#036-integer-division)
        * [0.3.7 Division with `double`](#037-division-with-double)
        * [0.3.8 Operator Precedence](#038-operator-precedence)
    * [0.4 Ternary Operators](#04-ternary-operators)
        * [Common condition tests](#common-condition-tests)
    * [0.5 Undefined Behaviour](#05-undefined-behaviour)
        * [Example: Division by zero](#example-division-by-zero)
        * [Integer Overflow](#integer-overflow)
        * [Key takeaway](#key-takeaway)
    * [0.X Lab](#0x-lab)

* [L1: Conditionals and Functions](#l1-conditionals-and-functions)
    * [1.1 Abstraction I: Functions](#11-abstraction-i-functions)
    * [1.2 Conditional Statements](#12-conditional-statements)
        * [1.2.1 If/else constructs](#121-ifelse-constructs)
        * [1.2.2 Comparison and logical operators](#122-comparison-and-logical-operators)
        * [1.2.3 Boolean operators](#123-boolean-operators)
    * [1.X Lab](#1x-lab)

* [L2: Abstractions, Structs, and the Stack](#l2-abstractions-structs-and-the-stack)
    * [2.1 Abstraction II: Functions](#21-abstraction-ii-functions)
        * [2.1.1 Abstraction of Behavior: Functions](#211-abstraction-of-behavior-functions)
        * [2.1.2 Abstraction of Data: Structs](#212-abstraction-of-data-structs)
    * [2.2 The Stack and Block Scoping](#22-the-stack-and-block-scoping)
        * [2.2.1 Stack Frames](#221-stack-frames)
        * [2.2.2 Local variables](#222-local-variables)
    * [2.X Lab](#2x-lab)

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

## 0.3 Arithmetic and Assignment Operators

### 0.3.1 Arithmetic Operators
**Arithmetic operators** let us do math:

| Operator | Meaning            | Example |
| -------- | ------------------ | ------- |
| `=`      | Assignmnent        | `x=1`   |
| `+`      | Addition           | `x + y` |
| `-`      | Subtraction        | `x - y` |
| `*`      | Multiplication     | `x * y` |
| `/`      | Division           | `x / y` |
| `%`      | Modulo (remainder) | `x % y` |

### 0.3.2 Unary operators
**Unary operators** only take one operand:
| Operator | Name | Example |
| -------- | ---- | ------- |
| `+` | Unary plus  | `+a` |
| `-` | Unary minus | `-a` |
| `++` | Increment | `a++` or `++a` |
| `--` | Decrement | `a--` or `--a` |

Example:
```c
int a = 2;
int b;
b = a++ /* b is 2, a is 3 */
b = ++a /* b is 4, a is 4 */
b = a-- /* b is 4, a is 3 */
b = --a /* b is 2, a is 2 */
```
### 0.3.3 Comparison Operators
**Comparison Operators** 
| Operator | Name                    | Example  |
| :------: | ----------------------- | -------- |
|   `==`   | Equal operator          | `a == b` |
|   `!=`   | Not equal operator      | `a != b` |
|    `>`   | Bigger than             | `a > b`  |
|    `<`   | Less than               | `a < b`  |
|   `>=`   | Bigger than or equal to | `a >= b` |
|   `<=`   | Less than or equal to   | `a <= b` |



### 0.3.4 Logic Operators
**Logical operators:**  work with boolean values.
| Operator | Name | example |
|---|---|---|
| `!` | NOT | `!a` |
| `&` |AND |`a && b` |
| `\|` | OR | `a \|\| b` |

### 0.3.5 Assignment Operators
**Assignment Operators** perform arithmetic transformation and and assignment   
| Operator | Name                      | Example  |
| :------: | ------------------------- | -------- |
|   `+=`   | Addition assignment       | `a += b` |
|   `-=`   | Subtraction assignment    | `a -= b` |
|   `*=`   | Multiplication assignment | `a *= b` |
|   `/=`   | Division assignment       | `a /= b` |
|   `%=`   | Modulo assignment         | `a %= b` |

### 0.3.6 Integer Division

If `x` and `y` are **integer-like types**, `/` **truncates the fractional part**.

```c
printf("%d\n", 50 / 20);  // 2
printf("%d\n", 50 % 20);  // 10
```

* `50 / 20` → `2`, not `2.5`
* `50 % 20` → `10` (remainder)
* `%` only works on **integral types**; not `float`/`double`.

### 0.3.7 Division with `double`

If you want to preserve decimal values, make sure **at least one operand is `double`/`float`**:

```c
int x = 50;

x / 20       // 2
x / 20.0     // 2.5
50.0 / 20.0  // 2.5
(double)x / 20  // 2.5
```

You can explicitly convert a value using a **cast**:

```c
(double)x
```

### 0.3.8 Operator Precedence

* `*`, `/`, `%` have **higher priority** than `+` and `-`
* `()` has the **highest priority**
* Similar to the normal order of operations in mathematics.

```c
x + 3 / x * (3 + x)
```

is evaluated according to these precedence rules.

---

> **Important:** `=` means **assignment**, not mathematical equality.

```c
int x = 5;
x = x + 2;  // x is now 7
x += 2;     // x is now 9
```

Assignment **changes the state of the program** by changing the value stored in a variable.


## 0.4 Ternary Operators

The **ternary operator** provides a compact way to choose between two expressions based on a condition.

```c
<expression1> ? <expression2> : <expression3>;
```

In English:

> If `<expression1>` is true, evaluate `<expression2>`; otherwise, evaluate `<expression3>`.

Example:

```c
double product_cost = 888;

double discount_amt = (product_cost >= 670) ? 2 : 0;
```

Since `product_cost` is `888`:

```text
888 >= 670 → true
```

Therefore:

```text
discount_amt = 2
```

If `product_cost` were less than `670`:

```text
discount_amt = 0
```

### Common condition tests

| Operator | Meaning               |
| -------- | --------------------- |
| `>`      | More than             |
| `>=`     | More than or equal to |
| `<`      | Less than             |
| `<=`     | Less than or equal to |
| `==`     | Equal to              |
| `!=`     | Not equal to          |

Another example:

```c
(product_cost >= 670)
    ? printf("You've reached min-spend")
    : printf("Spend another %f cents\n", 670 - product_cost);
```

The ternary operator is useful for **simple conditions** where there are two possible outcomes.

## 0.5 Undefined Behaviour

**Undefined Behaviour (UB)** is a major recurring aspect of C.

C is defined by a document called the **C Standard**. CS1010 uses the **C23 standard**.

The standard specifies what should happen for valid C code. However, for some erroneous code, the standard **imposes no requirements**.

If a program contains **undefined behaviour**:

> The program is allowed to do anything.

It might:

* produce an unexpected result
* crash
* appear to work
* behave differently on another compiler/system
* do something else entirely

**There are no guarantees.**

### Example: Division by zero

```c
#include <stdio.h>

int main() {
    printf("%d\n", 5);
    printf("%d\n", 1 / 0);
    return 0;
}
```

The expression:

```c
1 / 0
```

has **undefined behaviour**.

Do **not** assume that it will always produce a particular result.

### Integer Overflow

Overflow occurs when a value exceeds the range that its type can represent.

Assuming `int` is 4 bytes (32 bits):

**Unsigned integer overflow is well-defined:**

```c
unsigned int c = 4294967295;
c = c + 1;
```

The value **wraps around**:

```text
c = 0
```

**Signed integer overflow is undefined behaviour:**

```c
int c = 2147483647;
c = c + 1;  // Undefined Behaviour!
```

So:

| Situation                 | Behaviour                  |
| ------------------------- | -------------------------- |
| Unsigned integer overflow | Well-defined; wraps around |
| Signed integer overflow   | **Undefined Behaviour**    |

### Key takeaway

**UB = the C Standard gives no requirements for what happens.**

Therefore, **never rely on what seems to happen when testing UB**. A program may behave differently depending on the compiler, optimisation, machine, or other circumstances.

> **UB is an unavoidable part of C**, so learning to recognise and avoid it is important.

**Compiler Warnings**

The compiler can warn you about **some** problematic cases.

```text
Listen to what your compiler says!
```

Compiler warnings are useful for catching potential problems before they become bugs.

## 0.X Lab

**Goal:** Practice working with variables, format specifiers, and the ternary operator.

**Exercise 1 — Temperature conversion**

Write a program that stores a temperature in Celsius as a `double`, converts it to Fahrenheit, and prints both values to 2 decimal places.

```c
#include <stdio.h>

int main(void) {
    double celsius = 30.0;
    double fahrenheit = celsius * 9.0 / 5.0 + 32;
    printf("%.2f C = %.2f F\n", celsius, fahrenheit);
    return 0;
}
```

**Exercise 2 — Even or odd, with a ternary**

Read an `int` and use the ternary operator (not `if`) to print whether it is even or odd.

```c
#include <stdio.h>

int main(void) {
    int n = 7;
    printf("%s\n", (n % 2 == 0) ? "even" : "odd");
    return 0;
}
```

**Things to watch out for**
- Integer division silently truncates — cast to `double` if you need a fractional result (see [0.3.7](#037-division-with-double)).
- `%` only works on integer types.
- Always double check your format specifier matches the variable's type (e.g. `%f` for `double`/`float`, `%d` for `int`) — mismatching them is undefined behaviour (see [0.5](#05-undefined-behaviour)).

# L1: Conditionals and Functions

## 1.1 Abstraction I: Functions

*Function*
: is a named, reusable block of code that performs a specific task. It takes zero or more **arguments** as input, and can **return** a single value as output.

**Why functions?**
- **Abstraction** — the caller only needs to know *what* a function does (its interface), not *how* it does it (its implementation).
- **Reuse** — write the logic once, call it many times.
- **Readability** — breaking a program into small, well-named functions makes it easier to follow.

**Anatomy of a function**

```c
int add(int a, int b) {
    int sum = a + b;
    return sum;
}
```
- `int` (leftmost) is the **return type** — the type of value the function sends back.
- `add` is the function's **name**.
- `(int a, int b)` are the **parameters** — the inputs the function expects, along with their types.
- `return sum;` sends the value of `sum` back to whoever called the function. A function with return type `void` does not return a value, and can use a bare `return;` (or nothing) to end early.

**Calling a function**
```c
int result = add(3, 4); // result is 7
```

**Function prototypes**

If a function is defined *after* `main`, or in another file, the compiler needs to know its signature before it's used. A **prototype** declares the signature without the body:
```c
int add(int a, int b); // prototype

int main(void) {
    int result = add(3, 4);
    return 0;
}

int add(int a, int b) { // definition
    return a + b;
}
```

## 1.2 Conditional Statements
### 1.2.1 If/else constructs

The `if` statement runs a block of code only when a condition is true.

```c
if (condition) {
    // runs when condition is true
}
```

Add an `else` to handle the opposite case:
```c
if (condition) {
    // condition is true
} else {
    // condition is false
}
```

Chain multiple conditions with `else if`:
```c
if (score >= 90) {
    printf("A\n");
} else if (score >= 75) {
    printf("B\n");
} else if (score >= 50) {
    printf("C\n");
} else {
    printf("F\n");
}
```
Only the **first** branch whose condition is true runs; the rest are skipped.

**Always use braces**

As seen in the L2 lab below, omitting `{ }` means only the *single statement* immediately after the `if`/`else` belongs to it — everything after that runs unconditionally regardless of the condition. Always wrap the body in `{ }`, even for one-line bodies, to avoid this class of bug.

### 1.2.2 Comparison and logical operators

Recall the comparison operators (`==`, `!=`, `<`, `>`, `<=`, `>=`) and logical operators (`&&`, `||`, `!`) from [0.3](#03-arithmetic-and-assignment-operators). Inside an `if`, these are combined to build more complex conditions.

**Truth tables**

| `a` | `b` | `a && b` | `a \|\| b` |
| --- | --- | -------- | -------- |
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 |

| `a` | `!a` |
| --- | ---- |
| 0 | 1 |
| 1 | 0 |

**Short-circuit evaluation**

`&&` and `||` evaluate left to right and stop early once the result is already decided:
- `a && b` — if `a` is false, `b` is **never evaluated** (the whole expression is already false).
- `a || b` — if `a` is true, `b` is **never evaluated** (the whole expression is already true).

This matters when the right-hand side has side effects (e.g. a function call that prints something), as seen in the `foo() && bar()` example in the L2 lab below.

### 1.2.3 Boolean operators

C did not have a built-in boolean type until relatively recently. `<stdbool.h>` provides one:

```c
#include <stdbool.h>

bool is_valid = true;
```

Under the hood:
- `bool` is really a small integer type; `true` is `1` and `false` is `0`.
- Any non-zero value is treated as "true" in a condition; only `0` is "false".

```c
int x = 5;
if (x) {        // true, since x != 0
    printf("x is truthy\n");
}
```

**Returning a `bool` from a function**

```c
#include <stdbool.h>

bool is_even(int n) {
    return n % 2 == 0;
}
```
This is the pattern used by `foo()` and `bar()` in the L2 lab below — functions that return `bool` and are combined with `&&`/`||` inside an `if`.

## 1.X Lab

**Goal:** Practice writing your own functions that use conditionals.

**Exercise — Grade classifier**

Write a function `char grade(int score)` that returns `'A'`, `'B'`, `'C'`, or `'F'` based on the boundaries used in [1.2.1](#121-ifelse-constructs), then call it from `main` and print the result.

```c
#include <stdio.h>

char grade(int score) {
    if (score >= 90) {
        return 'A';
    } else if (score >= 75) {
        return 'B';
    } else if (score >= 50) {
        return 'C';
    } else {
        return 'F';
    }
}

int main(void) {
    int score = 82;
    printf("Grade: %c\n", grade(score));
    return 0;
}
```

**Stretch goal**

Write `bool is_leap_year(int year)` using the rule: divisible by 4, except centuries, unless also divisible by 400. Combine `&&`, `||`, and `!` from [1.2.2](#122-comparison-and-logical-operators).

# L2: Abstractions, Structs, and the Stack
##  2.1 Abstraction II: Functions 
### 2.1.1 Abstraction of Behavior: Functions

Section [1.1](#11-abstraction-i-functions) introduced functions as reusable blocks of code. Here we look at *why* wrapping behaviour in a function is a form of **abstraction**.

When we call a function, we only need to know:
1. Its **name**
2. Its **parameters** (types and meaning)
3. Its **return type**

We don't need to know *how* it's implemented internally — that's hidden inside the function body. This is exactly what happens with `read_point()` and `print_movement()` in the lab below: `main` doesn't need to know how a point is read or how movement is computed, only that these functions exist and what they do.

**Pass-by-value**

In C, arguments are passed **by value** — the function receives a *copy* of the argument. Modifying a parameter inside a function does not affect the caller's variable.
```c
void increment(int x) {
    x = x + 1; // only changes the local copy
}

int main(void) {
    int n = 5;
    increment(n);
    printf("%d\n", n); // still 5
}
```

### 2.1.2 Abstraction of Data: Structs

Just as functions abstract *behaviour*, **structs** abstract *data* — they let us group related variables into a single named type.

```c
typedef struct {
    int x;
    int y;
} Point;
```
- `struct { ... }` defines a new structure with the listed fields (**members**).
- `typedef ... Point;` gives the struct the alias `Point`, so we can write `Point p;` instead of `struct { ... } p;` every time.

**Creating and accessing a struct**
```c
Point p;
p.x = 3;
p.y = 4;
printf("(%d, %d)\n", p.x, p.y); // (3, 4)
```
The `.` (dot) operator accesses a member of a struct.

**Why this is abstraction**

Without a struct, a point would be two separate, unrelated `int` variables (`px`, `py`), and a function relating two points would need four separate parameters. With `Point`, related data travels together as one value — as seen in the lab below, where `print_movement(Point start, Point end)` takes just two arguments instead of four.

## 2.2 The Stack and Block Scoping
### 2.2.1 Stack Frames

Every time a function is called, the program sets aside a small block of memory called a **stack frame** to hold that call's local variables, parameters, and return address.

- When a function is **called**, a new frame is **pushed** onto the **call stack**.
- When the function **returns**, its frame is **popped** off the stack, and its memory is reclaimed.
- Each call gets its **own** frame — calling the same function twice (e.g. `read_point()` for `p` then for `q` in the lab below) creates two separate frames, each with its own copy of `pt`.

```text
call main()
  -> call read_point()    [frame for read_point pushed]
  <- return                [frame for read_point popped]
  -> call read_point()    [a *new* frame pushed]
  <- return                [popped again]
  -> call print_movement() [frame pushed]
  <- return                [popped]
```
This is also why a function cannot "see" another function's local variables — they live in different frames.

### 2.2.2 Local variables

A **local variable** is declared inside a function or block, and only exists — is only *in scope* — within that block.

```c
void foo(void) {
    int a = 1; // local to foo
}

void bar(void) {
    int a = 2; // a different `a`, local to bar
}
```
`foo`'s `a` and `bar`'s `a` are unrelated; each lives in its own stack frame.

**Block scoping**

Any `{ }` introduces a new scope, not just function bodies — including `if`, `else`, and loop bodies:
```c
int main(void) {
    int x = 10;
    if (x > 5) {
        int y = 20;     // y only exists inside this block
        printf("%d\n", y);
    }
    // y is not visible here — out of scope
    return 0;
}
```

**Lifetime vs. scope**
- **Scope** — where in the code a variable's name is visible.
- **Lifetime** — how long the variable's memory actually exists (tied to its stack frame, from when the block is entered to when it's exited).

## 2.X Lab

**More If-Else, Abstraction, Structs**

Part 1a:

Does the code below compile? What is its output?
```c
#include <stdbool.h>
#include <stdio.h>
 
bool foo(){
	printf("foo called returning true\n");
	return true;
}
 
bool bar(){
	printf("bar called returning false\n");
	return false;
}
 
int main(){
	if(foo() && bar()){
		printf("line A reached\n");
	}
 
	printf("BOOP\n");
 
	if(foo() || bar()){
		printf("line B reached\n");
	}
}
```

Output:
**Only one line output **
- If you omit the curly braces `{    }` in your if statement, only the line **below** the `if` statement is used as its output.
- 


Consider the following code:
```C
#include "input.h"
#include <stdbool.h>
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Point;

int main() {
    Point p;
    p.x = read_int();
    p.y = read_int();

    Point q;
    q.x = read_int();
    q.y = read_int();

    int dx = q.x - p.x;
    int dy = q.y - p.y;

    bool moving_right = dx > 0;
    bool moving_up = dy > 0;
    bool on_same_x = dx == 0;
    bool on_same_y = dy == 0;

    if (on_same_x && on_same_y) {
        printf("same point\n");
    } else if (on_same_x) {
        printf("vertical movement\n");
    } else if (on_same_y) {
        printf("horizontal movement\n");
    } else if (moving_right && moving_up) {
        printf("northeast\n");
    } else if (!moving_right && moving_up) {
        printf("northwest\n");
    } else if (moving_right && !moving_up) {
        printf("southeast\n");
    } else {
        printf("southwest\n");
    }
    return 0;
}
```

We can simplify this to:

```c
#include "input.h"
#include <stdbool.h>
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Point;

Point read_point() {
    Point pt;
    pt.x = read_int();
    pt.y = read_int();
    return pt;
}

void print_movement(Point start, Point end) {
    int dx = end.x - start.x;
    int dy = end.y - start.y;

    bool moving_right = dx > 0;
    bool moving_up = dy > 0;
    bool on_same_x = dx == 0;
    bool on_same_y = dy == 0;

    if (on_same_x && on_same_y) {
        printf("same point\n");
    } else if (on_same_x) {
        printf("vertical movement\n");
    } else if (on_same_y) {
        printf("horizontal movement\n");
    } else if (moving_right && moving_up) {
        printf("northeast\n");
    } else if (!moving_right && moving_up) {
        printf("northwest\n");
    } else if (moving_right && !moving_up) {
        printf("southeast\n");
    } else {
        printf("southwest\n");
    }
}

int main() {
    Point p = read_point();
    Point q = read_point();
    print_movement(p, q);
    return 0;
}
```

# L3: Fixed Size arrays and Recursion
## 3.1 Arrays
### 3.1.1 Array Declaration

Let's say we want to declare an array that stores 5 elements of type `double` that we want to call "costs".

An **array** is declared as such:
`<type> <array name>[<no. of elements>]`

```c
double costs[5];
```

> **Important:** Arrays have a fixed type. You cannot add multiple different types to an array unlike Python.

Arrays are stored on the stack. 
```stack
main

costs = {?,?,?,?,?}
```
An array will have all of its elements stored contiguously to each other in memory. * This has implications for both performance and security in the far future.

```c
double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
        // initializes the array with 5 values
```
It is stored in the stack as such:
```
stack:
|8.88|10.22|9.88|22.22|44.44|
```
### 3.1.2 Initializing elements
However, what if we initialize only 3 elements out of 5?

```c
double costs[5]= {8.88,10.22,9.88};
// the remaining elements will be initialized to 0.0 by default.


double zeroarray[5]={0};
//^^this is a very good way to initialize an entire array to 0!
```

What if we initalize more than 5 elements?
```c
double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44, 1.0};
```

If we have more values than the specified size, what happens is up to the compiler (technically not undefined behavior) [we don’t recommend doing this, there’s no good reason to at this stage]


What if we initialize it over 2 lines?
```c
double costs[5];
costs = {8.88, 10.22, 9.88, 22.22, 44.44, 1.0};
```
> This does **NOT** work and throws a `compile error`. Unlike scalar variables, arrays cannot be assigned new values as a whole.


### 3.1.3 Accessing an Array (writing)
We use the index.
```c
double costs[5];

costs[0] = 8.88;
// | 8.88 | ? | ? | ? | ? |

costs[4] = 44.44;
// | 8.88 | ? | ? | ? | 44.44 |
```

### 3.1.4 Copying Semantics
```c
int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    double costs_2[] = costs; // error!
}
```

> This does **NOT** work and will throw a *compile error*! `error: array initalizer must be an initializer list.`

Arrays (unlike numerical types and structs) as a whole are **not copyable** via assignment operators.

### 3.1.5 Arrays as arguments to functions
```c
#include <stdio.h>
#include <stddef.h>

void print_doublearr_index(double arr[], size_t index) {
    printf("%f\n", arr[index]);
}

int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    print_doublearr_index(costs, 3);
}
```

`size_t`: unsigned type (typically `unsigned long`)
- Guaranteed to be large enough to index any array
- Intent is clear: use by default for array indices, unless we need negative values
- `size_t` is defined in `<stddef.h>`

Array indices can technically be any integral type (`char`, `int`, `long` ...)

### 3.1.6 Length of arrays
```c
void print_last_element (double arr[]) {
    printf("%f\n", arr[?])
}

int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    print_last_element(costs);
}
```
In **C**, we do **NOT** have `length/len` operators to measure the length of an array.

Instead, we use `size_t` for now:
```c
void print_last_element(double arr[], size_t length) {
    printf("%f\n", arr[length - 1]);
}

int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    print_last_element(costs, 5);
}
```

### Setting Values inside Functinos

```c
int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    set_doublearr_index(costs, 3, 5.5);
    printf("%f\n", costs[3]);
}
void set_doublearr_index(double arr[], size_t index, double val) {
    arr[index] = val;
}
    //output is... 5.5.
```

This sets the index 3 (the 4th) element of costs to 5.5. But how is that possible? This is because arrays are pointers.
[](#)

### Returning from functions
For now, do not return arrays declared within functions.
```c
// DONT DO THIS
??? foo() {
    double costs[5] ={8.88, 10.22, 9.88, 22.22, 44.44, 1.0};
    return costs;
} // will return UB
```

## 3.2 Arrays and Structs
### Zeroing out

```c
#include <stdio.h>

typedef struct Position {
    int x;
    int y;
} Position;

int main(void){
    Position positions[2] = {0};
    printf("%d %d\n", positions[0].x, positions[0].y);
} // This will zero out all members of all structs.
```

### UB
```c
int main(void) {
    double costs[1] = {8.88};
    printf("%f\n", costs[1]);
}

// UB [1] 


int main(void) {
    double costs[1];
    printf("%f\n", costs[-1]);
}

// UB [2]

??? foo() {
    double costs[1] = {8.88};
    return costs;
}

// UB [3]

int main() {
    double costs[1];
    printf("%f\n", costs[0]);
}
```

### Variable-length arrays

Can we declare the size of an array as a variable? Yes.
```c
double costs[var];
```

> However, there are much better ways to do this (discussed later). We do not allow VLAs because of underlying issues. As a matter of fact, VLA was removed from Linux operating system.

## 3.3 Multidimensional Arrays
### 3.3.1 Array of arrays
```c
int main(void) {
    int a[2][3] = {{0,1,2},{3,4,5}};
    printf("%d\n", a[1][0]);
}
```

Then a is stored as:
$$a =
\left[\begin{matrix}
    0 & 1 & 2 \\ 3 & 4 & 5
\end{matrix}\right]$$

We are storing an array of arrays.

Example: tic-tac-toe
```c
int grid[3][3] = {{1,2,3},{4,5,6},{7,8,9}};
```
$$\text{grid} =
\left[\begin{matrix}
    1 & 2 &3 \\ 4 & 5 & 6 \\ 7&8&9
\end{matrix}\right]$$

Arrays can have more dimensions!

> Only the first dimension size can be omitted.

