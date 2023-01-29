# Lab 4 :  Decision making

Welcome to the third CSC 200 lab! This will familiarize you with using `if`, `else` and `elif` conditions for decision making as well as give you some experience in their proper use. **Be sure to read and follow all instructions unless otherwise specified.**  You'll find the table of contents for this lab below.

## Part 1. Introduction

There comes situations in real life when we need to make some decisions and based on these decisions, we decide what should we do next. Similar situations arise in programming also where we need to make some decisions and based on these decisions we will execute the next block of code. Decision-making statements in programming languages decide the direction of the flow of program execution.

``` {image} decision_making.png
:align: center
```

## Part 2. Decision making statements

### `if` statement in c++

```````` {card}

`if` statement is the most simple decision-making statement. It is used to decide whether a certain statement or block of statements will be executed or not i.e if a certain condition is `true` then a block of statement is executed otherwise not.  Here, the **condition** after evaluation will be either `true` or `false`. If the condition is `true` then it will execute the block of statements below it otherwise not.

``````` {tab-set}
`````` {tab-item} syntax
``` {code-block} c++
if (condition)
{
  //Statement to execute if condition is treu
}
```

If we do not provide the curly braces ‘{‘ and ‘}’ after if(condition) then by default if statement will consider the first immediately below statement to be inside its block. 

``` {code-block} c++
if(condition)
  statement1;
  statement2;

// Here if the condition is true, if block will consider only statement1 to be inside 
// its block.
```
``````
`````` {tab-item} example
``` {code-block} c++
#include<iostream>

int main()
{
  int i = 10;

  if (i > 15)
  {
    std::cout<<"10 is less than 15";
  }   

  std::cout<<"I am Not in if";
}
```
``````
`````` {tab-item} output
``` {code-block} bash
I am Not in if
```
because `i` is smaller that 15, the condition is `false` then the block below the `if` statement is not executed.
``````
```````
````````

### `if-else` statement in c++

```````` {card}
The `if` statement alone tells us that if a condition is `true` it will execute a block of statements and if the condition is `false` it won’t. But what if we want to do something else if the condition is false. Here comes the C++ `else` statement. We can use the `else` statement with `if` statement to execute a block of code when the condition is `false`.

``````` {tab-set}
`````` {tab-item} syntax
``` {code-block} c++
if (condition)
{
    // Executes this block if condition is true
}
else
{
    // Executes this block if condition is false
}
```
``````
`````` {tab-item} example
``` {code-block} c++
#include<iostream>

int main()
{
        int i = 20;
  
        if (i < 15)
            std::cout<<"i is smaller than 15";
        else
            std::cout<<"i is greater than 15";
            
    return 0;   
}
```
``````
`````` {tab-item} output
``` {code-block} bash
i is greater than 15
```
The block of code following the `else` statement is executed as the condition present in the `if` statement is `false`.
``````
```````
````````

### nested-`if` in c++

```````` {card}
A nested if in C++ is an if statement that is the target of another if statement. Nested if statements mean an if statement inside another if statement. Yes, C++ allows us to nested if statements within if statements, i.e, we can place an if statement inside another if statement. 
condition is false. Here comes the C++ `else` statement. We can use the `else` statement with `if` statement to execute a block of code when the condition is `false`.

``````` {tab-set}
`````` {tab-item} syntax
``` {code-block} c++
if (condition1) 
{
  // Executes when condition1 is true
  if (condition2) 
  {
      // Executes when condition2 is true
  }
}
```
``````
`````` {tab-item} example
``` {code-block} c++
#include <iostream>

int main()
{
int i = 10;

if (i == 10)
{
  // First if statement
  if (i < 15)
  std::cout<<"i is smaller than 15\n";

  // Nested - if statement Will only be executed if statement above is true
  if (i < 12)
    std::cout<<"i is smaller than 12 too\n";
  else
    std::cout<<"i is greater than 15";
}

return 0;
}
```
``````
`````` {tab-item} output
``` {code-block} bash
i is smaller than 15
i is smaller than 12 too
```
``````
```````
````````

### `if`-`else`-`if` in c++

