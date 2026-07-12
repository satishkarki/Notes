# Types, Operators, and Expressions

## Variable names
The conventions (not enforced, but expected)
* Underscore-leading names are conventionally avoided in your own code. Names starting with `_` are often used by library implementations for internal names (like `_iob` in old standard library headers).
* Lowercase for variables, and reserve all-uppercase for symbolic constants (things defined via #define)

```c
#define MAXLINE 1000
int lineCount;
```
## Data Type and Sizes

| Type | Meaning |
|------|---------|
| `char` | a single byte, holds one character in the local character set |
| `int` | an integer, typically reflects the "natural" size of integers on the host machine |
| `float` | single-precision floating point |
| `double` | double-precision floating point |

**Qualifiers**

You can modify int (and in older code, sometimes implicitly drop the word int itself) with:
```c
short int x;      // often written just "short x;"
long int count;   // often written just "long count;"
unsigned int u;
unsigned long bignum;
```
**Example**
```c
#include <stdio.h>

int main(void)
{
    printf("char: %zu bytes\n", sizeof(char));
    printf("short: %zu bytes\n", sizeof(short));
    printf("int: %zu bytes\n", sizeof(int));
    printf("long: %zu bytes\n", sizeof(long));
    printf("float: %zu bytes\n", sizeof(float));
    printf("double: %zu bytes\n", sizeof(double));
    return 0;
}
```
```bash
# Output
char: 1 bytes
short: 2 bytes
int: 4 bytes
long: 8 bytes
float: 4 bytes
double: 8 bytes
```
Note:
| Specifier | Expects |
|-----------|---------|
| `%d` | `int` |
| `%u` | `unsigned int` |
| `%ld` | `long` |
| `%lu` | `unsigned long` |
| `%zu` | `size_t` (unsigned) |

## Constants

Suffixes for type
```c
long int y = 123456789L;   // 'L' or 'l' suffix = long
unsigned int u = 42U;      // 'U' or 'u' suffix = unsigned
unsigned long ul = 42UL;   // both combined
```
Octal
```c
int x = 010;   // this is octal 10 = decimal 8, NOT ten!
```
Hexadecimal
```c
int x = 0x1A;   // hex 1A = decimal 26
```
Character Constant
```c
char c = 'A';   // 'A' is really just the integer 65 (in ASCII)
```
