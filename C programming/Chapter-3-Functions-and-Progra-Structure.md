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

