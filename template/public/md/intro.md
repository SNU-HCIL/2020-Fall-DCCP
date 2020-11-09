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

* All data in a computer is stored in sequences of `0`'s and `1`'s
* `Byte`: just enough memory to store a letter or a small number
   * Divided into .red[eight] bits
   * `Bit`: electrical component that can hold positive or negative charge, like on/off switch
   * The on/off pattern of bits in a byte represents data stored in the byte
    
    
* The decimal prefixes `kilo`, `mega`, `giga`, `tera`, etc., are powers of 10<sup>3</sup> = 1000. 
* The binary prefixes `kibi`, `mebi`, `gibi`, `tebi`, etc. are powers of 2<sup>10</sup> = 1024. 
* In casual usage, the two corresponding prefixes are considered equivalent.
   
]
.col-4[
<img src="https://user-images.githubusercontent.com/39995503/91276094-027f8180-e7bc-11ea-8214-1084ff230308.png" width=300>
https://en.wikipedia.org/wiki/Byte
]
]

---

# Storing Numbers 

* Bit (BInary digiT) represents one of the two values, `0` and `1`
* Computers use binary numbering system
   * Position of digit `j` is assigned the value 2<sup>`j-1`</sup>
   * To determine value of binary integer, sum position values of the 1s
* Byte size (8 bits) limits are `0` and `255`
   * `0` = all bits off; `255` = all bits on
   * To store larger numbers, use several bytes


* To store negative integers and real numbers, computers use binary numbering and encoding schemes
   * Negative integers encoded using .red[two’s complement]
   * Real numbers encoded using floating-point notation (double precision in Python)
       
.center[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a9/IEEE_754_Double_Floating_Point_Format.svg/618px-IEEE_754_Double_Floating_Point_Format.svg.png" height=100>]
    
.center[IEEE Standard for Floating-Point Arithmetic (IEEE 754)]

---

# Storing Integers (Signed Number Representation)

* Sign-magnitude Representation
    
     
* `1`'s Complement Representation
    
    
* `2`'s Complement Representation
        
---

# Sign-magnitude Representation

<img src="https://user-images.githubusercontent.com/39995503/92318238-353f3a80-f044-11ea-94e7-5a7ccaa26a44.png" height=150>
    
* Early computers used this represenation; e.g., IBM7090 (1959)


* two ways to represent zero, `00000000 (+0)` and `10000000 (-0)`
* addition and subtraction have to be implemented differently depending on the sign bit
* comparison requires sign bit inspection
* the minimum negative number is `-127`

---

# `1`'s Complement Representation

* `1`'s complement (c) of a binary number (b): b + c = 1


* Use `1`'s complement to represent a negative number


* Many early computers used ones' complement notation; e.g., CDC 6600 (1965), the LINC, the PDP-1, and the UNIVAC 1107 

* Positive numbers are represented in the same way as sign-magnitude representation
* Negative numbers are represented by taking `1`'s complement of the unsigned positive number
    * leftmost bit continues to function as a sign bit  
    <img src="https://user-images.githubusercontent.com/39995503/92318520-7afe0200-f048-11ea-8425-59d00fac8b38.png" height=100>

---

# `1`'s Complement Representation        


```
          binary    decimal
        11111100     −3
     +  11111011     −4
     ─────────     ──
      1 11110111     −8   ← Not the correct answer
               1     +1   ← Add end-around carry
     ─────────     ──
        11111000     −7   ← Correct answer
```

* two ways to represent zero, `00000000 (+0)` and `11111111 (-0)`
* the minimum negative number is `-127`

---

# `2`'s Complement Representation

* `2`'s complement (c) of a binary number (b): b + c = 2
    * `2`'s complement: (`1`'s complement) + 1


* Use `2`'s complement to represent a negative number


* Most commonly used computer representation for integers


* Positive numbers are represented in the same way as sign-magnitude representation
* Negative numbers are represented by taking `2`'s complement of the unsigned positive number
    * leftmost bit continues to function as a sign bit  
    <img src="https://user-images.githubusercontent.com/39995503/92318532-8f41ff00-f048-11ea-877c-06c21eb04b7f.png" height=100>