```````` {card}
Here, a user can decide among multiple options. The C++ if statements are executed from the top down. As soon as one of the conditions controlling the if is true, the statement associated with that if is executed, and the rest of the C++ else-if ladder is bypassed. If none of the conditions are true, then the final else statement will be executed. 

``````` {tab-set}
`````` {tab-item} syntax
``` {code-block} cpp
```cpp
if (condition)      statement;
else if (condition) statement;
else                statement;
```
``````
`````` {tab-item} example
``` {code-block} c++
#include<iostream>

int main() {
    int i = 20;
    
    if (i == 10)        std::cout<<"i is 10";
    else if (i == 15)   std::cout<<"i is 15";
    else if (i == 20)   std::cout<<"i is 20";
    else                std::cout<<"i is not present";
}
```
``````
`````` {tab-item} output
``` {code-block} bash
i is 20
```
``````
```````
````````

### `switch` statement in c++

```````` {card}
Switch case statement evaluates a given expression and based on the evaluated value(matching a certain condition), it executes the statements associated with it. Basically, it is used to perform different actions based on different conditions(cases).
: Switch case statements follow a selection-control mechanism and allow a value to change control of execution.
: They are a substitute for long `if` statement that compare a variable to several integral values.
: The switch statement is a multiway branch statement. It provides an easy way to dispatch execution to different parts of code based on the value of the expression.


``````` {tab-set}
`````` {tab-item} syntax
``` {code-block} c++
switch (n)
{
    case 1: // code to be executed if n = 1;
        break;
    case 2: // code to be executed if n = 2;
        break;
    default: // code to be executed if n doesn't match any cases
}
```
``````
`````` {tab-item} example
``` {card} Terminology
`break`
: This keyword is used to stop the execution inside a `switch` block. It helps to terminate the `switch` block and break out of it.

`default`
: This keyword is used to specify the set of statements to execute if there is no case match.
```
   
``` {card} Important Points About Switch Case Statements:** 
- The expression provided in the switch should result in a **constant value** otherwise it would not be valid. Some valid expressions for switch case will be
- Duplicate case values are not allowed.
- The `default` statement is optional. Even if the `switch` case statement do not have a `default` statement, it would run without any problem.
- The `break` statement is used inside the `switch` to **terminate a statement** sequence. When a `break` statement is reached, the `switch` terminates, and the flow of control jumps to the next line following the `switch` statement.
- The `break` **statement is optional**. If omitted, execution will continue on into the next case. The flow of control will fall through to subsequent cases until a `break` is reached.
- **Nesting of `switch` statements is allowed**, which means you can have `switch` statements inside another `switch`. However nested `switch` statements should be avoided as it makes the program more complex and less readable. 
- `switch` statements are **limited to integer values** only in the check condition.

``` {code-block} c++
#include <iostream>

int main()
{
int x = 2;
switch (x) {
    case 1:
      std::cout << "Choice is 1";
      break;
    case 2:
      std::cout << "Choice is 2";
      break;
    case 3:
      std::cout << "Choice is 3";
      break;
    default:
      std::cout << "Choice other than 1, 2 and 3";
      break;
}
return 0;
}
```
``````
`````` {tab-item} output
``` {code-block} bash
Choice is 2
```
``````
```````
````````

## Part 3. Exercises

``` {card} 1. Write a program
...that tells whether a given letter is a consonant or vowel.
```

``` {card} 2. Write a program
...that takes a value from the user as input any character and check whether it is the alphabet, digit or special character. Using if-else.
```

``` {card} 2. Write a program
...that checks whether a number is a prime or composite number.
```

```` {card} 4. Write a program
...that takes the basic salary of an employee as input and calculate its Gross salary by using the if-else statement. according to the following:

``` {code-block} bash
Basic Salary <= 10000 : HRA = 20%, DA = 80%
Basic Salary <= 20000 : HRA = 25%, DA = 90%
Basic Salary > 20000  : HRA = 30%, DA = 95%
```
````

### Requirements

``` {card}
1. Exercise 1 completed.
2. Exercise 2 completed.
2. Exercise 3 completed.
2. Exercise 4 completed.
```
