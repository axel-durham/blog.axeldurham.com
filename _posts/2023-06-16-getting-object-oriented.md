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

### Another simple class with private members

In this custom `Stack` class I play around with `std::array` and `assert`. Remember that the string attached to the assert condition becomes the error message you see when it fails.

```cpp
class Stack
{
    std::array<int, 10> m_memory {};
    std::size_t m_size {0};

public:
    void reset()
    {
        m_size = 0;
    }

    bool push(int val)
    {
        if (m_size < 10)
        {
            m_memory[m_size] = val;
            ++m_size;
            return true;
        }
        else
        {
            return false;
        }
    }

    int pop()
    {
        assert(m_size > 0 && "Cannot pop from an empty stack");
        
        // Return last item and decrement to shrink the stack
        return m_memory[--m_size];
    }

    void print()
    {
        std::cout << "( ";
        for (auto i = 0; i < m_size; ++i)
        {
            std::cout << m_memory[i] << ' ';
        }
        std::cout << ")\n";
    }
};
```