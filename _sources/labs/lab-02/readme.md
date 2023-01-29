# Lab 2 :  IDE Setup & Introduction

Your goal for this lab will be to complete any set up of your environment and familiarize yourself with some basic terminal commands. **Be sure to read and follow all instructions unless otherwise specified.**  You'll find the table of contents for this lab below.

## Part 1. Introduction

Hopefully you have chosen your C++ IDE for use throughout the semester, have it setup, and are ready to program.

``` {card} Suggestions:

- Windows
  - Visual Studio
  - VS Code
- Linux
  - Geany
- Mac OS
  - XCode
  - VS Code
- Online
  - [CS50 IDE](https://ide.cs50.io/)

In lieu of an IDE, feel free to simply use a text editor (I recommend Notepad++ or Sublime) & the terminal commands we'll be covering today.
```

The next section will deal with Unix commands, as Unix is a common environment for C++ development. For those of you in a Windows environment, you can install the [Windows Subsystem for Linux](https://itsfoss.com/install-bash-on-windows/) and gain access to a Unix Shell.

## Part 2. Basic Unix Command-Line Exploration

Now that you've set up your environment, we can start to learn some basic UNIX command line. Unix and [Unix-like operating systems](http://www.doc.ic.ac.uk/~wjk/unixintro/Lecture1.html), like Linux, can all use the following commands to interact with [file systems](http://homepages.uc.edu/~thomam/Intro_Unix_Text/File_System.html). Basic tasks like changing directories, creating or modifying files, or removing files all together are just a few examples of things we can do using a Shell terminal.

To really understand what you'll be doing for this section of the lab, having a strong understanding of what a file system is and how we can navigate it will be critically important.

### Opening a New Terminal

CS50: If you don't have a terminal already open in your environment, you can create one in the the CS50 IDE by clicking File > New Terminal.

Mac OS: Run the 'Terminal' program

Windows: If you followed the above steps to install the 'Windows Subsystem for Linux' then run the 'Ubuntu' program to open a terminal.

### Making a file

We can  make empty files on the fly with the `touch <filename>` command. Try the following below: 

``` {code-block} bash
$ touch test.cpp
```

Now, you should see `test.cpp` in your file manager on the left-hand side.

#### Removing files

Before your workspace gets too cluttered, let's remove that test file you just created with the `touch` command. You can do this by typing:

``` {code-block} bash
$ rm test.cpp
```

The test file you just created should be removed if this command ran properly.

Ok, lets create another empty file with the following command:

``` {code-block} bash
$ touch hello.cpp
```

#### Creating a new directory

Making and deleting files is great but we often need to organize them in a sensible way. We usually do this by making **directories**. You can think of directories as folders. They're named locations that can hold other files or directories.

To make a directory type the following terminal command:

``` {code-block} bash
$ mkdir projects
```

Now you should see your `hello.cpp` and `projects` folder in your file manager.

### Removing a directory

Just like how we created and removed a file, we can do the same with directories. Lets make a test directory named `testd` with the following command:

``` {code-block} bash
$ mkdir testd
```

To delete this directory (only if is empty), we can simply run:

``` {code-block} bash
$ rmdir testd
```

### Moving files

Lets clean up our workspace by moving that `hello.cpp` file into our projects folder.  The syntax to move one file from one location to another location is `mv <source> <target>`. In this case, it would be:

``` {code-block} bash
$ mv hello.cpp projects
```

Now, our `hello.cpp` file is in our `projects` directory.

### Print Working Directory

To see where we are, the command `pwd` will print the current directory you are operating in to the command line. Currently, running the command

``` {code-block} bash
$ pwd
```

If you are running on 'Ubuntu', it should print out `/home/ubuntu`, if at any point you changed directory with the following command your output will be different. The output of this line will differ based on your environment.

### Change Directory

Now that we have made a new directory named `projects` and moved our `hello.cpp` file to it, we need to navigate our terminal to this directory in order to have easy access to our file for editing/compiling/file management. This is accomplished with the `cd` command with syntax as follows, `cd <directory_path>`, meaning we can move more than one file at a time. For now the following command should get you to where you need to be,

```  {code-block} bash
$ cd projects/
```

Now that we have changed directory, we can execute the earlier commands to validate our position within the file system. Executing `pwd` from this file should output `/home/ubuntu/projects` (again, assuming you are running on 'Ubuntu') and executing `ls` should show that there is a file named `hello.cpp` present.

Some useful cd commands:
```  {code-block} bash
#### to change your working directory to its parent directory, i.e. one step back
$ cd ..
#### to change back to your user directory, i.e. "/home/ubuntu" or "~/" in the case of CS50 IDE's file system
$ cd
#### to change back to the file system root directory, i.e. "/" for short
$ cd /
```

> Note that `cd` can accept full paths, so for example `cd ../..` will move your working directory two steps back in the file system, though **don't do this now** as this will put you behind your root directory which is out of the scope of this lab

### Displaying File Contents

Another (popular) command-line utility available to us is `cat`, which is short for concatenate. In its simplest form, `cat` can display the contents of a text file; it can also be used to concatenate together many text files.

For example, if we had a text document named `test.txt` with the contents 

```text
I love CSC 200
```

The contents of that file would print out to our terminal by running:

```  {code-block} bash
$ cat test.txt
```

Spend some time to create a text file with some content in it and use the `cat` command to report those contents to the console.

### Shell Hints

Before we move on, there are a few things about the shell you should know. The up arrow goes to previous commands. And if you think the computer can guess what you are typing, you can hit TAB to have it completed for you. For example, if `cd pro` is typed in terminal, and the TAB key is hit, the rest of the file name will be filled in. You can find more information on terminal commands [here](http://mally.stanford.edu/~sr/computing/basic-unix.html).

## Part 3. Command-Line Arguments

It is often helpful for us to specify how a program will run by providing arguments during the execution process. For example, normally compiling a program and running may look like this:

```  {code-block} bash
g++ main.cpp -o prog && ./prog
```

But if we wanted the execution of our program to change based on some variable (number of loops, size of a data structure, etc.) we can provide an argument here like so:

```  {code-block} bash
g++ main.cpp -o prog && ./prog 5
```

Or even multiple arguments

```  {code-block} bash
g++ main.cpp -o prog && ./prog 5 3 6 local
```

Our code would look like so:

```  {code-block} cpp
int main (int argc, char*argv[]) {
    // do something...
}
```

``` {card} C++ String resources

- https://www.tutorialspoint.com/cplusplus/cpp_strings.htm
- https://www.youtube.com/watch?v=h2LGTzQXzJU
- https://eecs280staff.github.io/notes/05_Strings_Streams_IO.html#c-style-strings
- https://www.cprogramming.com/tutorial/lesson9.html

```

Where `argc` stands for the number of arguments passed (including the command to run the program!) and `argv` holds those arguments. Note the type! They will all be treated as char arrays or C-Style strings. You will need to convert them if you want to use them as different types (int, float, etc.) Using the last argument example, this is how we would extract them:

```  {code-block} cpp
#include <string> // string, stoi (string to integer)
int main(int argc, char*argv[]){
    int num1 = std::stoi(argv[1]); // extracts the 5
    int num2 = std::stoi(argv[2]); // extracts the 3
    int num3 = std::stoi(argv[3]); // extracts the 6
    std::string str(argv[4]); // converts the C-Style string to a C++ String Object
}
```

Additional reading can be found in [this tutorial](https://www.geeksforgeeks.org/command-line-arguments-in-c-cpp/)

## Part 4. Proper Programming Practices 

There are many ways to solve a problem. This too holds true for programming; there are multiple ways to code a solution to a problem. This section will go over a few tried-and-true rules to live by in order to create code that won't get you banished from polite society.

### Plan before you code!

A common trap students fall into is programming as they solve a problem; this has a tendency to spiral out of control into an unsalvageable mess that ends in a waste of time. Take the time to plan your solution BEFORE you even touch code. What functions, and variables, you'll need, the flow of your program, etc. I **guarantee** that the time spent planning before hand will more than makeup for the time you'd waste backtracking & re-writing code otherwise.

### K.I.S.S (Keep it Simple, Stupid!)

Your code will not be efficient if you do not first solve the underlying problem in a simple manner. Over-complication is common in these early programming courses; don't be afraid to reach out to staff and ask for feedback on your strategy! [You can read more about this amazing principle here](https://www.interaction-design.org/literature/article/kiss-keep-it-simple-stupid-a-design-principle)

### Naming Conventions

This is a [good reference page](https://google.github.io/styleguide/cppguide.html) for writing "proper" C++ code. 

On top of following the guidelines here, make sure to give your functions & variables **clear, proper** names! When you ask the staff for help its *incredibly* unhelpful (and time consuming) to attempt and parse hundreds of lines of code that look like ` int a;`

### Functions

- Follow the "Rule of Three"
  - If you have a piece of code that is replicated (read: copy & pasted) more than twice, this task should be a function.
- Any section of code that performs a specific task in your program should be a function. Some examples:
  - Reading from a file
  - Writing to a file
  - Performing calculations on an array

### Variables

Don't be afraid to create variables to improve code clarity! As mentioned before, name them appropriately!

### Ninety-ninety rule

This is a fantastic quote that really captures the main pitfalls many of you will fall into:

``` {epigraph}
"The first 90 percent of the code accounts for the first 90 percent of the development time. The remaining 10 percent of the code accounts for the other 90 percent of the development time."

-— Tom Cargill, Bell Labs
```

To clarify, software has a tendency to take longer than anticipated to finish. **Start your assignments early!**

### Chasing false efficiency

While I (Christian) am a huge proponent of writing efficient code, it is important to realize that not everything needs to be coded in the most efficient manner. Often times code clarity/development speed take a higher priority. As an example: if it takes 5 minutes to code a function that runs once in 0.005 seconds, is it really worth spending an hour to get that same function to run in 0.002 seconds? Probably not. A solid rule of thumb while you're learning is to get something that **works** first, **then** worry about efficiency to improve your skill afterwards.

### Avoid Hard-coding!

You should **always** use variables to represent values in your code. This makes your code easier to modify later on if needed & adds clarity to your code.

As an example:

````` {grid}
```` {grid-item-card} Bad
:columns: 6
```  {code-block} cpp
// Bad
for(int i = 0; i < 5; i++){
    // Do stuff
}
```
````
```` {grid-item-card} Good
:columns: 6
```  {code-block} cpp
// Good
unsigned int num_rows = 5;
for(int i = 0; i < num_rows; i++){
    // Do stuff
}
```
````
`````

## Part 5. Debugging

The hardest part of programming is figuring out where you went wrong. There are a few techniques we can use to narrow in on our mistakes:

``` {card} Rubber-duck debugging
Often we just need to methodically work through the code. Unfortunately, we tend to make assumptions while reviewing code that we wrote. In an effort to prevent glossing over key portions, the goal of this type of debugging is to explain the code to someone as if they had never seen it before. Since it can be difficult to find someone to speak to every time you get stuck (hint: a lot) it is helpful to substitute in a rubber duck. Yes, the generic kind you find in/around bath tubs. Here is a bit more reading on the subject (I recommend giving this a quick read!) https://www.thoughtfulcode.com/rubber-duck-debugging-psychology/
```

``` {card} Print Statements
Sometimes we just need to output everything our program is doing to track down the issue. This is *very* primitive, and does not scale well. But in an isolated environment is a quick and dirty way to discover where a calculation is going wrong. Bonus tip: Read input from the keyboard to "pause" your program and step through it slowly!
```

``` {card} Use a real debugger
This is the proper way to perform technique #2. Set breakpoints accordingly, compile your code, run it through a debugger, and use the tools given to you to explore the values in all of the variables, check scope, trace the program control, etc. This process will differ based on the IDE you are using, lookup tutorials and reach out to staff for help.
```

## Part 6. Exercise

Use what you learned in this lab (and Brightspace!) to complete the following exercises:

```` {card} 1. Create a new .cpp file, copy the following code into your IDE, fix the mistakes, and get it to compile & run.
```c++
// A mixed up program

// TODO: Place your name here

int main()
{
#include <iostream>
return 0;
std::cout << "Dogs are awesome.";
}

```
````

```` {card} 2. Create a new $.cpp$ file, copy the following code into your IDE, and complete the instructions in the $TODO$

```  {code-block} cpp
/* This program takes two values from the user and then swaps them
	before printing the values.  The user will be prompted to enter
	both numbers. */

// TODO: Place your name here

#include <iostream>

int main()

{
	
	float firstNumber;
	float secondNumber;
	
	// Prompt user to enter the first number.
	
	std::cout << "Enter the first number" << std::endl;
	std::cout << "Then hit enter" << std::endl;
	std::cin  >> firstNumber;
	
	// Promt user to enter the second number.
	
	std::cout << "Enter the second number" << std::endl;
	std::cout << "Then hit enter" << std::endl;
	std::cin  >> secondNumber;
	
	// Echo print the input.
	
	std::cout << std::endl << "You input the numbers as " << firstNumber
		 << " and " << secondNumber << std::endl;
	
    /* TODO: Write the code to swap the values of the two variables, 
    	firstNumber and secondNumber.
     DO NOT modify any of the code I've given you */

    
	// Output the values.
	
	std::cout << "After swapping, the values of the two numbers are "
	     << firstNumber << " and " << secondNumber << std::endl;
	
	return 0;
	
}
```
````

```` {card} 3. Follow the directions below to create a new program.

Write a program that converts and prints a user-supplied measurement in inches into:
: a. foot (12 inches)
: b. yard (36 inches)
: c. centimeter (2.54/inch)
: d. meter (39.37 inches)

Your program's input/output should look something like this (note: 24 is supplied by the user!):

``` {code-block} bash
Enter your measurement in inches: 24
24 inches is equal to:
2 feet
0.66 yards
60.96 centimeters
0.609 meters
```
````

### Requirements

``` {card}
1. Exercise 1 ordering fixed, compiles and runs correctly.
2. Exercise 2 values are swapped, compiles, and runs correctly.
3. Exercise 3 implemented to specification, compiles, and runs correctly..
```
