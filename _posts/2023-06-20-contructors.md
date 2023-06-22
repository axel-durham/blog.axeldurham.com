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
