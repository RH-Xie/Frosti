---
title: C++笔记
pubDate: 2021/5/31 13:29:00
description: 一些简陋的C++笔记，仅作个人参考
tags:
  - 笔记
categories:
  - tech
image: https://images.weserv.nl/?url=s2.loli.net/2023/08/22/WJHGmBMSx3dKjwc.webp
---



# C++

Warning: This passage includes wrong grammar, wrong words.

---

How to understand pure virtual function and abstract class ?

We can't always know the implementation of base class, for it's just not sure before derivate classes define the functions to make that description. For instance, we define a base class Shape, but we can't draw it before we define it's real shape in a derivate class, Rectangle or Triangle. In this occasion, the base class didn't initialize the parameters or functions on how to draw it, because none of the methods to initialization seems to be appropriate. We can't just draw a default rectangle instead of letting users use derivate classes. Why not let users make a good use of derivate classes ?

---

Which to choose?

There's a template function containing arguments of type Double and type Float. Then I call the function and key 1.1 and 2.2 into it. Then what's type of these two temporary arguments?

In fact, if you just do this, both arguments will be recognized as type Double. What about forcing the second argument into Float? That will go as you think : the second argument is successfully changed into Float.

In short, C++ Compiler regards decimals as Double at default, but you can force it into Float or Int.

---

How to call Template Function directly without calling normal function I defined?

Just use this format:

```cpp
FunctionName<>(argument1, argument2);
```

There's nothing in <>, but this provides the hint for compiler to use the template function.

How to forcibly NOT call template function?

Easy. Just let the template have only one typename and two arguments in this same type, then key two different types of arguments in it. This will run well once you prepare the corresponding function you want to call.

```cpp
#include<iostream>
using namespace std;

template <typename T>
double mmax(T a, T b)//I do NOT want to call this!!
{
	return a >b?a:b;
}

int mmax(int a, char b)//And I want to call this instead!
{
	return a > b ? a : b;
}

int main()
{
	cout << mmax(1,1.2222);//This is what I said "key two different types of arguments"
}
```

How to skip variable with `const` in class?

Use the Initialization Function when .

---

Today I saw an **AMAZING** explanation of how to pass the size of an array.

@[https://stackoverflow.com/questions/1328223/when-a-function-has-a-specific-size-array-parameter-why-is-it-replaced-with-a-p](https://stackoverflow.com/questions/1328223/when-a-function-has-a-specific-size-array-parameter-why-is-it-replaced-with-a-p)

The function:

```cpp
void foo ( char a[100] );
```

Will have the parameter adjusted to be a pointer, and so becomes:

```cpp
void foo ( char * a );
```

If you want that the array type is preserved, you should pass in a reference to the array:

```cpp
void foo ( char (&a)[100] );
```

**C++ '03 8.3.5/3:**

> ...The type of a function is determined using the following rules. The type of each parameter is determined from its own decl-specifier-seq and declarator. After determining the type of each parameter, any parameter of type "array of T" or "function returning T" is adjusted to be "pointer to T" or "pointer to function returning T," respectively....

**To explain the syntax:**

Check for "right-left" rule in google; I found one description of it [here](http://www.cpp-home.com/archives/106.html).

It would be applied to this example approximately as follows:

```cpp
void foo (char (&a)[100]);
```

Start at identifier 'a'

> 'a' is a

Move right - we find a `)` so we reverse direction looking for the `(`. As we move left we pass `&`

> 'a' is a reference

After the `&` we reach the opening `(` so we reverse again and look right. We now see `[100]`

> 'a' is a reference to an array of 100

And we reverse direction again until we reach `char`:

> 'a' is a reference to an array of 100 chars

Text above elaborately explains how the right-left works.

And I say that Notion is a quite good place for pasting codes and pages. It even retains the links (Hypertext) in pages that you copy.

---

I don't know how important on adding `this` to a base class which has derivate class until today. It is convenient for you to copy them directly to the derivate class without frequently adding `this` . But don't do it in friend function.

Overloading of signal "=' could **NOT** be declared as a friend function.

Declaration order of class

If vs show some problems on "see the declaration of class xx" and "xxx is not a member of class xx", but actually xxx is a member of class xx, then you need to check whether your class xx includes other classes. If it does, make the included one declared in front of class xx.