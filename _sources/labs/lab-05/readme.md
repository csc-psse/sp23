# Lab 5 :  Loops in C++

Welcome to the fourth CSC 200 lab! This will familiarize you with using Loops, as well as give you some experience in their proper use. **Be sure to read and follow all instructions unless otherwise specified.**  You'll find the table of contents for this lab below.

## Part 1. Introduction

Loops in programming come into use when we need to repeatedly execute a block of statements. For example: Suppose we want to print “Hello World” 10 times. This can be done in two ways as shown below:

### Iterative Method

An iterative method to do this is to write the cout statement 10 times

``` {code-block} cpp
#include <iostream>

int main()
{
    std::cout << "Hello World\n";
    std::cout << "Hello World\n";
    std::cout << "Hello World\n";
    std::cout << "Hello World\n";
    std::cout << "Hello World\n";
    std::cout << "Hello World\n";
    std::cout << "Hello World\n";
    std::cout << "Hello World\n";
    std::cout << "Hello World\n";
    std::cout << "Hello World\n";
    return 0;
}

```

### Using Loops

In loop, the statement needs to be written only once and the loop will be executed 10 times as shown below. In computer programming, a **loop** is a sequence of instructions that is **repeated** until a certain **condition** is reached.
: An operation is done, such as getting an item of data and changing it, and then some condition is checked such as whether a counter has reached a prescribed number.
: **Counter not Reached:** If the counter has not reached the desired number, the next instruction in the sequence returns to the first instruction in the sequence and repeat it.
: **Counter reached:** If the condition has been reached, the next instruction “falls through” to the next sequential instruction or branches outside the loop.

```` {card} Common loop types
``` {image} images/Loops_in_cpp.png
:align: center
```
Entry Controlled
: In this type of loops the test condition is tested before entering the loop body.`for` and `while` loops are entry controlled loops.

Exit Controlled Loops
: In this type of loops the test condition is tested or evaluated at the end of loop body. Therefore, the loop body will execute atleast once, irrespective of whether the test condition is true or false. `do`–`while` loop is an exit controlled loop.
````

## Part 2. Loops in C++

### `for` Loop in c++

```````` {card}
A for loop is a repetition control structure which allows us to write a loop that is executed a specific number of times. The loop enables us to perform n number of steps together in one line.

``````` {tab-set}
`````` {tab-item} syntax
``` {code-block} c++
for (initialization expr; test expr; update expr)
{    
      // body of the loop(statements we want to execute)
}
```
In for loop, a loop variable is used to control the loop. First initialize this loop variable to some value, then check whether this variable is less than or greater than counter value. If statement is true, then loop body is executed and loop variable gets updated . Steps are repeated till exit condition comes.

Initialization Expression
: In this expression we have to initialize the loop counter to some value.
    example: `int i = 1;`

Test Expression
: In this expression we have to test the condition. If the condition evaluates to true then we will execute the body of loop and go to update expression otherwise we will exit from the for loop. 
    example: `i <= 10;`

- **Update Expression**: After executing loop body this expression increments/decrements the loop variable by some value.
    example: `i++`;

``````
`````` {tab-item} example
``` {code-block} c++
#include <iostream>
   
int main()
{
      for (int i = 1; i <= 10; i++)
      {
         std::cout << "Hello World\n";
      }
   
      return 0;
}
```
``````
`````` {tab-item} output
``` {code-block} bash
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
```

``````
```````
````````

### `while` loop in c++

```````` {card}
While studying `for` loops we have seen that the number of iterations is known beforehand, i.e. the number of times the loop body is needed to be executed is known to us. `while` loops are used in situations where we do not know the exact number of iterations of loop beforehand. The loop execution is terminated on the basis of test condition.

We have already stated that a loop is mainly consisted of three statements – initialization expression, test expression, update expression. The syntax of the three loops – `for`, `while` and `do while` mainly differs on the placement of these three statements.

