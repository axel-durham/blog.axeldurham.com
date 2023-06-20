---
title:  "Constuctors"
mathjax: true
layout: post
categories: [coding, C++, OOP] 
---

Exploring constructors, and the good (and bad) ways of initializing member variables.

## List Initialization

If variables are public, they can simply be initialized using list initilization.

```cpp
class Employee
{
public:
    int m_id {};
    int m_salary {};
};

int main()
{
    // Create employee with id 1, salary 30,000
    Employee employee {1, 30000};

    return 0;
}
```

Leaving all our variables public is less than ideal, though. Enter, constructors. 

## Default Constructors

A constructor with no paramaters is the default constructor. Default values could be specified within.

```cpp
class Employee
{
private:
    int m_id {};
    int m_salary {};

public:
    Employee()
    {
        m_id = 1;
        m_employee = 30000;
    }
};

int main()
{
    // Also creates an employee with id 1, salary 30,000
    Employee employee {};

    return 0;
}
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