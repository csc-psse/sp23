# Lab 10 : `Class` Structure & Diagraming in C++

Welcome to the eighth session of  CSC 200 lab! This will familiarize you with reading class structure as well as give you some experience in their proper use. **Be sure to read and follow all instructions unless otherwise specified.**  You'll find the table of contents for this lab below.

## Part 1. Introduction

### `Class`

``` {card}
A `class` in C++ is the building block that leads to Object-Oriented programming. It is a user-defined data type, which holds its own data members and member functions, which can be accessed and used by creating an instance of that `class`. A C++ `class` is like a blueprint for an object.
For Example: Consider the `Class` of `Cars`. There may be many cars with different names and brand but all of them will share some common properties like all of them will have *4 wheels*, *Speed Limit*, *Mileage range*, etc. So here, `Car` is the `class` and wheels, speed limits, mileage are their properties.

- A `Class` is a user defined data-type which has data members and member functions.
- Data members are the data variables and member functions are the functions used to manipulate these variables and together these data members and member functions defines the properties and behavior of the objects in a `Class`.
- In the above example of class `Car`, the data member will be *speed limit*, *mileage* etc and member functions can be *apply brakes*, *increase speed* etc.

An **Object** is an instance of a `Class`. When a class is defined, no memory is allocated but when it is instantiated (i.e. an object is created) memory is allocated.
```

## Part 2. `Class` Definition

A class is defined in C++ using keyword class followed by the name of class. The body of class is defined inside the curly brackets and terminated by a semicolon at the end.

``` {image} https://media.geeksforgeeks.org/wp-content/cdn-uploads/Classes-and-Objects-in-C.png
:align: center
```

### Declaring Objects

When a class is defined, only the specification for the object is defined; no memory or storage is allocated. To use the data and access functions defined in the class, you need to create objects.

```` {card} Syntax
``` {code-block} cpp
Class Name ObjectName;
```
````

### Accessing data members and member functions

The data members and member functions of class can be accessed using the dot(‘.’) operator with the object. For example if the name of object is `obj` and you want to access the member function with the name `printName()` then you will have to write `obj.printName()`.

### Accessing Data Members

The public data members are also accessed in the same way given however the private data members are not allowed to be accessed directly by the object. Accessing a data member depends solely on the access control of that data member.

This access control is given by Access modifiers in C++. There are three access modifiers : **public, private and protected**.

```` {card} example
``` {code-block} cpp
// C++ program to demonstrate
// accessing of data members

#include <bits/stdc++.h>
class Geeks
{
    // Access specifier
    public:
    
    // Data Members
    string geekname;
    
    // Member Functions()
    void printname()
    {
        std::cout << "Geekname is: " << geekname;
    }
};

int main() {
    
    // Declare an object of class geeks
    Geeks obj1;
    
    // accessing data member
    obj1.geekname = "Abhi";
    
    // accessing member function
    obj1.printname();
    return 0;
}


```

output
``` {code-block} bash
Geekname is: Abhi
```
````

### Access modifier in C++

Access Modifiers or Access Specifiers in a class are used to assign the accessibility to the class members. That is, it sets some restrictions on the class members not to get directly accessed by the outside functions.

``` {card} Types of access modifiers available in C++
`Public`  
`Private`  
`Protected`  

_Note: If we do not specify any access modifiers for the members inside the class then by default the access modifier for the members will be `Private`._
```

Let us now look at each one these access modifiers in details:

#### `Public`

`````` {card}
All the class members declared under the public specifier will be available to everyone. The data members and member functions declared as public can be accessed by other classes and functions too. The public members of a class can be accessed from anywhere in the program using the direct member access operator (.) with the object of that class.

````` {card} Example

``` {code-block} cpp
// C++ program to demonstrate public
// access modifier

#include<iostream>

// class definition
class Circle
{
    public:
        double radius;

        double compute_area()
        {
            return 3.14*radius*radius;
        }
};

// main function
int main()
{
    Circle obj;
    
    // accessing public datamember outside class
    obj.radius = 5.5;
    
    std::cout << "Radius is: " << obj.radius << "\n";
    std::cout << "Area is: " << obj.compute_area();
    return 0;
}
```

Output

``` {code-block} bash
Radius is: 5.5
Area is: 94.985
```
`````

In the above program the data member `radius` is declared as `public` so it could be accessed outside the class and thus was allowed access from inside `main()`. 

``````

#### `Private`