---
# `2`'s Complement Representation

```
          binary    decimal
        11111101     −3
     +  11111100     −4
     ────────      ──
      1 11111001     −7   ← Correct answer
                          ← Ignore end-around carry

```


* only one way to represent zero, `00000000`
* the minimum negative number is `-128`

---
# Python's Integer Representaion

* All integers are implemented as “long” integer objects of .red[arbitrary] size.


* In languages like C/C++, the precision of integers is limited to 64-bit
* but Python has built-in support for .red[arbitrary-precision] integers.

* PyLongObject: a subtype of PyObject represents a Python integer object.

```c
struct {
    ssize_t ob_refcnt;
    struct _typeobject *ob_type;
    ssize_t ob_size; 
    uint32_t ob_digit[1];
};
```

* Example: source: <a href="https://rushter.com/blog/python-integer-implementation/" target="_blank"> https://rushter.com/blog/python-integer-implementation/</a>

<span style="font-family:courier;font-size:0.9em">
123456789101112131415 = 437976919∗2<sup>30\*0</sup> + 87719511\*2<sup>30\*1</sup> + 107\*2<sup>30\*2</sup>
</span>

```
ob_size    3
ob_digit   437976919 | 87719511 | 107
```


---
# Floating-point Representation for Real Numbers
```
0.1101 x 2^5 = 1.1010 x 2^4 
             = 11.010 x 2^3
             ≈ 0.0110 x 2^6
             ≈ 0.0011 x 2^7
```

---
# IEEE 754 Standard Formats


* Single Precision  
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Float_example.svg/590px-Float_example.svg.png" height=60>

* The real value of a single precision folating-point number is
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/5858d28deea4237a7c1320f7e649fb104aecb0e5">  
which yields  
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/15f92e12d6d0a7c02be4f12c83007940c432ba87">


* Double Precision (Python)  
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a9/IEEE_754_Double_Floating_Point_Format.svg/618px-IEEE_754_Double_Floating_Point_Format.svg.png" height=100>

