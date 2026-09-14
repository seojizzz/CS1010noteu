# CS1010 C Cheat Sheet
*Quick-reference snippets for the practical exam — separate from lecture notes.*

---

## 1. Remote Connection (SSH)

> _Add manually._

---

## 2. Tmux Commands

| Action | Command / Keys |
| --- | --- |
| New session | `tmux new -s <name>` |
| List sessions | `tmux ls` |
| Attach to session | `tmux attach -t <name>` |
| Detach | `Ctrl-b` then `d` |
| Kill session | `tmux kill-session -t <name>` |
| New window | `Ctrl-b` then `c` |
| Next / previous window | `Ctrl-b` then `n` / `p` |
| Rename window | `Ctrl-b` then `,` |
| Split pane horizontally | `Ctrl-b` then `"` |
| Split pane vertically | `Ctrl-b` then `%` |
| Move between panes | `Ctrl-b` then arrow key |
| Kill current pane | `Ctrl-b` then `x` |
| Scroll mode (to view history) | `Ctrl-b` then `[` (press `q` to exit) |

---

## 3. Format Specifiers

| Specifier | Type | Notes |
| --- | --- | --- |
| `%d` / `%i` | `int` | signed decimal |
| `%u` | `unsigned int` | |
| `%ld` | `long` | |
| `%lu` | `unsigned long` | |
| `%zu` | `size_t` | use for array lengths / indices |
| `%f` | `float`/`double` | default 6 d.p. |
| `%.2f` | `float`/`double` | 2 d.p. — set precision with `%.Nf` |
| `%e` | `double` | scientific notation |
| `%c` | `char` | single character |
| `%s` | `char[]` / string | |
| `%x` / `%X` | unsigned hex | lower / upper case |
| `%o` | unsigned octal | |
| `%p` | pointer | |
| `%%` | literal `%` | |

**Gotchas**
- Mismatched specifier ↔ variable type = **undefined behaviour**, not a compile error.
- `%d` on a `double` does **not** convert — it misreads the bytes. Cast or use `%f`.
- Always use `%zu` for `size_t`, never `%d`.

---

## 4. Mini ASCII Tables *(optional)*

| Range | Dec | Notes |
| --- | --- | --- |
| `'0'`–`'9'` | 48–57 | digit char → int: `c - '0'` |
| `'A'`–`'Z'` | 65–90 | |
| `'a'`–`'z'` | 97–122 | uppercase → lowercase: `c + 32` |
| space | 32 | |
| newline `\n` | 10 | |
| tab `\t` | 9 | |
| NUL `\0` | 0 | string terminator |

---

## 5. Essential Terminal Commands

| Command | Purpose |
| --- | --- |
| `pwd` | print working directory |
| `ls` / `ls -la` | list files (incl. hidden + details) |
| `cd <dir>` / `cd ..` / `cd ~` | change directory |
| `mkdir <dir>` | make directory |
| `touch <file>` | create empty file |
| `cp <src> <dst>` | copy file |
| `cp -r <src> <dst>` | copy directory |
| `mv <src> <dst>` | move / rename |
| `rm <file>` | remove file |
| `rm -r <dir>` | remove directory recursively |
| `cat <file>` | print file contents |
| `less <file>` | scroll through file (`q` to quit) |
| `head -n N <file>` / `tail -n N <file>` | first / last N lines |
| `man <cmd>` | manual page |
| `chmod +x <file>` | make file executable |
| `grep "pattern" <file>` | search text in file |
| `find . -name "*.c"` | find files by pattern |
| `diff <f1> <f2>` | compare two files |
| `wc -l <file>` | count lines |
| `clang -o out out.c` | compile |
| `clang -Wall -Wextra -o out out.c` | compile with warnings on |
| `./out` | run compiled program |
| `make` | build via Makefile |
| `valgrind ./out` | check memory errors/leaks |

---

## 6. C Standard Libraries

| Header | Common functions |
| --- | --- |
| `<stdio.h>` | `printf`, `scanf`, `fopen`, `fclose`, `fgets`, `fprintf`, `fscanf` |
| `<stdlib.h>` | `malloc`, `calloc`, `realloc`, `free`, `exit`, `atoi`, `atof`, `rand`, `srand` |
| `<string.h>` | `strlen`, `strcpy`, `strncpy`, `strcat`, `strcmp`, `strncmp`, `strchr`, `memcpy`, `memset`, `memcmp` |
| `<math.h>` | `sqrt`, `pow`, `fabs`, `floor`, `ceil`, `round` |
| `<stdbool.h>` | `bool`, `true`, `false` |
| `<stddef.h>` | `size_t`, `NULL` |
| `<ctype.h>` | `isalpha`, `isdigit`, `isspace`, `isupper`, `islower`, `toupper`, `tolower` |
| `<limits.h>` | `INT_MAX`, `INT_MIN`, `UINT_MAX`, `CHAR_MAX` |
| `<float.h>` | `DBL_MAX`, `FLT_MAX` |
| `<assert.h>` | `assert(condition)` — aborts if false |

---

## 7. Structs

**Declare with `typedef`:**
```c
typedef struct {
    int x;
    int y;
} Point;
```

**Create, set, access (dot operator):**
```c
Point p;
p.x = 3;
p.y = 4;
printf("(%d, %d)\n", p.x, p.y);
```

