---
title:  "Constructors"
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

Similarly, we could set the default values where we define the variables.

## Non-Static Member Initialization

```cpp
class Employee
{
private:
    int m_id { 1 };
    int m_salary { 30000 };

public:
    Employee()
    {
    }
};

int main()
{
    // Creates an employee with id 1, salary 30,000
    Employee employee {};

    return 0;
}
```

Rather than writing a default constructor with an empty body, it is more clear to explicitly state this is the code.

```cpp
class Employee
{
private:
    int m_id { 1 };
    int m_salary { 30000 };

public:
    Employee() = default;
};
```

We likely want to be able to specify member variable values when we initialize our objects.

## Constructors with Parameters

The code block below adds a second constructor, which can take two integer parameters. The second parameter is optional in this case, and has its own default value.

```cpp
class Employee
{
private:
    int m_id { 1 };
    int m_salary { 30000 };

public:
    Employee() = default;

    Employee(int id, int salary=30000)
    {
        m_id = id;
        m_salary = salary;
    }
};

int main()
{
    // Creates an employee with id 2, salary 50,000
    Employee employee {2, 50000};

    // Creates an employee with id 3, salary 30,000 (default)
    Employee employee {3};

    return 0;
}
```

Defining variables in this way is effective, except for with const variables. These must be defined on the line where they are declared, and cannot be changed. This causes a problem, as our method above sets a default value, and then overrides it. The solution is to use member initializer lists.

## Member Initializer List

The method can also simplify repetitive constructors. Let's use member variables `name` and `salary` here.

Before reduction:
```cpp
class Employee
{
private:
    std::string m_name;
    int m_salary;

public:
    Employee(std::string_view name)
    {
        m_name = name;
        m_salary = 30000;
    }

    Employee(int salary)
    {
        m_name = "John";
        m_salary = salary;
    }

    Employee(std::string_view name, int salary)
    {
        m_name = name;
        m_salary = salary;
    }
};
```

After:
```cpp
class Employee
{
private:
    std::string m_name {"John"};
    int m_salary {30000};

public:
    // This constructor takes no arguments and uses the defaults above
    Employee() = default;

    Employee(std::string_view name)
        : m_name {name}
    {
    }

    Employee(int salary)
        : m_salary {salary}
    {
    }

    Employee(std::string_view name, int salary)
        : m_name {name}, m_salary {salary}
    {
    }
};
```
