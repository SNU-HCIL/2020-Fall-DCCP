layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Input, Processing, and Output

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---

# Designing a Program

* Programs must be designed before they are written


* Program development cycle:
    * Design the program
    * Write the code
    * Correct syntax errors and static sematics errors
    * Test the program
    * Correct logic errors (i.e., sematics errors)

--

# Design is Important!

* Design is the most important part of the program development cycle


* Understand the task that the program is to perform
   * Work with users to get a sense what the program is supposed to do
   * Ask questions about their .red[goals] and .red[tasks]
   * Create one or more software requirements (program details)
    

---
# Problems and Algorithms

* In many domains there are key general problems (or tasks) that ask for .red[output] with specific properties when given valid .red[input].

* The first step is to .red[precisely state the problem], using the appropriate .red[structures] to specify the input and the desired output.

* We then solve the general problem by .red[specifying the steps of a procedure] that takes a valid input and produces the desired output.  This procedure is called an .red[algorithm]. 

---
# Program Implements Algorithm

 
* An .red[algorithm] is a finite set of precise instructions for performing a computation or for solving a problem.

* The foundation of computer programming.
* Most generally, an algorithm just means a .red[definite procedure] for performing some sort of task.
* A computer program is simply a .red[description of an algorithm in a language] precise enough for a computer to understand, requiring only operations the computer already knows how to do.
* We say that a program .red[implements] its algorithm.

  
.right[<img src="https://www.researchgate.net/profile/Jorge_Fernandez25/publication/326357560/figure/fig13/AS:647700987011079@1531435357496/Abu-Jafar-Muhammad-ibn-Musa-al-Khwarizmi.png" width=100>]

.right[
Abu Ja’far Muhammed ibin Musa .red[Al-Khowarizmi]  
"Algorithmi"
(780-850)
]

---

# Designing a Program

* Determine the steps that must be taken to perform the task
    * Break down required task into a series of steps
    * Create an algorithm, listing logical steps that must be taken
    * Algorithms are often described in Pseudocode


* .red[Pseudocode]
   * Fake code
   * Informal language that has no syntax rule 
   * Not meant to be compiled or executed
   * Used to create a model program
   * No need to worry about syntax errors
   * Focus on program’s .red[high-level design]
   * Helps us analyze the time required to solve a problem using an algorithm, independent of the actual programming language used to implement algorithm 
   * Can be translated directly into actual code in any programming language

---
<img src="https://user-images.githubusercontent.com/39995503/91539385-2f669c80-e954-11ea-91d0-a25b216a895d.png" width=600>

---

# Flowcharts

* Diagram that graphically depicts the steps in a program

.row[
.col-8[
<img src="https://user-images.githubusercontent.com/39995503/91542448-db11eb80-e958-11ea-8e93-2902e97f4bd6.png" width=350>
https://en.wikipedia.org/wiki/Flowchart
]
.col-4[
<img src="https://miro.medium.com/max/690/1*HdrcTjtfgBfd_UQzNYWraQ.png" width=250>
]
]
https://medium.com/@ralphagarcia2017/draw-professional-flowchart-online-ee199179a4fc

---

# Input, Processing, and Output

* Typically, computer performs three-step process
   * Receive .red[input]
        * Input: any data that the program receives while it is running
   * Perform some .red[processing] on the input
        * Example: mathematical calculation
   * Produce .red[output]
   
---
# Displaying Output with the `print` Function

* .red[Function]: piece of prewritten code that performs an operation


* `print` function: displays output on the screen
* .red[Argument]: data given to a function
    * Example: data that is printed to screen
* Statements in a program execute in the order that they appear
    * From top to bottom


```python
# exmaple code to show how to use the print function
print("This is my first Python output!") # print: function name
print("This is my second Python output!") # string: argument
```

---

# Function Definitions and Function Calls

* In Python, each fuinction definition is of the form:


&ensp;&ensp;&ensp;&ensp;`def` .blue[*name of function*] (list of .green[*formal parameters*]): <br\>  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;.red[*body of function*]


* Example:

    ```python3
    def maxVal(x, y):
        if x > y:
            return x
        else:
            return y
    ```


* We can call this function after definition:
    ```python3
    maxVal(3, 4)  # this expression returns 4
    ```
    