**Struct with an array member:**
```c
typedef struct {
    char name[20];
    int score;
} Student;

Student s = {"Ada", 95};
printf("%s: %d\n", s.name, s.score);
```

**Struct pointer (arrow operator `->`):**
```c
void move_point(Point *p, int dx, int dy) {
    p->x += dx;   // shorthand for (*p).x += dx;
    p->y += dy;
}

Point p = {0, 0};
move_point(&p, 5, 5);
```

**Zeroing out a struct / array of structs:**
```c
Point p = {0};              // all members zeroed
Point pts[3] = {0};         // all structs in array zeroed
```

---

## 8. Arrays

**Declaration:**
```c
double costs[5];                             // uninitialized
double costs[5] = {8.88, 10.22, 9.88};       // rest default to 0.0
double zeros[5] = {0};                       // whole array zeroed
```

> ⚠️ **Never declare a variable-length array (VLA):**
> ```c
> int n = get_size();
> double arr[n];   // DON'T — size must be a compile-time constant
> ```
> Use a fixed constant size, or `malloc` on the heap instead.

**Passing to functions (arrays decay to pointers — always pass length too):**
```c
void print_arr(double arr[], size_t len) {
    for (size_t i = 0; i < len; i++) {
        printf("%f\n", arr[i]);
    }
}
```

**Modifying inside a function works (no need to return):**
```c
void set_index(double arr[], size_t index, double val) {
    arr[index] = val;   // mutates caller's array directly
}
```

**2D arrays:**
```c
int grid[3][3] = {{1,2,3}, {4,5,6}, {7,8,9}};
printf("%d\n", grid[1][0]);   // 4
```
Only the **first** dimension's size may be omitted in an initializer.

**Don't do this:**
```c
double a[5] = {1,2,3,4,5};
double b[5] = a;        // error — arrays aren't copyable via `=`
b = a;                   // error — same reason

??? foo(void) {
    double local[5] = {0};
    return local;        // UB — never return a local array
}
```

---

## 9. Vim Commands

**Modes:** `Esc` → Normal | `i` → Insert | `v` → Visual

**Normal mode — movement**
| Keys | Action |
| --- | --- |
| `h j k l` | left / down / up / right |
| `w` / `b` | next / previous word |
| `0` / `$` | start / end of line |
| `gg` / `G` | top / bottom of file |
| `:N` | go to line N |

**Normal mode — editing**
| Keys | Action |
| --- | --- |
| `x` | delete character |
| `dd` | delete (cut) line |
| `dw` | delete word |
| `yy` | yank (copy) line |
| `p` / `P` | paste after / before |
| `u` | undo |
| `Ctrl-r` | redo |
| `/pattern` then `n`/`N` | search forward, next/prev match |

**Insert mode — entry points (from Normal)**
| Keys | Action |
| --- | --- |
| `i` / `a` | insert before / after cursor |
| `I` / `A` | insert at start / end of line |
| `o` / `O` | open new line below / above |

**Visual mode**
| Keys | Action |
| --- | --- |
| `v` | character-wise select |
| `V` | line-wise select |
| `Ctrl-v` | block (column) select |
| `d` / `y` / `c` | delete / yank / change selection |

**Save & quit**
| Keys | Action |
| --- | --- |
| `:w` | save |
| `:q` | quit |
| `:wq` or `ZZ` | save and quit |
| `:q!` | quit without saving |

---

## 10. Recursion — Void Functions Only

> Assumption: "void loops" = recursive functions with **`void` return type** (no return value) — output happens via `printf` or by mutating an array/pointer argument, not via a returned value. Base case always ends with a bare `return;`.

### Template A — Incrementing recursion
*Walks up from a start value toward a limit.*
```c
void count_up(int current, int limit) {
    if (current > limit) {
        return;                      // base case
    }
    printf("%d\n", current);
    count_up(current + 1, limit);    // move toward base case: +1
}
// call: count_up(1, 10);
```

### Template B — Decrementing recursion
*Walks down from a start value toward zero (or processes an array back-to-front).*
```c
void count_down(int current) {
    if (current < 0) {
        return;                      // base case
    }
    printf("%d\n", current);
    count_down(current - 1);         // move toward base case: -1
}
// call: count_down(10);

void print_arr_reverse(int arr[], size_t len) {
    if (len == 0) {
        return;                      // base case
    }
    printf("%d\n", arr[len - 1]);
    print_arr_reverse(arr, len - 1); // shrink toward base case
}
```

### Template C — Interval recursion
*Two bounds close in on each other — classic for in-place array work.*
```c
void interval_helper(int arr[], size_t start, size_t end) {
    if (start >= end) {
        return;                      // base case: bounds met/crossed
    }
    // do work with arr[start] and/or arr[end] here
    interval_helper(arr, start + 1, end - 1);   // narrow the interval
}

void interval_wrapper(int arr[], size_t len) {
    if (len == 0) {
        return;
    }
    interval_helper(arr, 0, len - 1);   // set up initial bounds
}
// call: interval_wrapper(arr, len);
```

**Pattern to remember:** when a function needs extra bookkeeping parameters (an index, a pair of bounds) that the caller shouldn't have to supply, write a small `void` **wrapper** that takes just `(arr, len)` and calls a `void` **helper** with the real starting parameters.