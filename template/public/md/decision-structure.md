layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Decision Structures and Boolean Logic

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---

# Structuring a Program

.row[
.col-7[

* Control structure 
    * logical design that controls order in which set of statements execute


* Sequence structure
    * set of statements that execute in the order they appear
    
    
* Decision structure
    * specific action(s) performed only if a condition exists
    * also known as selection structure
]
.col-5[
<img src="https://user-images.githubusercontent.com/39995503/91689100-63cd9900-eb9e-11ea-91a9-26b619d3b92b.png" width=360>
]
]

---

# `if` Statement

* In flowchart, diamond represents true/false condition that must be tested
* Actions can be .red[conditionally] executed
   * Performed .red[only when a condition is true]
* Single alternative decision structure: provides only one alternative path of execution
   * If condition is not true, exit the structure

.row[
.col-6[

<img src="https://user-images.githubusercontent.com/39995503/91682725-6f649400-eb8d-11ea-916a-a5b89c6f8c8a.png" width=300>

]
.col-6[

```python3
if condition:
    statement
    statement
```
]
]

---
# How to Define a Condition

* .red[Boolean expression]: expression tested by `if` statement to determine if it is true or false
    * Example: `a > b`
    * `True` if `a` is greater than `b`; `False` otherwise


* .red[Relational operator]: determines whether a specific relationship exists between two values
    
.center[<img src="https://user-images.githubusercontent.com/39995503/92232269-3a3ba700-eee9-11ea-9ba1-928dff7ff2a9.png" width=300>]
    
---
# `if` Statement - example
```python

HIGH_SCORE = 95
test1 = int(input('Enter the score for test 1: '))
test2 = int(input('Enter the score for test 2: '))
test3 = int(input('Enter the score for test 3: '))

# Calculate the average test score.
average = (test1 + test2 + test3) / 3

# Print the average.
print('The average score is', average)

# If the average is a high score,
# congratulate the user.
if average >= HIGH_SCORE:
    print('Congratulations!')
    print('That is a great average!')
```
---
# Boolean Expressions and Relational Operators 

* Any relational operator can be used in a decision block
    * Example: `if balance == 0`
    * Example: `if payment != balance`


* It is possible to have a block inside another block
   * Example: `if` statement inside another `if` statement
   * Statements in inner .blue[block] must be .red[indented] with respect to the outer .blue[block]
    
.center[<img src="https://user-images.githubusercontent.com/39995503/91687487-ce7cd580-eb9a-11ea-97c8-71df99cb6ee4.png" width=500>]


---
# `if-else` Statement

* Dual alternative decision structure: two possible paths of execution
* One is taken if the condition is true, and the other if the condition is false

* Syntax: 

```python3
if condition:
    statements
    statements
else:
    statements
    statements
```


* `if` clause and `else` clause must be .red[aligned]
* Statements must be .red[consistently indented]

---

# `if-else` Statement

* Dual alternative decision structure

<img src="https://user-images.githubusercontent.com/39995503/91688087-2962fc80-eb9c-11ea-8823-c727d6ca24e6.png" width=450>  

* .red[Alignment] and .red[indentation] are important!

<img src="https://user-images.githubusercontent.com/39995503/91688150-56171400-eb9c-11ea-94de-d0d915503b63.png" width=700>

---

# String Comparison
* Strings can be compared using the `==` and `!=` operators


* String comparisons are .red[case sensitive]


* Strings can be compared using `>`, `<`, `>=`, and `<=`
   * Compare character by character based on the .red[ASCII values] for each character
   * If shorter word is substring of longer word, longer word is greater than shorter word  
   * e.g., 'Mary' > 'Mark', 'James' > 'Jam'
    
.center[<img src="https://user-images.githubusercontent.com/39995503/91688593-44823c00-eb9d-11ea-8b8a-c6737862790b.png" width=150>]

---
# Nested Decision Structures

* A decision structure can be nested inside another decision structure
* Example: 


```python3
# Determine the grade.
if score >= A_SCORE:
    print('Your grade is A.')
else:
    if score >= B_SCORE:
        print('Your grade is B.')
    else:
        if score >= C_SCORE:
            print('Your grade is C.')
        else:
            if score >= D_SCORE:
                print('Your grade is D.')
            else:
                print('Your grade is F.')
```

---

# `if-elif-else` Statements
* Makes logic of nested decision structures simpler to write

.row[
.col-6[
```python3
# Determine the grade.
if score >= A_SCORE:
    print('Your grade is A.')
elif score >= B_SCORE:
    print('Your grade is B.')
elif score >= C_SCORE:
    print('Your grade is C.')
elif score >= D_SCORE:
    print('Your grade is D.')
else:
    print('Your grade is F.')
```
]
.col-6[
<img src="https://user-images.githubusercontent.com/39995503/91690596-36ceb580-eba1-11ea-8454-7a5da152331b.png" width=400>
]
]

