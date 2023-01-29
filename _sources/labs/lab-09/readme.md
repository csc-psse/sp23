# Lab 9 :  File Input/ Output in C++

Welcome to the seven session of  CSC 200 lab! This will familiarize you with reading a file or writing in a file as well as give you some experience in their proper use. **Be sure to read and follow all instructions unless otherwise specified.**  You'll find the table of contents for this lab below.

## Part 1. Writing/Reading a file in C++

C++ provides the following classes to perform output and input of characters to/from files: 

``` {card}
`ofstream`
: Stream class to write on files

`ifstream`
: Stream class to read from files

`fstream`
: Stream class to both read and write from/to files.
```

These classes are derived directly or indirectly from the classes `istream` and `ostream`. We have already used objects whose types were these classes: `cin` is an object of class `istream` and `cout` is an object of class `ostream`. Therefore, we have already been using classes that are related to our file streams. And in fact, we can use our file streams the same way we are already used to use `cin` and `cout`, with the only difference that we have to associate these streams with physical files. Let's see an example:



**Example : writing in a file**

``` {code-block} cpp
// basic file operations
#include <iostream>
#include <fstream>

int main () {
  ofstream myfile;
  myfile.open ("example.txt");
  myfile << "Writing this to a file.\n";
  myfile.close();
  return 0;
}
```

```` {card} example.txt
``` {code-block} bash
Writing this to a file.
```
````

This code creates a file called `example.txt` and inserts a sentence into it in the same way we are used to do with `cout`, but using the file stream `myfile` instead.

But let's go step by step:

### Open a file

The first operation generally performed on an object of one of these classes is to associate it to a real file. This procedure is known as to ***open a file***. An open file is represented within a program by a *stream* (i.e., an object of one of these classes; in the previous example, this was `myfile`) and any input or output operation performed on this stream object will be applied to the physical file associated to it.

In order to open a file with a stream object we use its member function `open`:

`open (filename, mode);`
Where `filename` is a string representing the name of the file to be opened, and `mode` is an optional parameter with a combination of the following flags:

| `ios::in`     | Open for input operations.                                   |
| :------------ | :----------------------------------------------------------- |
| `ios::out`    | Open for output operations.                                  |
| `ios::binary` | Open in binary mode.                                         |
| `ios::ate`    | Set the initial position at the end of the file. If this flag is not set, the initial position is the beginning of the file. |
| `ios::app`    | All output operations are performed at the end of the file, appending the content to the current content of the file. |
| `ios::trunc`  | If the file is opened for output operations and it already existed, its previous content is deleted and replaced by the new one. |

All these flags can be combined using the bitwise operator OR (`|`). For example, if we want to open the file `example.bin` in binary mode to add data we could do it by the following call to member function `open`:

``` {code-block} cpp
ofstream myfile;
myfile.open ("example.bin", ios::out | ios::app | ios::binary);
```

​Each of the `open` member functions of classes `ofstream`, `ifstream` and `fstream` has a default mode 		that is used if the 		file is opened without a second argument: 

| class      | default mode parameter |
| ---------- | ---------------------- |
| `ofstream` | ios::out               |
| `ifstream` | ios::in                |
| `fstream`  | ios::in \| ios::out    |

1.  For `ifstream` and `ofstream` classes, `ios::in` and `ios::out` are automatically and respectively assumed, even if a mode that does not include them is passed as second argument to the `open` member function (the flags are combined).
2. For `fstream`, the default value is only applied if the function is called without specifying any value for the mode parameter. If the function is called with any value in that parameter the default mode is overridden, not combined.
3. File streams opened in *binary mode* perform input and output operations independently of any format considerations. Non-binary files are known as *text files*, and some translations may occur due to formatting of some special characters (like newline and carriage return characters).

Since the first task that is performed on a file stream is generally to open a file, these three classes include a constructor that automatically calls the `open` member function and has the exact same parameters as this member. Therefore, we could also have declared the previous `myfile` object and conduct the same opening operation in our previous example by writing:

``` {code-block} cpp
ofstream myfile ("example.bin", ios::out | ios::app | ios::binary);
```

Combining object construction and stream opening in a single statement. Both forms to open a file are valid and equivalent.

To check if a file stream was successful opening a file, you can do it by calling to member `is_open`. This member function returns a `bool` value of `true` in the case that indeed the stream object is associated with an open file, or `false`otherwise:

``` {code-block} cpp
if (myfile.is_open()) { /* ok, proceed with output */ }
```

### Closing a file

When we are finished with our input and output operations on a file we shall close it so that the operating system is notified and its resources become available again. For that, we call the stream's member function `close`. This member function takes flushes the associated buffers and closes the file:

``` {code-block} cpp
myfile.close();
```

Once this member function is called, the stream object can be re-used to open another file, and the file is available again to be opened by other processes.

In case that an object is destroyed while still associated with an open file, the destructor automatically calls the member function `close`.

### Text Files

Text file streams are those where the `ios::binary` flag is not included in their opening mode. These files are designed to store text and thus all values that are input or output from/to them can suffer some formatting transformations, which do not necessarily correspond to their literal binary value.

Writing operations on text files are performed in the same way we operated with `cout`:

``` {code-block} cpp
// writing on a text file
#include <iostream>
#include <fstream>

int main () {
  ofstream myfile ("example.txt");
  if (myfile.is_open())
  {
    myfile << "This is a line.\n";
    myfile << "This is another line.\n";
    myfile.close();
  }
  else std::cout << "Unable to open file";
  return 0;
}
```

``` {code-block} bash
[file example.txt]
This is a line.
This is another line.
```



Reading from a file can also be performed in the same way that we did with `cin`:

``` {code-block} cpp
// reading a text file
#include <iostream>
#include <fstream>
#include <string>

int main () {
  string line;
  ifstream myfile ("example.txt");
  if (myfile.is_open())
  {
    while ( getline (myfile,line) )
    {
      std::cout << line << '\n';
    }
    myfile.close();
  }

  else std::cout << "Unable to open file"; 

  return 0;
}
```

```
This is a line.
This is another line. 
```

This last example reads a text file and prints out its content on the screen. We have created a while loop that reads the file line by line, using [getline](https://www.cplusplus.com/getline). The value returned by [getline](https://www.cplusplus.com/getline) is a reference to the stream object itself, which when evaluated as a boolean expression (as in this while-loop) is `true` if the stream is ready for more operations, and `false`if either the end of the file has been reached or if some other error occurred.



## Part 2. Exercises

```` {card} 1. Write a function
... to get the size of the pyramid and print hollow star pyramid in a diamond pattern in a file. 

``` {code-block} bash
Input : 6
      *
     * *
    *   *
   *     *
  *       *
 *         *
*           *
 *         *
  *       *
   *     *
    *   *
     * *
      *
````

``` {card} 1. Write a function
...that reads an array from a file and finds the contiguous subarray (containing at least one number) which has the largest sum and return *its sum*.
   
A **subarray** is a **contiguous** part of an array.

Example 1:

``` {code-block} bash
Example 1 :
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
__________________________________________________ 
  
Example 2:
Input: nums = [1]
Output: 1
___________________________________________________ 

Example 3 :
Input: nums = [5,4,-1,7,8]
Output: 23
```

### Requirements

``` {card}
1. Exercise 1 completed.
2. Exercise 2 completed.
```