`````` {card}
The class members declared as *private* can be accessed only by the member functions inside the class. They are not allowed to be accessed directly by any object or function outside the class. Only the member functions or the [friend functions](https://www.geeksforgeeks.org/friend-class-function-cpp/) are allowed to access the private data members of a class. 

````` {card} Example

``` {code-block} cpp
// C++ program to demonstrate private
// access modifier

#include<iostream>

class Circle
{
    // private data member
    private:
        double radius;
    
    // public member function
    public:
        double compute_area()
        { // member function can access private
            // data member radius
            return 3.14*radius*radius;
        }
};

// main function
int main()
{
    // creating object of the class
    Circle obj;
    
    // trying to access private data member
    // directly outside the class
    obj.radius = 1.5;
    
    std::cout << "Area is:" << obj.compute_area();
    return 0;
}
```

Output:

``` {code-block} bash
 In function 'int main()':
11:16: error: 'double Circle::radius' is private
         double radius;
                ^
31:9: error: within this context
     obj.radius = 1.5;
```

The output of above program is a compile time error because we are not allowed to access the private data members of a class directly outside the class. Yet an access to obj.radius is attempted, radius being a private data member we obtain a compilation error. 
`````

However, we can access the private data members of a class indirectly using the public member functions of the class. 

````` {card} Example

``` {code-block} cpp
// C++ program to demonstrate private
// access modifier

#include<iostream>

class Circle
{
    // private data member
    private:
        double radius;
    
    // public member function
    public:
        void compute_area(double r)
        {   // member function can access private
            // data member radius
            radius = r;
        
            double area = 3.14*radius*radius;
        
            std::cout << "Radius is: " << radius << endl;
            std::cout << "Area is: " << area;
        }
};

// main function
int main()
{
    // creating object of the class
    Circle obj;
    
    // trying to access private data member
    // directly outside the class
    obj.compute_area(1.5);
    
    return 0;
}
```

Output

``` {code-block} bash
Radius is: 1.5
Area is: 7.065
```
`````
``````

#### `Protected`

`````` {card}
Protected access modifier is similar to private access modifier in the sense that it can’t be accessed outside of it’s class unless with the help of friend class, the difference is that the class members declared as Protected can be accessed by any subclass(derived class) of that class as well. 

_Note: This access through inheritance can alter the access modifier of the elements of base class in derived class depending on the [modes of Inheritance](https://www.geeksforgeeks.org/inheritance-in-c/#Modes) of Inheritance (Don't worry, you'll this nex session)._

````` {card} Example

``` {code-block} cpp
// C++ program to demonstrate
// protected access modifier
#include <bits/stdc++.h>

// base class
class Parent
{
    // protected data members
    protected:
    int id_protected;
};

// sub class or derived class from public base class
class Child : public Parent
{
    public:
    void setId(int id)
    {
        // Child class is able to access the inherited
        // protected data members of base class

        id_protected = id;
    }
    
    void displayId()
    {
        std::cout << "id_protected is: " << id_protected << endl;
    }
};

// main function
int main() {
    
    Child obj1;
    
    // member function of the derived class can
    // access the protected data members of the base class
    
    obj1.setId(81);
    obj1.displayId();
    return 0;
}
```

Output:

``` {code-block} bash
id_protected is: 81
```
`````
``````

### Member Functions in Classes

`````` {card}

``` {card} Defining a member function:
- Inside class definition
- Outside class definition
```

To define a member function outside the class definition we have to use the scope resolution :: operator along with class name and function name.

````` {card} Example
``` {code-block} cpp
// C++ program to demonstrate function
// declaration outside class

#include <bits/stdc++.h>
class Geeks
{
    public:
    string geekname;
    int id;
    
    // printname is not defined inside class definition
    void printname();
    
    // printid is defined inside class definition
    void printid()
    {
        std::cout << "Geek id is: " << id;
    }
};

// Definition of printname using scope resolution operator ::
void Geeks::printname()
{
    std::cout << "Geekname is: " << geekname;
}
int main() {
    
    Geeks obj1;
    obj1.geekname = "xyz";
    obj1.id=15;
    
    // call printname()
    obj1.printname();
    cout << endl;
    
    // call printid()
    obj1.printid();
    return 0;
}
```

Output:

``` {code-block} cpp
Geekname is: xyz
Geek id is: 15
```
`````

``` {note}
- All the member functions defined inside the class definition are by default **inline**, but you can also make any non-class function inline by using keyword inline with them. Inline functions are actual functions, which are copied everywhere during compilation, like pre-processor macro, so the overhead of function calling is reduced.

- Declaring a[ friend function ](https://www.geeksforgeeks.org/friend-class-function-cpp/)is a way to give private access to a non-member function.
```
``````

### Constructor

`````` {card}
Constructors are special class members which are called by the compiler every time an object of that class is instantiated. Constructors have the same name as the class and may be defined inside or outside the class definition.

``` {card} Types of constructors:
- [Default constructors](https://www.geeksforgeeks.org/constructors-c/)
- Parameterized constructors
- [Copy constructors](https://www.geeksforgeeks.org/copy-constructor-in-cpp/)
```

```` {card} example
``` {code-block} cpp
// C++ program to demonstrate constructors

#include <bits/stdc++.h>
class Geeks
{
    public:
    int id;
    
    //Default Constructor
    Geeks()
    {
        std::cout << "Default Constructor called" << endl;
        id=-1;
    }
    
    //Parameterized Constructor
    Geeks(int x)
    {
        std::cout << "Parameterized Constructor called" << endl;
        id=x;
    }
};
int main() {

    // obj1 will call Default Constructor
    Geeks obj1;
    std::cout << "Geek id is: " <<obj1.id << endl;
    
    // obj1 will call Parameterized Constructor
    Geeks obj2(21);
    std::cout << "Geek id is: " <<obj2.id << endl;
    return 0;
}
```

Output

```
Default Constructor called
Geek id is: -1
Parameterized Constructor called
Geek id is: 21
```
````

A **Copy Constructor** creates a new object, which is exact copy of the existing object. The compiler provides a default Copy Constructor to all the classes.

```` {card} syntax
``` {code-block} cpp
class-name (class-name &){}
```
````

``````

### Destructors

Destructor is another special member function that is called by the compiler when the scope of the object ends.

`````` {card} example

``` {code-block} cpp
// C++ program to explain destructors

#include <bits/stdc++.h>
class Geeks
{
    public:
    int id;
    
    //Definition for Destructor
    ~Geeks()
    {
        std::cout << "Destructor called for id: " << id <<endl;
    }
};

int main()
{
    Geeks obj1;
    obj1.id=7;
    int i = 0;
    while ( i < 5 )
    {
        Geeks obj2;
        obj2.id=i;
        i++;
    } // Scope for obj2 ends here
    
    return 0;
    } // Scope for obj1 ends here
```

Output

``` {code-block} bash
Destructor called for id: 0
Destructor called for id: 1
Destructor called for id: 2
Destructor called for id: 3
Destructor called for id: 4
Destructor called for id: 7
```
``````

## Part 3. Exercises

``` {card} Overview
1. Define and implement a class called `UltimateBridgeSolver`. **Use a header file** for your class declaration **and a separate .cpp file** for your implementation.

2. `UltimateBridgeSolver` should contain the following variables and functions, note what needs to be private vs public:

3. Create a **new file** to serve as your **main program file** and save it as **UBSTester.cpp**
   - _This file should only have one function, the `main()` function. In your `main()`_
     - Guidance to follow...

What to Submit
: UltimateBridgeSolver.h
: ​UltimateBridgeSolver.cpp
: UBSTester.cpp
```

``` {figure} images/uml.png
:align: center

Below are descriptions for each function
```

``` {card} Function descriptions

`UltimateBridgeSolver()`
: is a no argument constructor that sets smallLen to 1 and bigLen to 5

`UltimateBridgeSolver(b : int)`
: is a constructor that sets bigLen to b

`getBigLen()`
: returns the value of `bigLen`

`getSmallLen()`
: returns the value of `smallLen`

`canBuild(smalls : int, bigs : int, n : int)`
: returns `true` if we can build a bridge of exactly of length `n` using at most smalls boards of length `smallLen` and at most bigs boards of `bigLen`. For example, if `bigLen` is 8, then `canBuild(1, 3, 5)` would return `false`

`howManyBigs(smalls : int, bigs : int, n : int)`
: returns exactly how many boards of length `bigLen` we need to build a bridge of length `n` or -1 if it can’t be built. Hint: Use a layered call to `canBuild()`

`howManySmalls(smalls : int, bigs : int, n : int)`
: returns exactly how many boards of length `smallLen` we need to build a bridge of length `n` or -1 if it can’t be built. Hint: Use layered calls to `canBuild()` and `howManyBigs()`

`solve(smalls : int, bigs : int, n : int)`
: prints how many boards of each length are needed to build a bridge of length `n` or prints that the bridge cannot be made. Hint: Use layered calls to `canBuild()`, `howManyBigs()`, and `howManySmalls()`
```

:::: {card} `main()`

- Create an instance of your `UltimateBridgeSolver` using the no argument constructor

- Call `getBigLen()` and `getSmallLen()` as shown below to test that they are correct (in this example, the reference variable to my `UltimateBridgeSolver` object is called `mySolver`). If they print `false` (i.e., 0) then there is a bug in your code:

    ``` {code-block}
    cout << (mySolver.getBigLen() == 5);
    cout << (mySolver.getSmallLen() == 1);
    ```

- Perform the following calls testing what your functions return, as shown above and in the testing slides. I’ve given you partial answers, the rest you should figure out on your own:

    ``` {code-block} cpp
    solve(3, 1, 8)       //can build with 1 big and 3 smalls
    solve(3, 1, 9)       //can’t build
    solve(3, 5, 14)      //can’t build
    solve(14, 5, 14)     //can build with 14 smalls
    solve(4, 3, 7)       //can build with 1 big and 2 smalls
    ```

- Create an instance of your `UltimateBridgeSolver` using the overloaded `constructor`.

- Create your own set of tests to ensure your functions work as expected for both instances of the class (default and overloaded constructor)
::::

### Requirements

``` {card}
- Code was divided into appropriate files, as specified, and was done so correctly
- Member variables are correctly labeled public or private, per UML diagram
- Member functions are correctly labeled public or private, per UML diagram
- Member function signatures match UML diagram
- Functions work correctly, as specified
- Correct use of layered calls, as instructed
- Tests performed correctly and as instructed for default constructor object
- Tests performed correctly and as instructed for overloaded constructor object
```
