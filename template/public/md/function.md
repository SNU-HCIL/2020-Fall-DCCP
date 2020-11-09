layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Function

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---
# Introduction to Functions

* Function: group of statements within  a program that perform a specific task
   * Usually one task of a large program
   * Known as .red[divide and conquer] approach (.red[decomposition])
   
   
* .red[Modular programming]: a software design technique that emphasizes separating the functionality of a program into independent, interchangeable modules
   * high-level `decomposition` of the code of an entire program into pieces: .red[package](folder) -> .red[module](file) -> .red[function]
   * each module contains everything necessary to execute only one aspect of the desired functionality
 
 
* .red[Abstraction]: it allows the users of a function to use a piece of code as if it were a .blue[black box] 
   * interior implementation details: we cannot see, don't need to see,  and shouldn't even want to see
   * users of a function just have to know `assumptions` (about input) and `guarantees` (about output) 


* Top-down design: technique for breaking algorithm into functions

---

# Benefits of Modularizing a Program with Functions

* Simpler code


* Code reuse
   * write the code once and call it multiple times 
   
   
* Better testing and debugging 
   * can test and debug each function individually
   
   
* Faster development


* Easier facilitation of teamwork
   * different team members can write different functions

---

# Function Definitions

* In Python, each fuinction definition is of the form:


&ensp;&ensp;&ensp;&ensp;.purple[def] .blue[*name of function*] (list of .green[*formal parameters*]): <br\>  
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;.red[*body of function*]


* Example:

    ```python3
    def maxVal(x, y):   # function header
        """Return maximum of x and y."""
        if x > y:
            return x
        else:
            return y
    ```
---
# Indentation in Python

* Each block must be indented
   * Lines in a block must begin with the same number of spaces
   * Use .red[tabs] or .red[spaces] to indent lines in a block, but not both as this can confuse the Python interpreter


* IDLE automatically indents the lines in a block


* Blank lines that appear in a block are ignored


---

# Function Definitions

* Function is also an .red[object].


* We can call this function after definition:


```python3
    >>> maxVal
    <function maxVal at 0x7fb2c65751f0>
    >>> maxVal(3, 4)
    4
    >>> mV = maxVal
    >>> mV(3, 4)
    4
    >>> 
```


* At the time of .purple[function invocation] (or .purple[function call])
   * .blue[Formal parameters] (`x` and `y`) are .green[bound] to .red[actual parameters] (`3` and `4`) 
     <br/>-> <span class="red">binding</span>
   * .red[actual parameters] are also referred to as .red[arguments]
---
# Passing Arguments to Functions

* .red[Argument]: piece of data that is sent into a function
   * Function can use argument in calculations
   * When calling the function, the argument is placed in parentheses following the function name


* .red[Formal Parameter] (.green[Parameter variable]): variable that is assigned the value of an argument when the function is called
   * The parameter and the argument reference the same value


* Scope of a parameter: within the function in which the parameter is used
   * .red[Scope]: the part of a program in which a variable may be accessed

.row[
.col-5[
```python3
def show_triple(number):
    result = number * 3
    print(result)
    
def main():
    value = 10
    show_triple(value)
```
]
.col-7[
<img src="https://user-images.githubusercontent.com/39995503/93667671-a8c05d80-fac2-11ea-9eb5-47d220a94424.png" width=250>
]
]

---
# Local Variables

* Local variable: variable that is .red[assigned a value] inside a function
   * Belongs to the function in which it was created
   * Only statements inside that function can access it, error will occur if another function tries to access the variable


* .red[Scope]: the part of a program in which a variable may be .red[accessed]
   * For local variable: its scope is the function in which it is created
   * Local variable cannot be accessed by statements inside its function which precede its creation
    
    ```python3
    def f(args):
        print(args, x)
        x = 3
    ```


* Different functions may have local variables with the same name 
   * Each function does not see the other function’s local variables, so no confusion

---