``````` {tab-set}
`````` {tab-item} syntax
``` {code-block} c++
initialization expression;
while (test_expression)
{
   // statements
   
   update_expression;
}

```
``````
`````` {tab-item} example
``` {code-block} c++
#include <iostream>

int main()
{
      // initialization expression
      int i = 1;
   
      // test expression
      while (i < 6)
      {
         std::cout << "Hello World\n";
   
         // update expression
         i++;
      }
   
      return 0;
}
```
``````
`````` {tab-item} output
``` {code-block} bash
Hello World
Hello World
Hello World
Hello World
Hello World
```
``````
```````
````````

### `do while` loop in c++

```````` {card}
In `do while` loops also the loop execution is terminated on the basis of test condition. The main difference between `do while` loop and `while` loop is in `do while` loop the condition is tested at the end of loop body, i.e `do while` loop is exit controlled whereas the other two loops are entry controlled loops.

_Note: In `do while` loop the loop body will execute at least once irrespective of test condition._

``````` {tab-set}
`````` {tab-item} syntax
``` {code-block} c++
initialization expression;
do
{
   // statements

   update_expression;
} while (test_expression);
```

_Note: Notice the semi – colon(“;”) in the end of loop._
``````
`````` {tab-item} example
``` {code-block} c++
#include <iostream>

int main()
{
   int i = 2; // Initialization expression

   do
   {
      // loop body
      std::cout << "Hello World\n";

      // update expression
      i++;

   } while (i < 1); // test expression

   return 0;
}
```
``````
`````` {tab-item} output
``` {code-block} bash
Hello World
```
In the above program the test condition (`i < 1`) evaluates to false. But still as the loop is exit – controlled the loop body will execute once.
``````
```````
````````

### **What about an Infinite Loop?**

```````` {card}
An infinite loop (sometimes called an endless loop ) is a piece of coding that lacks a functional exit so that it repeats indefinitely. An infinite loop occurs when a condition always evaluates to true. Usually, this is an **error**.

```` {card} example

```{code-block} c++
// Uncomment the sections to see the output

#include <iostream>

int main ()
{
   int i;

   // This is an infinite for loop as the condition
   // expression is blank
   for ( ; ; )
   {
      std::cout << "This loop will run forever.\n";
   }

   // This is an infinite for loop as the condition
   // given in while loop will keep repeating infinitely
   /*
   while (i != 0)
   {
      i-- ;
      cout << "This loop will run forever.\n";
   }
   */

   // This is an infinite for loop as the condition
   // given in while loop is "true"
   /*
   while (true)
   {
      cout << "This loop will run forever.\n";
   }
   */
}
```

Output:

``` {code-block} bash
This loop will run forever.
This loop will run forever.
................... 
```

``` {card} Important Points
- Use **for loop** when number of iterations is known beforehand, i.e. the number of times the loop body is needed to be executed is known.
- Use **while loops** where exact number of iterations is not known but the loop termination condition is known.
- Use **do while loop** if the code needs to be executed at least once like in Menu driven programs
```
````````   

## Part 3. Nested Loops in C++

**Nested loop** means a **loop statement** inside another loop statement. That is why nested loops are also called as “**loop inside loop**“.

``````` {card} Syntax of nested loops

`````` {tab-set}
````` {tab-item} for
``` {code-block} cpp
for ( initialization; condition; increment ) {

   for ( initialization; condition; increment ) {
      
      // statement of inside loop
   }

   // statement of outer loop
}
```
````` 
````` {tab-item} while
``` {code-block} cpp
while(condition) {

   while(condition) {
      
      // statement of inside loop
   }

   // statement of outer loop
}
```
````` 
````` {tab-item} do while
``` {code-block} cpp
do{

   do{
      
      // statement of inside loop
   } while (condition);

   // statement of outer loop
} while (condition);
```
`````
````` {tab-item} do-while-for
``` {code-block} cpp
do{

   while(condition) {
      
      for ( initialization; condition; increment ) {
      
         // statement of inside for loop
      }

      // statement of inside while loop
   }

   // statement of outer do-while loop
} while (condition);
```
`````
``````
```````