---
# Strings and String Literals

* .red[String]: sequence of characters that is used as data
* .red[String literal]: string that appears in actual code of a program
    * Must be enclosed in single (`'`) or double (`"`) quote marks
* String literal can be enclosed in triple quotes (`'''` or `"""`)
   * Enclosed string can contain both single(`'`) and double(`"`) quotes and can have multiple lines
   * .red[Multiline strings] with triple quotes
        
```python3
# exmaple code to show how to use the print function
print('''Title: "The Waste Land"''')
print('BY T. S. ELIOT')

print("""April is the cruellest month, breeding

Lilacs out of the dead land, mixing

Memory and desire, stirring

Dull roots with spring rain.""")
```


---
# `print` Function with Multiple Arguments

* Python allows one to display multiple items with a single call to print
   * Items are separated by commas when passed as arguments
   * Arguments displayed in the order they are passed to the function
   * Items are automatically separated by a .red[space] when displayed on screen
    
```python
# This program demonstrates the print function with two arguments.
room = 503
print('I am staying in room number', room)

firstName = 'Martin'
middleName = 'Luther'
lastName = 'King'
print(firstName, middleName, lastName)
```

---
# Comments

* Notes of explanation within a program
* Ignored by Python interpreter
* Intended for a person reading the program’s code


* Begin with a `#` character


* End-line comment: appears at the end of a line of code
* Typically explains the purpose of that line

```python
# exmaple code to show how to use the print function
print("This is my first Python output!") # end-line comment
print("This is my second Python output!") # second statement
```
---
# Multiline String as Comments

* Python <strong>ignore</strong> string literals that are not assigned to a variable
* multiline string literals as multiline comment

* Example: relu function in activations.py (Keras project)
```python3
def relu(x, alpha=0., max_value=None):
       """
        Rectified Linear Unit.
        # Arguments
            x: Input tensor.
            alpha: Slope of the negative part. Defaults to zero.
            max_value: Maximum value for the output.
        # Returns
            The (leaky) rectified linear unit activation: `x` if `x > 0`,
            `alpha * x` if `x < 0`. If `max_value` is defined, the result
            is truncated to this value.
        """
        return K.relu(x, alpha=alpha, max_value=max_value)
```

---
# Variables

* Variable: .red[**name**] that .red[**represents a value**] stored in main memory
   * Used to access and manipulate data stored in memory
   * A variable .red[references] the value it represents


* In Python, .red[a variable is just a name], nothing more!

* .red[**Assignment**] statement: used to .red[**create a variable**] and make it .red[**reference**] data
* General format is `variable = expression`
    * Example: `age = 25`
    * ***Assignment operator***: the equal sign (`=`)


* In an assignment statement, variable receiving value must be on left side


* A variable can be passed as an argument to a function
    * Variable name should not be enclosed in quote marks


* You can only use a variable if a value is assigned to it

---
# Variables

```python
age = 25 # create the variable named "age" and it references the value, 25
new_age = age # create another vaiable that also references the same object
```
<img src="https://user-images.githubusercontent.com/39995503/91629980-a65d6d00-ea08-11ea-84e3-2b3daf727279.png" height=300>
--
<img src="https://user-images.githubusercontent.com/39995503/91629950-58e10000-ea08-11ea-8efc-c291b6a72690.png" height=300>


---
# Variable Naming Rules

* Rules for naming variables in Python:
    * Variable name cannot be a Python keyword 
    * Variable name cannot contain spaces
    * First character must be a letter or an underscore(`_`)
    * After first character may use letters, digits, or underscores
    * Variable names are case sensitive


* Variable name should reflect its use
```    
    gross_pay  # snake case
    pay_rate  
    hot_dogs_sold_today  
    
    grossPay   # camel case
    payRate  
    hotDogsSoldToday
```


---

# Variable Reassignment

* Variables can reference different objects (or values) while program is running


* .red[Garbage collection]: removal of values that are no longer referenced by variables
    * Carried out by Python interpreter


* A variable can refer to item of any type
   * Variable that has been assigned to one type can be reassigned to another type
   * .red[Dynamic Binding] vs. .red[Static Binding]
    