# When a function is called: e.g., `maxVal(1+2, z)`

```python3
    z = 6
    result = maxVal(1 + 2, z)
```

* The expressions that make up the actual parameters are evaluated.


* The formal parameters are bound to the evaluation results.
    * `x` -> `3`, `y` -> whatever value of `z` at the time of call
    
    
* The code in the body is executed.


* A return statement determins the value of invocation (or call).
    * If there is no return statement to execute, returns the value `None`.
    
    
* The value of the invocation (i.e., the function call) is the returned value.


---
# Function returns a value

```python3
    z = 6
    result = maxVal(1 + 2, z)  # maxVal returns a value, 6
    print(result)
```

* Even .red[void functions] (without a `return` statement) do return a value, i.e., `None`

```python
def naturalNumbers(n):
    i=1
    while i <= n:
        print(i)
        i += 1
   
naturalNumbers(10)       # prints natural numbers from 1 to 10
naturalNumbers(0)        # prints nothing
print(naturalNumbers(0)) # prints "None"
```
---
# Positional Arguments vs. Keyword Arguments
* Two ways that formal parameters get bound to actual parameters
   * .red[positional] arguments (bound by position of argument)
   * .red[keyword] arguments (bound by the name of the formal parameter)
   
```python3
def printName(firstName, lastName, reverse):
    if reverse:
        print(lastName + ', ' + firstName)
    else:
        print(firstName, lastName)
        
printName('Jason', 'Mraz', False)  # positional
printName('Jason', 'Mraz', True)   # positional
printName('Jason', 'Mraz', reverse = False) # positional and keyword
```
---
# Positional Arguments vs. Keyword Arguments
   
```python3
def printName(firstName, lastName, reverse):
    if reverse:
        print(lastName + ', ' + firstName)
    else:
        print(firstName, lastName)
        
printName('Jason', 'Mraz', False)  # positional
printName('Jason', 'Mraz', True)   # positional
printName('Jason', 'Mraz', reverse = False) # positional and keyword

printName(reverse=False, lastName = 'Mraz', firstName = 'Jason') # keyword
printName('Jason', firstName = 'Jason', False) # error
```

* keyword arguments can appear in any order

* .red[keyword arguments must follow positional arguments]
---
# Keyword Arguments and Default (Argument) Values

* We can specify a default value for one or more arguments/parameters.


* Keyword arguments are commonly used with default argument values

```python
def printName(firstName, lastName='Mraz', reverse=False):
    if reverse:
        print(lastName + ', ' + firstName)
    else:
        print(firstName, lastName)

printName('Jason')
printName('Jason', 'Bourne')
printName('Jackson', 'Brown', True)
printName(firstName='Jackson')
```

---
# More about Default Values

* The default values are evaluated at the point of function .red[definition]

```python
i = 5

def f(arg = i):
    print(arg)

i = 6
f()
```

---
# More about Default Values

* The default values are .red[evaluated only once].

```python
def append2List(a, L = []):
    L.append(a)
    return L

print(append2List(1))   # prints [1]
print(append2List(2))   # prints [1, 2]
print(append2List(3))   # prints [1, 2, 3]
```

* A .red[reference] to the default value (i.e., object) is saved in the function definition

* Don't use a .red[mutable] object as a default value!

---
# Scoping

.row[
.col-3[

```python3
def f(x):    
    x = x + 1
    print(x)  
    # prints 4

x = 3
f(x)
print(x)  
# prints 3
```
]
.col-9[
<img src="https://user-images.githubusercontent.com/39995503/93693697-2f665080-fb3e-11ea-8e9f-87283eeedc65.png" width=600>
]
]

* Even though the actual and formal parameters have the same name, they are not the same variable
* Each function defines a new .red[name space], also called a .red[scope]
* The formal parameter `x` exists (can be accessed) only within `f`
* The assgnment statement `x = x + 1` binds the local name `x` to the object `4`
* This assgnment have no effect on the bindings of the name `x` outside `f`

