layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Introduction to Computers and Programming

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---
# Hardware

.row[
.col-6[
* Hardware: The physical devices that make up a computer
    * Computer is a system composed of several components that all work together
    
    
* Typical major components:
    * Central processing unit
    * Main memory
    * Secondary storage devices
    * Input and output devices
]
.col-6[

<img src="https://upload.wikimedia.org/wikipedia/commons/d/d8/ABasicComputer.gif" width=450>
<img src="https://upload.wikimedia.org/wikipedia/en/f/fc/Intel_Core_i9-10900K.png" width=170>
<img src="https://upload.wikimedia.org/wikipedia/commons/e/e8/DDR2_ram_mounted.jpg" width=170>

]
]

---

# The CPU 

* Central processing unit (CPU): the part of the computer that actually runs programs
    * Most important component
    * Without it, cannot run software
    * Used to be a huge device


* Microprocessors: CPUs located on small chips

# Main Memory

* Main memory: where computer stores a program while program is running, and data used by the program


* Known as Random Access Memory or RAM
    * CPU is able to quickly access data in RAM
    * Volatile memory used for temporary storage while program is running
    * Contents are erased when computer is off

---

# Software

.row[
.col-8[

* Everything the computer does is controlled by software


* Application software: programs that make computer useful for every day tasks
    * Examples: word processing, email, games, and Web browsers
 
 
* System software: programs that control and manage basic operations of a computer
    * Operating system: controls operations of hardware components
    * Utility Program: performs specific task to enhance computer operation or safeguard data
    * Software development tools: used to create, modify, and test software programs


]
.col-4[

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/87/Operating_system_placement_%28software%29.svg/1280px-Operating_system_placement_%28software%29.svg.png" width=300>

]
]

---

# How Computers Store Data 

.row[
.col-8[

* All data in a computer is stored in sequences of 0s and 1s
* Byte: just enough memory to store letter or small number
    * Divided into eight bits
    * Bit: electrical component that can hold positive or negative charge, like on/off switch
    * The on/off pattern of bits in a byte represents data stored in the byte
    
    
* The decimal prefixes kilo, mega, giga, tera, etc., are powers of 10<sup>3</sup> = 1000. 
* The binary prefixes kibi, mebi, gibi, tebi, etc. are powers of 2<sup>10</sup> = 1024. 
* In casual usage, the two corresponding prefixes are considered equivalent.
   
]
.col-4[
<img src="https://user-images.githubusercontent.com/39995503/91276094-027f8180-e7bc-11ea-8214-1084ff230308.png" width=300>
https://en.wikipedia.org/wiki/Byte
]
]

---

# Storing Numbers 

* Bit represents two values, 0 and 1
* Computers use binary numbering system
    * Position of digit j is assigned the value 2<sup>j-1</sup>
    * To determine value of binary integer, sum position values of the 1s
* Byte size limits are 0 and 255
    * 0 = all bits off; 255 = all bits on
    * To store larger numbers, use several bytes


* To store negative integers and real numbers, computers use binary numbering and encoding schemes
    * Negative integers encoded using two’s complement
    * Real numbers encoded using floating-point notation
    
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Float_example.svg/1180px-Float_example.svg.png" height=70>  
        *IEEE Standard for Floating-Point Arithmetic (IEEE 754)*

---

# Storing Characters

* Data stored in computer must be stored as binary number


* Characters are converted to numeric code, numeric code stored in memory
    * Most important coding scheme is ASCII
    * ASCII is limited: defines codes for only 128 characters
    * Unicode coding scheme becoming standard
        * Compatible with ASCII
        * Can represent characters for other languages
        
---

# How a Program Works 

.row[
.col-7[

* Program must be copied from secondary memory to RAM each time CPU executes it


* CPU executes program in cycle:

    1. **Fetch**: read the next instruction from memory into CPU
    2. **Decode**: CPU decodes fetched instruction to determine which operation to perform
    3. **Execute**: perform the operation

   
]
.col-5[
<img src="https://computersciencewiki.org/images/2/24/Fetch-execute-cycle.png" width=300>
[fetch–decode–execute cycle]
https://computersciencewiki.org/
]
]

---

# From Machine Language to Assembly Language 

* Impractical for people to write in machine language (binary numbers)


* **Assembly language**: uses short words (mnemonics) for instructions instead of binary numbers
    * Easier for programmers to work with
* **Assembler**: translates assembly language to machine language for execution by CPU


* Low level programming had many issues
    * Access: learning curve was too difficult
    * Mass production: not standard, cannot be generalized to every machine
    * Programming performance issue: repetitive code/operations


* To solve these issue an abstraction was required

---

# High-Level Languages 

* Low-level language: close in nature to machine language
    * Example: assembly language
    
    
* High-Level language: allows simple creation of powerful and complex programs
    * No need to know how CPU works or write a large number of instructions
    * More intuitive to understand
    
    
            C (1972)
            C++ (1982)
            Python (1991)
            Java (1994)
            Javascript (1995)
            C# (2000)
            etc

---

# High-Level Programming Paradigms 

* Control-oriented Programming (before mid 80’s)
    * Real world problem -> a set of **functions**
    * Data and functions are separately treated
    * Fortran, Cobol, PL/1, Pascal, C (1972, Bell Lab)
    
    
