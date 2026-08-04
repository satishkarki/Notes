# Function and Program Structure

Here I will introduce ideas like scope, separate compilation, and the preprocessor.

Basic Structure of function:
```c
return-type function-name(parameter declarations)
{
    declarations
    statements
}
```
## Functions returning non-integers
If a function is used before its definition or declaration appears, and nothing tells the compiler otherwise, C (in the old K&R style) assumed it returned `int`. If your function actually returns a `double`, that assumption silently produces garbage - the bit pattern of a `double` gets misinterpreted as an `int`.

Fix:
```c
#include <stdio.h>

double average(double a, double b);   // <-- prototype: promise of what's to come

int main(void)
{
    double result = average(4.0, 7.0);
    printf("Average: %.2f\n", result);
    return 0;
}

double average(double a, double b)    // <-- actual definition
{
    return (a + b) / 2;
}
```
## External Variables
```c
#include <stdio.h>

int counter = 0;   // external variable — declared outside any function

void increment(void)
{
    counter++;      // no need to pass counter in — it's visible here
}

void print_counter(void)
{
    printf("Counter is: %d\n", counter);
}

int main(void)
{
    increment();
    increment();
    increment();
    print_counter();   // prints "Counter is: 3"
    return 0;
}
```
Now lets look at another example here:
```c
int count = 10;   // external variable, count = 10, visible file-wide

void reset(void)
{
    int count = 0;   // LOCAL variable — shadows the external one!
    printf("Inside reset: count = %d\n", count);  // uses the LOCAL count
}

int main(void)
{
    reset();
    printf("Inside main: count = %d\n", count);   // uses the EXTERNAL count
    return 0;
}
```

**Shadowing**: Inside `reset()`, the line `int count = 0;` creates a brand-new local variable that happens to share the same name as the external one. C's scoping rule is: the innermost declaration wins. So inside `reset()`, every reference to count refers to the local `count = 0` - the external count is temporarily "shadowed" and completely inaccessible from within that function.

Once `reset()` returns, that local count is destroyed - it never touched the external count at all. So back in `main()`, count still refers to the external variable, untouched at 10.

## Scope Rules

**Automatic Variables**
```c
int main(void)
{
    int x = 5;         // automatic — scope: within main's braces only
    if (x > 0) {
        int y = 10;     // automatic — scope: within the if-block ONLY
        printf("%d\n", y);
    }
    // y is NOT visible here — it's out of scope
    return 0;
}
```
**External Variables**
```c
int main(void)
{
    // x is NOT visible here yet!
    return 0;
}

int x = 100;   // x's scope begins HERE, extends to end of file
```
**extern**
```c
/* helper.c */
int total = 0;

void add_to_total(int n)
{
    total += n;
}
```
```c
#include <stdio.h>

extern int total;              // declares the variable defined in helper.c
void add_to_total(int n);      // prototype for the function in helper.c

int main(void)
{
    add_to_total(5);
    add_to_total(10);
    printf("Total: %d\n", total);   // prints "Total: 15"
    return 0;
}
```
>Key Concept
* Block scope is strict in C — unlike Python, a variable declared inside an if or for block is genuinely invisible outside it. Braces wall things off.
* Top-to-bottom visibility — an external variable's scope starts at its declaration line, not automatically from the top of the file. Using it earlier fails to compile.
* extern solves the ordering/multi-file problem — it's a declaration (announces type, no storage allocated), not a definition (which actually allocates memory and happens exactly once). This lets you:

    * Use a variable in main() before its real definition appears later in the file.
    * Share a variable across multiple .c files — defined once in one file, declared extern wherever else it's needed.


* Shadowing — a local variable can share a name with an external one; inside that block, the local one wins and the external one is temporarily hidden.

## Header Files
A header file (.h) collects related declarations - extern variables, function prototypes, macros, type definitions - in one place. Any .c file that needs them just does `#include "yourheader.h"`, and the preprocessor literally pastes that file's contents in at that point, before real compilation even begins.

Python analogy: This is loosely like import mymodule - except C's `#include` is far more primitive. It's not a smart module system; it's literally a textual copy-paste performed by the preprocessor. There's no namespacing, no "module object" - just raw text substitution

```c
/* helper.h */
extern int total;              // declaration, not definition
void add_to_total(int n);      // prototype
```
```c
/* helper.c */
#include "helper.h"    // pulls in declarations for consistency-checking

int total = 0;         // the one true DEFINITION

void add_to_total(int n)
{
    total += n;
}
```
```c
/* main.c */
#include <stdio.h>
#include "helper.h"    // same declarations, now shared/reused

int main(void)
{
    add_to_total(5);
    add_to_total(10);
    printf("Total: %d\n", total);
    return 0;
}
```

## Static Variables

1. static on a variable inside a function - persistence across calls.
    ```c
    #include <stdio.h>

    void counter(void)
    {
        static int calls = 0;   // initialized ONCE, ever
        calls++;
        printf("Called %d times\n", calls);
    }

    int main(void)
    {
        counter();   // "Called 1 times"
        counter();   // "Called 2 times"
        counter();   // "Called 3 times"
        return 0;
    }
    ```
    Normally, automatic (local) variables are destroyed when the function returns and recreated fresh next time. `static` changes that: the variable is initialized once, and then retains its value between function calls - while still only being visible inside that function (scope unchanged).

2. static on an external variable or function - restricting visibility to one file.
    ```c
    /* helper.c */
    static int secret = 42;   // ONLY visible within helper.c

    static void internal_helper(void)   // ONLY callable within helper.c
    {
        // ...
    }
    ```
    Here `static` means something almost opposite: instead of persistence, it's about hiding something from other files. Normally, external variables/functions are visible to any file that `extern`-declares them. Marking one `static` at file scope makes it private to that `.c` file only — no other file can link to it, even with `extern`.

## Register Variables