---
# Symbol Table and Stack Frame

* At top level, i.e., the level of the shell, a .red[symbol table] (often called a .red[stack frame]) keeps track of .blue[all names] defined at that level and their .blue[current bindings]
* .green[When a function is called], .purple[a new symbol table is created] for the function 
   * It keeps track of .blue[all names] defined within the function and their .blue[current bindings]
   * If a function is called from within the function, another stack frame is created
   * .green[Functions can reference variables from the containing scope] 
* When the function completes, its .red[stack frame] goes away (is .red[popped] off)

.row[
.col-5[
```python
def f(x):    
    y = 1
    x = x + 1
    print(x)   # prints 4

x = 3
y = 2
f(x)
print(x) # prints 3
print(y) # prints 2
```
]
.col-7[
.center[<img src="https://user-images.githubusercontent.com/39995503/93707699-d7464300-fb6b-11ea-8547-0cc9a1d24e6e.png">]
]
]

---
# Static (or Lexical) Scoping

* We can determine the scope of a name by just looking at the program text
   * without considering the runn-time context, i.e., call stack (dynamic binding)


* The order in which references to names occur is not relevant
   * If an object is bound to a name .red[anywhere in the function body], it is treated as .red[local] to that function
   
```python
def f():
   print(x)  # x references the x outside f
   
def g():
   print(x)  # x references the local x
   x = 1

x = 3
f()    # prints 3
x = 3
g()    # unboundLocalError: local variable 'x' referenced before assignment
```

---
# Nested Scopes
 
.row[
.col-5[
```python
def f(x):
    def g():
        x = 'abc'
        print('x =', x)
    def h():
        z = x
        print('z =', z)
    x = x + 1
    print('x =', x)
    h()
    g()
    print('x =', x)
    return g
    
x = 3
z = f(x)
print('x =', x)
print('z =', z)
z()
```
]
.col-7[
<img src='https://user-images.githubusercontent.com/39995503/93709727-90f8e000-fb7b-11ea-997d-ab01678ee892.png' width=450>

Result:
```python3
x = 4
z = 4
x = abc
x = 4
x = 3
z = <function f.<locals>.g at 0x7fd7552ec1f0>
x = abc
```
]
]

---
# Global Variable

* Global variable is .red[created by assignment statement] written .red[outside all the functions]


* Can be accessed by any statements in the program file, including from within a function


* If a function needs to assign a value to a global variable, the global variable must be redeclared within the function
   `global variable_name`


* In Python, variables that are only `referenced` inside a function are implicitly .red[global]. 


* If a variable is `assigned a value` anywhere within the function’s body, it’s assumed to be a .red[local] unless explicitly declared as `global`.

---
# Referencing a Global Variable

* In Python, variables that are only `referenced` inside a function are implicitly .red[global].  

```python
# Create a global variable.
my_value = 10

# The show_value function prints
# the value of the global variable.

def show_value():
    print(my_value)

# Call the show_value function.
show_value()
```

---
# To Change a Global Variable

* If a function needs to assign a new value to a global variable, the global variable must be .red[redeclared] with the keyword `global` within the function
   * gernal format: `global variable_name`
   
```python
# Create a global variable.
number = 0

def main():
    global number
    number = int(input('Enter a number: '))
    show_number()
    
def show_number():
    print('The number you entered is', number)

main()
```

---
# Hide/Shadow a Global Variable

* If you do not redeclare a global variable with the `global` keyword inside a function, 
   * you cannot change the variable's value inside that function
   * you are creating a new .red[local variable with the same name] 
   * --> .red[hiding]/.red[shadowing] the global variable
   
```python
# Create a global variable.
number = 0

def main():
    global number   # redeclare the variable, number
    number = int(input('Enter a number: '))
    show_number()
    
def show_number():
    number = 100    # shadow the global variable
    print('The number you entered is', number)

main()
```