* Object-oriented Programming (after mid 80’s)
    * Real world problem -> a set of **classes**
    * Data and functions are encapsulated inside classes
    * C++ (1982, Bell Lab)
    * Python (1991)
    * Java (1994)
    * and most Script Languages (Ruby, PHP, R,…)
    
---

# The C Programming Language 

.row[
.col-8[

* designed and implemented by Dennis Ritchie, 1972
* ISO/IEC: C99 (1999), C11(2011)


* Table of Contents 
    * Chapter 1. Tutorial Introduction
    * Chapter 2. Types, Operators, and Expressions
    * Chapter 3. Control Flow
    * Chapter 4. Functions and Program Structure
    * Chapter 5. Pointers and Arrays
    * Chapter 6. Structures
    * Chapter 7. Input and Output
    * Chapter 8. The UNIX System Interface
    * Appendix A. Reference Manual
    * Appendix B. Standard Library
    
]
.col-4[
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/The_C_Programming_Language%2C_First_Edition_Cover.svg/1280px-The_C_Programming_Language%2C_First_Edition_Cover.svg.png" width=170>

<img src="https://images-na.ssl-images-amazon.com/images/I/411ejyE8obL._SX377_BO1,204,203,200_.jpg" width=170>

]
]

    
---

# The C++ Programming Language

.row[
.col-6[
* created by Bjarne Stroustrup as an extension of the C programming language, or "C with Classes, 1985
* C++11 (ISO, 2011), C++14, C++17 (ISO/IEC 14882:2017)


* Table of Contents 
    * Part I: Introductory Material
    * Part II: Basic Facilities 

        <img src="https://upload.wikimedia.org/wikipedia/en/c/c7/The_C%2B%2B_Programming_Language%2C_Fourth_Edition.jpg" width=150>
]
.col-6[
<img src="https://user-images.githubusercontent.com/39995503/91307116-7e8fbe80-e7e8-11ea-93ae-b30125e00ef3.png">
]
]

---

# Most Popular Programming Languages

<img src="https://user-images.githubusercontent.com/39995503/91426723-db967d80-e897-11ea-8584-bfe8bc77ed93.png" width=600>

percentage of programmers with either proficiency in specific language or currently learning/mastering one
[https://youtu.be/Og847HVwRSI]

---

# Most Popular Programming Languages


<img src="https://upload.wikimedia.org/wikipedia/commons/6/64/Tiobe_index_2020_may.png" width=750>

the number of search engine results for queries containing the name of the language
[https://en.wikipedia.org/wiki/TIOBE_index]

---

# Programming Languages

* In early 1990’s, C++ was the most popular language.
    * Computers were slow at the time
    * Java requires a lot of resource, so it was slow


* In early 2000’s, Java was the most with rapid increase in computer hardware


* Around 2010, Python became the most popular
    * It is easy to learn
    * Has a lot of features (“batteries included” philosophy)
    * Has most support for Machine Learning & AI
---

# Programming Languages

* How to print "Hello World!" in different languages

.row[
.col-5[
```c
/* C */
#include <stdio.h>
int main()
{
    printf("Hello, World!\n");
    return 0;
}
```

```python
# Python
print("Hello, World!")
```

]
.col-7[

```c
// C++
#include <iostream>
using namespace std;
    
int main()
{
    cout << "Hello, World! << endl;
    return 0;
}
```

```java
// Java
class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```   

]
]

---

# Compilers and Interpreters

* Programs written in high-level languages must be translated into machine language to be executed


* **Compiler**: translates high-level language program into separate machine language program
    * Machine language program can be executed at any time
    
    
* **Interpreter**: translates and executes instructions in high-level language program
    * Used by Python language
    * Interprets one instruction at a time
    * without requiring codes previously to have been compiled into a machine language program


---

# Using Python

* Python Interpreter
    * Translate source code into some efficient intermediate representation and immediately execute this
    * **souce code(.py)** -> **byte code(.pyc)** -> **PVM(Python Virual Machine; Python Interpreter)**
 
 
* Python must be installed and configured prior to use
    * One of the items installed is the Python interpreter


* Python interpreter can be used in two modes:
    * **Interactive mode**: enter statements on keyboard
    * **Script mode**: save statements in Python script

---

# Interactive Mode

* When you start Python in interactive mode, you will see a prompt
    * Indicates the interpreter is waiting for a Python statement to be typed
    * Prompt reappears after previous statement is executed
    * Error message displayed if you incorrectly type a statement
 

* Good way to learn new parts of Python


# Script Mode

* Statements entered in interactive mode are not saved as a program


* To have a program use script mode
    * Save a set of Python statements in a file
    * The filename should have the .py extension
    * To run the file, or script, type the following at the operating system command line:
    
    
            python filename 
	
---

# IDE 

* Integrated Development Environment
* a software that provides tools to write, execute and test a program

    
* IDLE(Integrated Development and Learning Environment)
    * Automatically installed when Python language is installed
    * Runs in the interactive mode
    * Has a built-in text editor with features designed to help write Python programs

    <img src="https://user-images.githubusercontent.com/39995503/91443546-700bda80-e8ae-11ea-8c89-5b7683d13c8e.png" width=700>

---

# Acknowledgement

* Professor Hyung-Joo Kim
* Professor Tony Gaddis and Pearson Education, Ltd.