source: [https://en.wikipedia.org/wiki/Single-precision_floating-point_format]

---
# IEEE 754 Standard Formats

  
<img src="https://user-images.githubusercontent.com/39995503/92426721-9c382d00-f1c5-11ea-841e-055e90b8792f.png" width=500>


* .red[Sign bit]: The sign is stored in the first bit of the word.
* .purple[Normalized] .red[significand]
   * The first bit of the true significand is always `1` and need not be stored in the significand field. 
   * (-1)^s x .red[1].bbb…b x 2^±E
* .purple[Biased] .red[exponent]
   * `127` is added to the true exponent to be stored in the exponent filed. 
   * 0 ~ 255    ->   -127 ~ +128
   * Exponents range from .red[−126 to +127] because exponents of `−127` (all `0`'s) and `+128` (all `1`'s) are reserved for special numbers

---
# Expressible (Normalized) Numbers in 32-bit Formats

.center[<img src="https://user-images.githubusercontent.com/39995503/92390002-12507b80-f155-11ea-9646-cd34aea1894f.png" width=700>]

---
# Five Groups of Floating Point Numbers

.center[<img src="https://user-images.githubusercontent.com/39995503/92390825-95260600-f156-11ea-9aa8-f3ec1695bcb1.png" width=700>]

* Extreme exponent values (`0` and `255`): used to indicate special values
* `NaN`(Not a Number) is used to signal exception conditions

---
```
(largest normal number)
0 11111110 111111111111111111111112 = 2^127 × (2 − 2^−23) 
≈ 3.4028234664 × 10^38

(smallest positive normal number)
0 00000001 000000000000000000000002 = 2^−126 ≈ 1.1754943508 × 10^−38
                                                   
(one)
0 01111111 000000000000000000000002 = 1 

(largest subnormal number)
0 00000000 111111111111111111111112 = 2^−126 × (1 − 2^−23) 
≈ 1.1754942107 ×10−38

(smallest positive subnormal number)
0 00000000 000000000000000000000012 = 2^−126 × 2^−23 = 2^−149 
≈ 1.4012984643 × 10−45                                                   
```

Source: [https://en.wikipedia.org/wiki/Single-precision_floating-point_format]

---

# Storing Characters

* Data stored in computer must be stored as binary number


* Characters are converted to numeric code, numeric code stored in memory
    * Most important coding scheme is ASCII
    * ASCII is limited: defines codes for only 128 characters
    * Unicode coding scheme became standard
       * Compatible with ASCII
       * Can represent characters for other languages
 
---

# ASCII Character Set

* US-ASCII
* American Standard Code for Information Interchange
* Character encoding standard for electronic communication


.center[<img src="https://user-images.githubusercontent.com/39995503/92238226-b3d89280-eef3-11ea-9976-a06837ba00f2.png" width=600>]

.center[https://en.wikipedia.org/wiki/ASCII]
 
---

# UTF-8

* Unicode (or Universal Coded Character Set) Transformation Format – 8-bit
* Used by approximately 95% of all web pages
* Encode all 1,112,064 valid character code points in Unicode using one to four byte (8-bit) code units
    * If the code point is < 128, it’s represented by the corresponding byte value.
    * If the code point is >= 128, it’s turned into a sequence of two, three, or four bytes, where each byte of the sequence is between 128 and 255.
* Backward compatibility with ASCII
    * the first 128 characters of Unicode are encoded using a single byte with the same binary value as ASCII
   


.center[<img src="https://user-images.githubusercontent.com/39995503/92293528-3cd8e380-ef5f-11ea-8c5c-241ff54e083e.png" width=500>]

---

# Python's Unicode Support

* The default encoding for Python source code is .red[UTF-8]
* Any string created using "unicode rocks!", 'unicode rocks!', or the triple-quoted string syntax is stored as Unicode
* Python 3 also supports using Unicode characters in identifiers

```python3
>>> ord("한")    # convert a one-character Unicode string to a code point value
54620
>>> chr(54620)  # assemble strings using chr()
'한'
>>> 합계 = 10
>>> 합계 = 합계+20
>>> print(합계)
30
>>> 
```

* Python interpreter looks for `coding: name` or `coding=name` in the comment

```python3
#!/usr/bin/env python
# -*- coding: latin-1 -*-
```               
               
---

# How a Program Works 

.row[
.col-7[

* Program must be copied from secondary memory to RAM each time CPU executes it


* CPU executes program in cycle:

   1. .red[Fetch]: read the next instruction from memory into CPU
   2. .red[Decode]: CPU decodes fetched instruction to determine which operation to perform
   3. .red[Execute]: perform the operation

   
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


* .red[Assembly language]: uses short words (mnemonics) for instructions instead of binary numbers
    * Easier for programmers to work with
* .red[Assembler]: translates assembly language to machine language for execution by CPU


* Low level programming had many issues
    * Access: too difficult to learn 
    * Mass production: not standard, cannot be generalized to every machine
    * Programming performance issue: repetitive code/operations


* To solve these issue an `abstraction` was required

---

# "Hello, world!" in Assembly Language 

* x86 assembly language (DOS in MASM style assembly)

```assembler
.model small
.stack 100h

.data
msg	db	'Hello, world!$'

.code
start:
	mov	ah, 09h   ; Display the message
	lea	dx, msg
	int	21h
	mov	ax, 4C00h  ; Terminate the executable
	int	21h

end start
```
source:[https://en.wikipedia.org/wiki/X86_assembly_language]

---

# High-Level Languages 

* Low-level language: close in nature to machine language
    * Example: assembly language
    
    
* High-Level language: allows simple creation of powerful and complex programs
    * No need to know how CPU works or write a large number of instructions
    * More `intuitive` to understand
    
    
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
   * Real world problem -> a set of .red[functions]
   * Data and functions are separately treated
   * Fortran, Cobol, PL/1, Pascal, C (1972, Bell Lab)
    
    
* Object-oriented Programming (after mid 80’s)
   * Real world problem -> a set of .red[classes]
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

* How to print "Hello, World!" in different languages

.row[
.col-5[

```python
# Python
print("Hello, World!")
```

```c
/* C */
#include <stdio.h>
int main()
{
    printf("Hello, World!\n");
    return 0;
}
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
# Turing Completeness

* A programming language is .red[Turing complete] if it can be used to simulate a Universal Turing Machine 
   * a hypothetical computing device with an unbounded memory (tape) on which one could write `0`'s and `1`'s, and some very premitive instructions for moving, reading, and writing to the memory.
   * fixed-program computer vs. .red[stored-program computer]


* All modern programming languages are Turing complete.
    * Anything that can be programmed in one programming language (e.g., C++) can be programmed in any other programming language (e.g., Python).
    
    
* If a function is .red[computable], a Turing Machine can be programmed to compute it. (Church-Turing Thesis)
   * Turing discovered in the 1930’s that there are problems .red[unsolvable] by any algorithm -> .red[uncomputable]
   * e.g., .red[Halting problem]: 
        * Given an arbitrary algorithm and its input, will that algorithm eventually halt, or will it continue forever in an infinite loop?



    
---

# Programming Lanugage

* Each progamming language has:
   * primitive constructs: literals (numbers andd strings), operators
   * .red[syntax]: defines which strings of characters and symbos are well-formed
       * syntax error: He cats loves.
   * .red[static semantics]: define which syntactically valid strings have a meaning
       * static semantics error: He run quickly.
   * .red[semantics]: associates a meaning with each syntactically correct string that has no static semantic errors
       * If a program has no syntactic errors and no static semantic errors, it has semantics.
       * sematics error: He runs quickly. (But I wanted to write "She runs quickly.")

---

# Compilers and Interpreters

* Programs written in high-level languages must be translated into machine language to be executed


* .red[Compiler]: translates high-level language program into separate machine language program
    * Machine language program can be executed at any time
    
    
* .red[Interpreter]: translates and executes instructions in high-level language program
    * Used by Python language
    * Interprets one instruction at a time
    * without requiring codes previously to have been compiled into a machine language program

---

# Why Python

* General purpose , High level, Scripting Language


* First appeared 1991 , invented by Guido van Rossum


* Easy to use, easy to learn


* Widely used as
    * Scientific libraries
    * Web Frameworks
    * Backend Frameworks
    * UI Frameworks
    * Graphic Frameworks
    * Data Mining Frameworks
    * And many others…

---

# Why Python: Advantages vs Disadvantages

* Advantages
    * Fast prototype testing
    * Minimal development effort
    * High readability


* Disadvantages
    * As a scripting language, it requires a interpreter
    * Performance might be an issue (memory, computation)
    * Weak typing might be harder to debug (weak static semantics checking)
        * Not optimal for programs that have high reliability constraints
        * Not optimal for programs that are built and maintained by many people or over a long period of time

---

# Using Python

* Python Interpreter
   * Translate source code into some efficient intermediate representation and immediately execute this
   * .red[souce code(.py)] -> .red[byte code(.pyc)] -> .red[PVM(Python Virual Machine; Python Interpreter)]
 
 
* Python must be installed and configured prior to use
   * One of the items installed is the Python interpreter


* Python interpreter can be used in two modes:
   * .red[Interactive mode]: enter statements on keyboard
   * .red[Script mode]: save statements in Python script

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
    
    
```
python filename 
```
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

# Simple Output and Input in Python

```python
print("My name is Python.")

name = input("What is your name? (type in your name here and hit 'enter': ")

print("Your name is", name)

age = input("How old are you? (type in your age here and hit 'enter': ")

print("You are ", age, "years old.")
```

---

# Acknowledgement

* Professor Hyung-Joo Kim
* Professor Tony Gaddis and Pearson Education, Ltd.
