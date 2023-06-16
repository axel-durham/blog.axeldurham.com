---
title:  "Getting Object Oriented"
mathjax: true
layout: post
categories: [coding, C++, OOP] 
---

## learncpp

Working through the [learncpp](https://www.learncpp.com) course has introducted me to a lot of object-orientated examples and principles but it's hard to internalize these without lots of examples.

So, starting with the basics...

## The Basics

A super simple class containing a pair of integers, with only public methods `set()` and `print()`.

```cpp
class IntPair
{
public:
    int m_int1 {};
    int m_int2 {};

    void set(int num1, int num2)
    {
        m_int1 = num1;
        m_int2 = num2;
    }

    void print()
    {
        std::cout << "Pair(" << m_int1 << ", " << m_int2 << ")\n";
    }
};
```

### A class with some private members

While the member variables are private, they can still be seen by any instance of the `Point3d` class. So `isEqual()` can view the member variables of the two objects it is comparing. 

```cpp
class Point3d
{
    int m_x {};
    int m_y {};
    int m_z {};

public:
    void setValues(int x, int y, int z)
    {
        m_x = x;
        m_y = y;
        m_z = z;
    }

    void print()
    {
        std::cout << "<" << m_x << ", " << m_y << ", " << m_z << ">\n";
    }

    bool isEqual(Point3d point2)
    {
        return (m_x == point2.m_x && m_y == point2.m_y && m_z == point2.m_z);
    }
};
```

