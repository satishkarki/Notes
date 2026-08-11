# Pointers and Arrays

A pointer is just a variable whose value is the address of another variable.

Let's introduce two variables:

* `&` (address of): give me the address of this variable
* `*` (dereference, in a declaration or expression context): give me the value stored at this address

```c
int x=1;
int *ip; //ip is declared as pointer to int
ip=&x; //ip now holds the address of x
printf("%d\n", *ip); //deference, prints 1
```
> Note the dual role of `*` here — in the declaration `int *p;`, it means "p is a pointer to int." In the expression `*p`, it means "dereference p." Same symbol, different job depending on context.

Example:

```c
int y = 42;
int *p = &y;
*p=100;
printf("%d\n", y);

// Output
100 //Why?
```
Why? - That's the core insight of pointers: `*p = 100` doesn't change what `p` points to, it changes the value at that location. Since `p` points to `y`, you're editing `y` "through the back door."

## Pointers and Function Arguments

```c
#include <stdio.h>

void swap(int *pa, int *pb)
{
    int temp;
    temp=*pa;
    *pa=*pb;
    *pb=temp;
}
int main()
{
    int a=5,b=10;
    printf("The value of a is %d and b is %d before the swap\n", a,b);
    swap(&a,&b);
    printf("The value of a is %d and b is %d after the swap\n", a,b);
    return 0;
}
```
## Pointers and Arrays
```c
int a[10];
int *pa;
pa=a; //equivalent to pa=&a[0];
```
> Core Fact: The name of an array, when used in an expression, "decays" into a pointer to its first element.

So that means, these two statements are equal:
```c
a[i]     ==  *(a + i)
pa[i]    ==  *(pa + i)
```
Now lets look at this example and see how we can use pointers instead:
```c
//Regular way
int a[5] = {10, 20, 30, 40, 50};
int sum = 0;
int i;
for (i = 0; i < 5; i++)
    sum += a[i];
```
```c
//Using the pointer
int a[5] = {10, 20, 30, 40, 50};
int sum = 0;
int *p;
for (p = a; p < a + 5; p++)
    sum += *p;
```
One Important difference
```c
int a[5] = {10, 20, 30, 40, 50};
int *pa = a;

pa++;      // legal - pa is a variable, can be reassigned
a++;       // ILLEGAL - a is not a variable, it's a fixed label for the array's address
```
## Address Arithmetic

> Important concept : `i * sizeof(the pointed-to type)`

Suppose int is 4 bytes on your system, and a starts at memory address 1000.
```c
int a[5] = {10, 20, 30, 40, 50};
```
Memory layout will look like this:
```bash
address:  1000   1004   1008   1012   1016
value:    a[0]   a[1]   a[2]   a[3]   a[4]
          10     20     30     40     50
```
Each `int` takes 4 bytes, so consecutive elements are 4 bytes apart, not 1 byte apart.

Now, `a + 2` doesn't mean "address 1002" (that would land you inside `a[0]`, garbage). It means:
```c
a + 2  =  1000 + (2 * sizeof(int))  =  1000 + 8  =  1008
```
...which correctly lands you at `a[2]`. The compiler knows `a` is `int *`, so it automatically multiplies your offset by `sizeof(int)` before adding it to the raw address.

> Legal Pointer Operations
1. Add or subtract an integer to/from a pointer: `p + n`, `p - n`
2. Subtract one pointer from another (only if both point into the same array): `p2 - p1`
3. Compare two pointers with `<`, `<=`, `>`, `>=`, `==`, `!=` (only meaningful if both point into the same array)

```c
int a[10];
int *p1 = &a[2];
int *p2 = &a[7];

int n = p2 - p1;   // n == 5
```
## Character Pointers and Functions


