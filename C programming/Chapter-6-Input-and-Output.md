## 1. Standard Input and Output

- **Streams**: C treats I/O as streams of bytes. Keyboard, file, or another program's output all look the same to your code.
- **Three default streams**: `stdin` (keyboard), `stdout` (screen), `stderr` (screen, for errors).
- **`getchar()` / `putchar(c)`**: read/write one character on `stdin`/`stdout`.
- **`int c`, not `char c`**: `getchar()` returns an `int` so it can hold `EOF` (typically -1) alongside every valid character value. With `char c`, `EOF` detection can fail (a `char` may be unsigned, or -1 may collide with a real character).
- **Redirection**: the shell rewires streams (`prog < infile > outfile`) without any change to your C code.
- **Macros**: `getchar`/`putchar` are often macros (`getc(stdin)`, `putc(c, stdout)`), which avoids function-call overhead per character. Avoid passing arguments with side effects (like `i++`) to anything that might be a macro.

## 2. Formatted Output -Printf
If you want to dive deep into it, there is more about formatted output in Appendix B1.2 of the book. For now the below information will suffice.
```c
int printf(char *format, arg1, arg2, ...);
```
The format string contains two kinds of things:
- Ordinary characters, copied straight to the output.
- Conversion specifications, each starting with `%`, which consume the next argument and format it.

What does it mean by two kinds of strings?
Example: 
```c
int age = 30;
printf("I am %d years old\n", age);
```
`I am` is copied straight out- ordinary character. At `%d`, it detects the conversion specs and consumes `age` and prints `30`.

### 2.1 Anatomy of conversion spec

```bash
%  [-]  [width]  [.precision]  conversion-char
```
The flags in the bracket are optional.

- `-` : left-justify (default is right-justify)
- `width` : minimum field width (pads with spaces if shorter)
- `.precision` : for strings, the max characters printed; for floats, digits after the decimal point; for integers, the minimum digits
- `conversion-char` : what kind of value it is

```c
/* Example of width and precision*/

printf(":%s:",        "hello, world");  // :hello, world:
printf(":%10s:",      "hello, world");  // :hello, world:      (already wider than 10)
printf(":%.10s:",     "hello, world");  // :hello, wor:        (truncated to 10 chars)
printf(":%-10s:",     "hello, world");  // :hello, world:
printf(":%.15s:",     "hello, world");  // :hello, world:      (max 15, only 12 exist)
printf(":%-15s:",     "hello, world");  // :hello, world   :   (left-justified, padded to 15)
printf(":%15.10s:",   "hello, world");  // :     hello, wor:   (truncate to 10, pad to 15)
printf(":%-15.10s:",  "hello, world");  // :hello, wor     :
```
### 2.2 The `*` shortcut
```c
char *s = "computer";
int max = 3;

printf("%.*s\n", max, s);   // com
max = 5;
printf("%.*s\n", max, s);   // compu
```
The `*` in `%.*s` means "don't use a number here, take it from the next argument." So `printf` reads two arguments for this one spec:

- First, an `int` for the precision (`max`)
- Then, the string (`s`)

### 2.3 Conversion Character

| Char | Argument type / output |
|---|---|
| `d`, `i` | `int`, decimal |
| `o` | unsigned octal (no leading `0`) |
| `x`, `X` | unsigned hex (no leading `0x`), lowercase/uppercase digits |
| `u` | unsigned decimal |
| `c` | single character |
| `s` | string (`char *`) |
| `f` | `double`, like `123.456000` (default precision 6) |
| `e`, `E` | `double`, like `1.234560e+02` |
| `g`, `G` | `double`, uses `%e` or `%f`, whichever is shorter |
| `p` | pointer (implementation-defined format) |
| `%` | a literal `%` sign |


```c
#include <stdio.h>

int main(void)
{
    int n = 255;
    unsigned int big = 3000000000u;
    char ch = 'A';
    char *word = "hello";
    double x = 123.456;

    printf("d:  %d\n", n);             // 255
    printf("i:  %i\n", n);             // 255 (same as %d for output)
    printf("o:  %o\n", n);             // 377
    printf("x:  %x\n", n);             // ff
    printf("X:  %X\n", n);             // FF
    printf("u:  %u\n", big);           // 3000000000
    printf("c:  %c\n", ch);            // A
    printf("s:  %s\n", word);          // hello
    printf("f:  %f\n", x);             // 123.456000
    printf("e:  %e\n", x);             // 1.234560e+02
    printf("E:  %E\n", x);             // 1.234560E+02
    printf("g:  %g\n", x);             // 123.456
    printf("g:  %g\n", 0.00001234);    // 1.234e-05  (tiny, so %e style is shorter)
    printf("G:  %G\n", 0.00001234);    // 1.234E-05
    printf("p:  %p\n", (void *)&n);    // e.g. 0x7ffd5c3a1b4c (varies per run)
    printf("%%: 100%%\n");             // 100%

    return 0;
}
```
### 2.4 Warnings
Two warnings from the book:

1. Arguments must match the format.
    ```c
    printf("%d\n", 3.14);   // wrong: %d expects int, got double - undefined behavior
    printf("%d %d\n", 5);   // wrong: second %d has no argument
    ```
2. Never pass user text as the format string
    ```c
    printf(s);          // BAD: if s contains "%", printf treats it as a conversion spec
    printf("%s", s);    // GOOD: s is treated as plain data
    ```