---
# Logical Operators (Boolean Operators)

* operators that can be used to create complex Boolean expressions


* `and` operator and `or` operator: .red[binary] operators, connect two Boolean expressions into a .red[compound] Boolean expression


* `not` operator: .red[unary] operator, reverses the truth of its Boolean operand

---
# `and` Operator

* Takes two Boolean expressions as operands 


* Creates compound Boolean expression that is true only when both sub expressions are true


* Can be used to simplify nested decision structures


* Truth table for the `and` operator 

```
     P        Q         P and Q  
     --------------------------
     False    False     False  
     False    True      False  
     True     False     False  
     True     True      True
```

---
# `or` Operator

* Takes two Boolean expressions as operands 


* Creates compound Boolean expression that is true when either sub expressions is true


* Can be used to simplify nested decision structures


* Truth table for the `or` operator 

```
     P        Q         P or Q  
     --------------------------
     False    False     False  
     False    True      True  
     True     False     True  
     True     True      True
```

---
# Short-Circuit Evaluation

* Deciding the value of a compound Boolean expression after evaluating only one sub expression


* Performed by the `or` and `and` operators


* For `or` operator: If left operand is `True`, compound expression is `True`; the expression on the .red[right side will not be evaluated (or checked)]. Otherwise, evaluate right operand


* For `and` operator: If left operand is `False`, compound expression is `False`. the expression on the .red[right side will not be evaluated (or checked)]. Otherwise, evaluate right operand

---
# Short-Circuit Evaluation


```python
def f(arg) :  # defining a function that retuns a Boolean value
    print("f is called!")
    if (arg>3):
        return True
    else:
        return False

if 3 <= 2 or f(2):
    print('ok')
else:
    print('not ok')
```

---
# `not` Operator

* Takes one Boolean expressions as operand and reverses its logical value


* Sometimes it may be necessary to place parentheses around an expression to clarify to what you are applying the `not` operator


* Truth table for the `not` operator 

```
     P        not P  
     --------------
     False    True  
     True     False
```

```python
temp = 99
    
if not (temp < 100):   # () is not necessary, but it is more clear!
    print('It is hotter than 100.')
else:
    print('It is not hotter than 100.')

```

---
# `not` Operator


```python
temp = 99
    
if (not temp) > 100:
    print('It is not hotter than 100.')
else:
    print('It is hotter than 100.')

print(not temp)
print(False == 0)
```

* `if not temp > 100` is the same as `if not (temp > 100)`
* `(not temp) > 100`
   * `temp` is not `0` -> meaning it is `True` -> `not temp` is `False` -> value of `False` is `0`

---
# Checking Numeric Ranges with Logical Operators

* To determine whether a numeric value is within a specific range of values, use `and` operator 
    * Example: `x >= 10 and x <= 20`


* To determine whether a numeric value is outside of a specific range of values, use `or` operator
    * Example: `x < 10 or x > 20`


* The following compound comparisons are valid expressions in Python

```python3
>>> 1 < 5 < 7
True
>>> x = 1
>>> 2 > x < 7
True
>>> 5 > 4 > 3.2 >= 1 == 1 != 8
True
```
---
# Boolean Variables

* Boolean variable references one of two Boolean constants, `True` or `False`
    * Represented by `bool` data type
    * The built-in function `bool()` can be used to convert any value to a Boolean
    * In numeric contexts, they behave like the integers `0` and `1`, respectively.



* Commonly used as flags
* .red[Flag]: variable that signals when some condition exists in a program
    * Flag set to `False` -> condition does not exist
    * Flag set to `True` -> condition exists
    * e.g., `isSomeConditionSet = True`
    
---
# Truth Value Testing

* Any object can be tested for truth value, for use in an `if` or `while` condition or as operand of the Boolean operations


* By default, an object is considered .red[true] unless its class defines either a `__bool__()` method that returns .red[`False`] or a `__len__()` method that returns .red[zero], when called with the object. 


* Here are most of the built-in objects considered false:
    * constants defined to be false: `None` and `False`.
    * zero of any numeric type: `0`, `0.0`, `0j`, `Decimal(0)`, `Fraction(0, 1)`
    * empty sequences and collections: `''`, `()`, `[]`, `{}`, `set()`, `range(0)`



* Operations and built-in functions that have a Boolean result always return `0` or `False` for false and `1` or `True` for true, unless otherwise stated.

---

# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.

