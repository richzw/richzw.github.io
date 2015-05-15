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

- **Copy Constructor and Constructor**

```cpp
class Pt {
public:
	Pt() {
		std::cout << "default constructor" << std::endl;
	}

	Pt(const Pt& rvalue) {
		std::cout << "copy constructor" << std::endl;
	}

	Pt(const Pt&& rvalue) {
		std::cout << "move constructor" << std::endl;
	}

	Pt& operator=(const Pt& rvalue) {
		std::cout << "copy assignment" << std::endl;
		return *this;
	}

	Pt& operator=(const Pt&& rvalue) {
		std::cout << "move assignment" << std::endl;
	}

	~Pt() {
		std::cout << "~Pt" << std::endl;
	}

	//a function to call in order to prevent getting optimized out
	void test() {
		std::cout << " " << std::endl;
	}
};

int i = 1;

int _tmain(int argc, _TCHAR* argv[])
{
	{
		//here the compiler thinks that we declare a function
		std::cout << "step 1" << std::endl;
		Pt pt();
	}
	{
		//here the compiler calls a default constructor
		std::cout << "step 2" << std::endl;
		Pt pt;
	}
	{
		//here the compiler calls a default constructor too
		std::cout << "step 3" << std::endl;
		Pt pt = Pt();
	}

	{
		//here the compiler calls a copy constructor and doesn't call the default constructor prior to that
		// O_o
		std::cout << "step 4" << std::endl;
		Pt pt = pt;

		/*
		Constructions like `type object = something` call copy constructors, not assignment operators

		Having this in mind, here's what happens:

		1. `Pt pt =` -> at this point, `Pt` object is created, named `pt` (nothing is initialized at this point)

		2. `= pt;` -> at this point, `pt`'s copy constructor is called with argument - itself (`pt`)
		
		3. as `pt` is created BUT not initialized (in `1.`), this is (kinda) valid - `pt`'s copy constructor (in `2.`) 
		will be "properly" executed, taking as right-hand-side argument the already existing and uninitialized object pt (from `1.` again)
		Shortly - this is bad.

		It's worth noting, that if the `pt` object is global or static, it will be default-initialized at step `1.` - after reaching the `=`.
		
		*/
	}

	{
		Pt pt1;
		Pt pt2;
		std::cout << "step 5" << std::endl;
		
		pt1 = pt2;
	}

	return 0;
}
```
