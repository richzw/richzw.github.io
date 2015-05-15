---
layout: post
title: C++ Jotting
---

- **Precompiled Header (PCH)**


> To reduce compilation time, some compiler allow head file to be precompiled into a form that is faster for compiler to process

**Forward Declaration** of one class instead of including the header file

- **How to get the length of one array as one parameter**

```cpp
template <typename T, unsigned int N>
unsigned int sizeofarray(T (&)[N])
{
    return N;
}

int A[5];
unsigned int size = sizeofarray(A);
```

- **Question**

```cpp
int i = 1;
void main()
{
    int i = i;
}
```

What is the value of i after assignment? 

**Complie Error**

`i` is still undefined in the local scope, although the question is at least slightly more interesting. The local `i` shadows the global one as soon as it's defined, so by the time the assignment happens the local definition already exists, and the right-hand side `i` refers to the `i` defined within main, not the global one. If it didn't removing the global `int i = 1;` would cause a compile error, as `int i = i;` would refer to an i that doesn't exist yet

> The point of declaration for a name is immediately after its complete declarator (clause 8) and before its initializer (if any), except as noted below. [Example:

> int x = 12;

> { int x = x; }

> Here the second x is initialized with its own (indeterminate) value. ]