<img src="https://user-images.githubusercontent.com/39995503/91630838-de1be300-ea0f-11ea-88fc-760ece6f61c8.png" height=250>
--
<img src="https://user-images.githubusercontent.com/39995503/91630842-effd8600-ea0f-11ea-9956-5aa7bea684ea.png" height=250>

---

# Variable Reassignment

```python
year = 2020
print('The data type of "year":\n', type(year))
year = "2020"
print('The data type of "year":\n', type(year))
```   

* Built-in Function `type`
    * `class type(object)` : With one argument, return the type of an object.

---

# Numeric Data Types, Literals, and `str` Data Type

* Data types: categorize values in memory
    * e.g., `int` for integer, `float` for real number, `str` used for storing strings in memory
    * `room = 503`  
    * `dollars = 2.75`  
    * `name = 'James'`


* .red[Numeric literal]: number written in a program
   * .red[No decimal point] considered `int`, otherwise, considered `float`
 
 
* Some operators behave differently depending on data type (`+`/`*` is overloaded)
    * `1 + 2`
    * `'a'+'b'`
    * `3 * 4`
    * `3 * 'a'`

---

# Reading Input from Keyboard

* Most programs need to read input from the user


* Built-in `input` function reads input from keyboard
   * Returns the data as a .red[string]
   * Format: `variable = input(prompt)`
       * prompt is typically a string instructing user to enter a value
   * Does not automatically display a space after the prompt
   


```python
# Get the user's first name.
first_name = input('Enter your first name: ')

# Get the user's last name.
last_name = input('Enter your last name: ')

# Print a greeting to the user.
print('Hello,', first_name, last_name)
```

---
# Reading Input from Keyboard
* Built-in functions convert between data types
* `int(item)` converts item to an `int`
* `float(item)` converts item to a `float`
* Nested function call: 
    * `function1(function2(argument))`
    * value returned by `function2` is passed to `function1`



```python
# Get the user's name, age, and income.
name = input('What is your name? ')
age = int(input('What is your age? '))
income = float(input('What is your income? '))
# Display the data.
print('Here is the data you entered:')
print('Name:', name)
print('Age:', age)
print('Income:', income)
```
---

# Performing Calculations

* Math expression: performs calculation and gives a value
    * Math operator: tool for performing calculation
    * Operands: values surrounding operator
        * Variables can be used as operands
    * Resulting value typically assigned to variable


* Two types of division:
    * `/` (division) operator performs floating point division
    * `//` (floor division) operator performs integer division
        * Positive results truncated, negative rounded away from zero

```
    >>> 10/3
    3.3333333333333335
    >>> 10//3
    3
    >>> -10//3
    -4
    >>> 
```
---

# Math Operators in Python

.row[
.col-8[
* Three numeric types: 
    * `int` for integers 
    * `float` for floating point numbers
    * `complex` for complex numbers


* Integers
   * .red[unlimited] precision
   * Booleans (`bool`) are a subtype of integers


* Floating point numbers are usually implemented using `double` in C

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a9/IEEE_754_Double_Floating_Point_Format.svg/1920px-IEEE_754_Double_Floating_Point_Format.svg.png" height=100>
]
.col-4[
<img src="https://user-images.githubusercontent.com/39995503/92233067-918e4700-eeea-11ea-9ea0-c24c3dc238b3.png" width=300>
]
]

* Mathematical functions in the `math` module
    * https://docs.python.org/3/library/math.html

---

# Performing Calculations


<iframe src="http://brython.info/console.html" width="800" height="400"></iframe>


* Operators in Python  
    <img src="https://user-images.githubusercontent.com/39995503/91682373-527b9100-eb8c-11ea-995f-1a1d9d500ccc.png" width=700>

---
  

# Operator  Precedence and Grouping with Parentheses   

* Python operator precedence:
    1. Operations enclosed in parentheses
        * Forces operations to be performed before others
    2. Exponentiation (`**`)
    3. Multiplication (`*`), division (`/` and `//`), and remainder (`%`)
    4. Addition (`+`) and subtraction (`-`)


* Higher precedence performed first
    * Same precedence operators execute from left to right
    <img src="https://user-images.githubusercontent.com/39995503/92428117-406fa300-f1c9-11ea-8cb8-295c0754eae8.png" width=500>

---
  

# Operator  Precedence in Python 