---
# Global Constants 

* .red[Named Constants] in Global Scope
   * You should use named constants instead of magic numbers.


* If you do not redeclare a global variable with the global keyword in side a function, you .red[cannot change] the variable's value inside that function.
   * .red[global constant]: global name that references a value that cannot be changed.
   * `CONTRIBUTION_RATE = 0.05` (next page)
   
---
# Gobal Constant - Example

```python3
# The following is used as a global constant
# the contribution rate.
CONTRIBUTION_RATE = 0.05

def main():
    gross_pay = float(input('Enter the gross pay: '))
    bonus = float(input('Enter the amount of bonuses: '))
    show_pay_contrib(gross_pay)
    show_bonus_contrib(bonus)
    
def show_pay_contrib(gross):
    contrib = gross * CONTRIBUTION_RATE
    print('Contribution for gross pay: $', format(contrib, ',.2f'), sep='')

def show_bonus_contrib(bonus):
    contrib = bonus * CONTRIBUTION_RATE
    print('Contribution for gross pay: $', format(contrib, ',.2f'), sep='')

main()
```
---
# Avoid Using Global Variables

* Global variables make debugging difficult
   * Many locations have to be checked to track down a bug


* Functions that use global variables are usually dependent on those variables
   * Makes such functions hard to transfer to another programs
   
   
* Global variables make a program hard to understand
   * The key to making programs readable is locality
   * Global variables can be modified or read in a wide variety of places


* There are times when global variables are just what is needed
   * for debugging or analyzing purpose
   * e.g., count how many times a function has been called

---
# Arbitrary Argument Lists

* a function can be called with an arbitrary number of arguments. 

```python
def sum_many(*args):
    """
    args: passed as a tuple
    """
    
    print(args)
    sum = 0
    for i in args:
        sum = sum + i
    return sum
    
result = sum_many(1, 2, 3)
print(result)  # prints 6
result = sum_many(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
print(result)  # prints 55
```
---
# Arbitrary Argument Lists

```python
def sum_mul(ops, *args):
    if ops == 'sum':
        result = 0
        for i in args:
            result = result + i
    elif ops == 'mul':
        result = 1
        for i in args:
            result = result * i  
    else:
        result = None
    return result
    
result = sum_mul('sum', 1, 2, 3, 4, 5)
print(result)  # prints 15
result = sum_mul('mul', 1, 2, 3, 4, 5)
print(result)  # prints 120
```

---
# Arbitrary Argument Lists

.row[
.col-6[

```python3
def sum(*values, **options):
    """
    values: passed as a tuple
    options: passed as a dictionary
    """
    
    sum = 0
    answer = ''
    
    for i in values:
        sum = sum + i
       
    if 'neg' in options:
        if options['neg']:
            sum = -sum
    
    if 'explain' in options:
        if options['explain']:
            answer = "The answer is "
            
    return answer + str(sum)
```

]
.col-6[

* `**options` expects keyword arguments 
   * of the form `parameter = value` pairs
   * passed as a `dictionary` to the function

```python3
>>> sum(1, 2, 3)
'6'
>>> sum(1, 2, 3, neg = True)
'-6'
>>> sum(1, 2, 3, neg = False)
'6'
>>> sum(1, 2, 3, explain = True)
'The answer is 6'
>>> sum(1, 2, 3, neg=True,explain=True)
'The answer is -6'
```
]
]

---
# Returning Multiple Objects


```python
def sum_and_mul(a, b):
    return a + b, a * b   # returns a tuple

sum, mul = sum_and_mul(1, 2)
print(sum) # prints 3
print(mul) # prints 2

result = sum_and_mul(1, 2)
print(result)  # prints (3, 2)
```

---
# Anonymous Functions with Lambda Expression

* Small .red[anonymous functions] can be created with the `lambda` keyword.

