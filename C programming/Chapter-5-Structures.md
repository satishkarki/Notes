# Structures

I am hoping the `struct` concept is easier to wrap my head around than `pointer`. Pointer gave me PTSD and I still have difficulty sleeping at night. The only good thing came out of pointer, not for me but for my wife - I'm now afraid to point my finger at my her mistakes. I now point to a pointer of her mistake. Got it? Let's dive into `struct`.

## The Core Idea
A structure is a collection of one or more variables, possibly of different types, grouped together under a single name for convenient handling.

```c
// Structure Declaration (the template)
struct point {
    int x;
    int y;
};
```
* This defines the shape of a structure but creates no variable and allocates no memory - like designing a blank form.
```c
// Structure Variable Declaration (instantiation)
struct point origin;
```
* `struct point` acts as a type name (like `int`). This line actually creates a variable and allocates memory for it - like photocopying the blank form.

```c
// The Dot(.) operator - accessing members
origin.x=10;
origin.y=20;
```
* Reaches into a struct variable to read/write a specific member.
```c
// Initialization at Declaration
struct point pt={10,20};
```
* Creates and fills in a struct in one step. Values are matched in order to the members as declared.

```c
// Nested Structures
struct rect {
    struct point pt1;   // upper-left
    struct point pt2;   // lower-right
};
```
* A struct can contain other structs as members - building complex shapes from simpler ones.
```c
// Chained Dot Access
screen.pt2.y = 100;
```
## Structures and Functions