<img src="https://user-images.githubusercontent.com/39995503/91633823-55f50800-ea26-11ea-884f-0a1c760495fe.png" width=500>  

https://docs.python.org/3/reference/expressions.html#operator-precedence

---

# Assignment Statements

* Simple Assignment
`<variable> = <expr>`

* `<variable>` is an identifier, `<expr>` is an expression
* The expression on the .red[RHS](Right-Hand Side) is evaluated to produce a value which is
then associated with the variable named on the .red[LHS](Left-Hand Side)
    
```
>>> x = 3.9 * x * (1 - x)
>>> fahrenheit = 9/5 * celsius + 32
>>> x = 5
```

---
# Simultaneous Assignment

* Several values can be calculated at the same time

    ```<var1>, <var2>, ... = <expr1>, <expr2>, ...```

* Evaluate the expressions on the RHS and assign them to the variables on the LHS

    ```python3
    sum, diff = x+y, x-y
    ```

* How could you use this to swap the values for `x` and `y`?
* Would this work?
    ```python3
    x = y
    y = x
    ```
* We can use a temporary variable as we can do in other programming languages like C, Java
* We can swap the values of 2 variables quite easily in Python!

    `x, y = y, x`


---
    

# Converting Math Formulas to Python Statements

* Operator required for any mathematical operation 


* When converting mathematical expression to programming statement:
    * May need to add multiplication operators
    * May need to insert parentheses 


.center[<img src="https://user-images.githubusercontent.com/39995503/92428864-42d2fc80-f1cb-11ea-968f-41a3c034bfb8.png" width=500>]

---

# Implicit Data Type Conversion

* Data Type Conversion occurs in mixed-type expressions 
* Data type resulting from math operation depends on data types of operands


* Two `int` values (with operator `+`, `-`, `*`, `//`): result is an `int`
* Two `int` values (with operator `/`): result is n `float`
* Two `float` values: result is a `float`
* `int` and `float`: `int` temporarily converted to `float`, result of the operation is a `float`
    * Mixed-type expression


* Type conversion of `float` to `int` causes truncation of fractional part

---

# Implicit Data Type Conversion

* Data Type Conversion occurs in mixed-type expressions 
* Data type resulting from math operation depends on data types of operands


```python
fvalue = 5*2.0
print("result :", fvalue);

fvalue = 2.6
ivalue = int(fvalue)
print("integer value:", ivalue)

fvalue = -2.9
ivalue = int(fvalue)
print("integer value:", ivalue)
```

---
# Breaking Long Statements into Multiple Lines
* Long statements cannot be viewed on screen without scrolling and cannot be printed without cutting off