```python3
>>> (lambda a, b: a+b)(1, 2)
3
>>> f = lambda a, b: a+b   # define a lambda function
>>> f
<function <lambda> at 0x7fc9657ac5e0>
>>> f(1, 2)
3
```

This lambda function is equivalent to:

```python3
def f(a, b):
    return a + b
```

---
# Anonymous Functions with Lambda Expression

* Lambda functions can be used wherever function objects are required. 
* They are syntactically restricted to a single expression. 
* Semantically, they are just `syntactic sugar` for a normal function definition. 
* Like nested function definitions, lambda functions can reference variables from the containing scope.

```python3
>>> def make_incrementor(n):
...     return lambda x: x + n    
...     # lambda function can reference the formal parameter (local variable, n)
...
>>> f = make_incrementor(42)
>>> f(0)
42
>>> f(1)
43
```
---
# Anonymous Functions with Lambda Expression

* Let's translate the following code using lambda expression

```python3
def is_even(x):      
    if x % 2 == 0: 
        return True
    else: 
        return False

source_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] 

filtered_list = list(filter(is_even, source_list))   

print(filtered_list)   # prints [2, 4, 6, 8, 10]
```

* Built-in function: `filter(function, iterable)`
   * Construct an iterator from those elements of `iterable` for which `function` returns `True`.

---
# Anonymous Functions with Lambda Expression

* Another use of Lambda expression is to pass a small function as an argument:

```python
# Program to filter out only the even items from a list

source_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

filtered_list = list(filter(lambda x: (x % 2 == 0) , source_list))

print(filtered_list)   # prints [2, 4, 6, 8, 10]
```

---
# Documentation Strings: docstring

* docstring
   * text describing the function what function does
   * describe .red[specification] of a function: `assumptions` and `guarantees`
   * comes immediately after function header
   * use triple quotes to enclose
   
```python3
def myfunc():
   '''
   This description is more than one line and this
   helps people understand what this function does
   '''
   print("Hello") # Greeting
```

---
# Documentation Strings: docstring

* Some `special attributes` of a user-defined `function` object
   * `__doc__` : The function’s .blue[documentation string], or `None` if unavailable 
   * `__name__` : The function’s .blue[name]
 
```python3   
>>> print(myfunc.__doc__)

   This description is more than one line and this
   helps people understand what this function does
   
>>> print(myfunc.__name__)
myfunc

>>> help(myfunc)
Help on function myfunc in module __main__:

myfunc()
    This description is more than one line and this
    helps people understand what this function does
```

---
# Specification of Function in docstring

* A specification of a function defines a contract between
    * the implementer of the function
    * and
    * clients - those who will be writing programs whtat use the function


* It contains .red[assumptions] (about input) and .red[guarantees] (about output)


* Function specification are usually included in docstring 

---
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

```python3
def findRoot(x, power, epsilon):
    """
       Find an approximation to a root.
       
       Assumes x and epsilon int or float, power an int, epsilon > 0 & power >= 1
       Returns float y such that y**power is within epsilon of x. 
           If such a float does not exist, it returns None
    """
    if x < 0 and power % 2 ==0:
        return None
    
    low = min(-1.0, x)
    high = max(1.0, x)
    ans = (high + low) / 2.0
    while abs(ans**power - x) >= epsilon:
        if ans**power < x:
            low = ans
        else:
            high = ans
        ans = (high + low) / 2.0
    return ans
```   

---
# Function Annotations

* completely `optional metadata` information about the types used by user-defined functions 


* Annotations are stored in the `__annotations__` attribute of the function object as a dictionary 
   * have no effect on any other part of the function 

```python3
def f(ham: str, other: str = 'eggs') -> str:
    print("Arguments:", ham, other)
    return ham + ' and ' + other
```

```python3
>>> f('spam')
Arguments: spam eggs
'spam and eggs'
>>> f.__annotations__
{'ham': <class 'str'>, 'other': <class 'str'>, 'return': <class 'str'>}
>>> 
```

---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag