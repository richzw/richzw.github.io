---
layout: post
title: C++ Jotting
---

Precompiled Header (PCH)
-------------

> To reduce compilation time, some compiler allow head file to be precompiled into a form that is faster for compiler to process

**Forward Declaration** of one class instead of including the header file

How to get the length of one array as one parameter
-------------

```cpp
template <typename T, unsigned int N>
unsigned int sizeofarray(T (&)[N])
{
    return N;
}

int A[5];
unsigned int size = sizeofarray(A);
```
