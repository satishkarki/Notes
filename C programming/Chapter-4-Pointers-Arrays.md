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