* Multiline continuation character (`\`): Allows to break a statement into multiple lines


```python
value1 = 100
value2 = 200
value3 = 300

result = value1*value2 + value2*value3 \
            + value3*value1
```

---
# Breaking Long Statements into Multiple Lines

* Any part of a statement that is enclosed in parentheses can be broken without the line continuation character

```python
value1 = 100
value2 = 200
value3 = 300

print("Monday's sales are", value1,
      "and Tuesday's sales are", value2,
      "and Wednesday's sales are", value3)

total = (value1 + value2 +
         value3 + value4 +
         value5 + value6)
```

---
# More about `print` Function 

* `print` function displays line of output 


* Newline character at end of printed data
* Special argument `end='delimiter'` causes `print` to place delimiter at end of data instead of newline character


* `print` function uses space as item separator
* Special argument `sep='delimiter'` causes print to use delimiter as item separator

```python3
print('1', end=' ')
print('2', end=' ')
print('3')

print('One', end='')
print('Two', end='')
print('Three')

print('One', 'Two', 'Three')
print('One', 'Two', 'Three', sep='*')
```

---
# Escape Sequence

.row[
.col-8[

* Special characters appearing in string literal
   * Treated as commands embedded in string
   * Preceded by backslash (`\`)
    * Examples: newline (`\n`), horizontal tab (`\t`)
    
```python
print("Read \"Hamlet\" by tomorrow.")
print('I\'m ready to begin.')

print('Mon\tTues\tWed')
print('Thur\tFri\tSat')

print('The path is C:\\temp\\data.')

print(r'The path is C:\temp\data.')
```
]
.col-4[
<img src="https://user-images.githubusercontent.com/39995503/91674265-fe17e780-eb72-11ea-8882-b1d83fc1a08e.png" width=300>
]
]

---
# Formatting Numbers
* Can format display of numbers on screen using built-in `format` function
   * Two arguments:
       * Numeric value to be formatted
       * Format specifier
   * Returns string containing formatted number
   * Format specifier typically includes precision and data type
       * Can be used to indicate scientific notation, comma separators, and the minimum field width used to display the value

```python3
>>> print(format(12345.6789, '.2f')) 
12345.68
>>> print(format(12345.6789, '.1f')) 
12345.7
>>> print('The number is', format(1.234567, '.2f'))
The number is 1.23
```

---
# Formatting Numbers

```python3
>>> print(format(0.5, '.0%')) 
50%
>>> print(format(0.5, '%')) 
50.000000%
>>> print(format(0.5, '.0%')) 
50%
>>> print(format(123456, 'd')) 
123456
>>> print(format(123456, ',d')) 
123,456
>>> print(format(123456, '10d')) 
    123456
>>> print(format(123456, '10,d')) 
   123,456
>>>
```

---


# Python Built-in Functions

<img src="https://user-images.githubusercontent.com/39995503/91674429-944c0d80-eb73-11ea-922b-1caaea4b5f00.png" width=700>


---
# `format`

* `format(value[, format_spec])`


* Convert a value to a “formatted” string representation, as controlled by format_spec. 
* The interpretation of format_spec will depend on the type of the value argument
* There is a standard formatting syntax that is used by most built-in types
   * [Format Specification Mini-Language](https://docs.python.org/3.3/library/string.html#format-specification-mini-language).
* The default format_spec is an empty string which usually gives the same effect as calling `str(value)`.

---
# Format examples

```python3
>>> '{0}, {1}, {2}'.format('a', 'b', 'c')
'a, b, c'
>>> '{2}, {1}, {0}'.format('a', 'b', 'c')
'c, b, a'
>>> '{0}{1}{0}'.format('abra', 'cad')   # arguments' indices can be repeated
'abracadabra'
>>> 'Coord: {latitude}, {longitude}'.format(latitude='37.24N', longitude='-115.81W')
'Coord: 37.24N, -115.81W'
>>> '{:<30}'.format('left aligned')
'left aligned                  '
>>> '{:>30}'.format('right aligned')
'                 right aligned'
```
---
# Format examples

```python3
>>> '{:^30}'.format('centered')
'           centered           '
>>> '{:*^30}'.format('centered')  # use '*' as a fill char
'***********centered***********'
>>> '{:,}'.format(1234567890)
'1,234,567,890'
>>> 'Correct answers: {:.2%}'.format(19/22)
'Correct answers: 86.36%'
```
---
# Magic Numbers

* A magic number is an .red[unexplained numeric value] that appears in a program’s code. 
* Example: `amount = balance * 0.069`


* What is the value 0.069? An interest rate? A fee percentage? Only the person who wrote the code knows for sure.

* It can be difficult to determine the purpose of the number.
* If the magic number is used in multiple places in the program, it can take a lot of effort to change the number in each location, should the need arise.

* You take the risk of making a mistake each time you type the magic number in the program’s code. 
    * For example, suppose you intend to type 0.069, but you accidentally type .0069. This mistake will cause mathematical errors that can be difficult to find.
    
---
# Named Constants

* You should use named constants instead of magic numbers.
* A named constant is a name that represents a value that does not change during the program's execution.
* Example: `INTEREST_RATE = 0.069`
* This creates a .red[named constant] named `INTEREST_RATE`, assigned the value 0.069. It can be used instead of the magic number: `amount = balance * INTEREST_RATE`

* Named constants make code self-explanatory (self-documenting)
* Named constants make code easier to maintain 
    * change the value assigned to the constant, and the new value takes effect everywhere the constant is used
* Named constants help prevent typographical errors that are common when using magic numbers

---
# Python Built-in Constants

`False`  
`True`  
`None`  
`NotImplemented`  
`Ellipsis`  
`__debug__`  

https://docs.python.org/3/library/constants.html


---

# Acknowledgement

* Professor Hyung-Joo Kim
* Professor Tony Gaddis and Pearson Education, Ltd.