## Part 4. Loops Control Statement

### `break`

```` {card}
The **break** in C++ is a loop control statement which is used to terminate the loop. As soon as the break statement is encountered from within a loop, the loop iterations stops there and control returns from the loop immediately to the first statement after the loop.

**Syntax:**

``` {code-block} c++
break;
```

When we can use **break** :

we are not sure about the actual number of iterations for the loop or we want to terminate the loop based on some condition.

**We will see here the usage of break statement with three different types of loops:**

1. Simple loops

2. Nested loops

3. Infinite loops

   

Let us now look at an examples for simple loop using break statement.

``` {code-block} c++
for (int i = 0; i < 10; i++) {
   if (i == 4) {
      break;
   }
   std::cout << i << "\n";
} 
```
````

### `continue`

````````` {card}
`Continue` is also a loop control statement just like the break. `continue` statement is opposite to that of `break` statement, instead of terminating the loop, it forces to execute the next iteration of the loop.

As the name suggest the `continue` statement forces the loop to continue or execute the next iteration. When the `continue` statement is executed in the loop, the code inside the loop following the `continue` statement will be skipped and next iteration of the loop will begin.

``````` {tab-set}
`````` {tab-item} syntax
``` {code-block} c++
continue;
```
``````
`````` {tab-item} example
Consider the situation when you need to write a program which prints number from 1 to 10 and but not 6. It is specified that you have to do this using loop and only one loop is allowed to use.
Here comes the usage of `continue` statement. What we can do here is we can run a loop from 1 to 10 and every time we have to compare the value of iterator with 6. If it is equal to 6 we will use the `continue` statement to continue to next iteration without printing anything otherwise we will print the value.

Below is the implementation of the above idea:
``` {code-block} c++
#include <iostream>

int main()
{
   // loop from 1 to 10
   for (int i = 1; i <= 10; i++) {

      // If i is equals to 6,
      // continue to next iteration
      // without printing
      if (i == 6)
         continue;

      else
         // otherwise print the value of i
         std::cout << i << " ";
   }

   return 0;
}
```
``````
`````` {tab-item} output
``` {code-block} bash
1 2 3 4 5 7 8 9 10 
```
The `continue` statement can be used with any other loop also like while or do while in a similar way as it is used with for loop above.
``````
```````
`````````

## Part 5. Exercises

```` {card} 1. Print all numbers from 1 to n in reverse, comma seperated.
_Note: The last element should not have a comma placed after it!_
   
``` {code-block} bash
Enter your number: 5
Ouput :  5, 4, 3, 2, 1
```
````

```` {card} 2. Given a number n, print a right triangle similar to the one below.

``` {code-block} bash
Input: 7
Output:
*
* * 
* * *
* * * *
* * * * *
* * * * * *
* * * * * * *
```
````

```` {card} 3. Count the number of digits in n.
_Hint: You'll need to use math to do this._
``` {code-block} bash
Enter your number: 41256
Ouput : 5
```
````

```` {card} 1. Print all prime numbers between 1 and n.
``` {code-block} bash
     Enter your number: 20
     Ouput : 2 , 3 ,  5 , 7 , 11 , 13 , 17,  19
```
````

```` {card} 1. Given a number n, print a pyramid with n rows.
_Hint: You'll want to find patterns for spaces & `*`s_

``` {code-block} bash
Input: 5
Output:
    *
   ***
  *****
 *******
*********
```

### Requirements

``` {card}
1. Exercise 1 completed.
2. Exercise 2 completed.
2. Exercise 3 completed.
2. Exercise 4 completed.
5. Exercise 5 completed.
```
