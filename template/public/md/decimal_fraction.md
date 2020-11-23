layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Decimal and Fraction

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  

---
# A Few Words About Using Floating-point Numbers

```python
x = 0.0

for i in range(10):
    x = x + 0.1    # 0.1 = 0.00011001100110011001100.... in binary representation

if x == 1.0:
    print(x, '= 1.0')
else:
    print(x, 'is not 1.0')
```

---
# A Few Words About Using Floating-point Numbers

```python3
epsilon = 0.001
if abs(x - 1.0) < epsilon:
    # do something
```
* .red[Chopping errors] could make devastating results
   * Software Problem Led to System Failure at Dhahran, Saudi Arabia 
      * https://www.gao.gov/assets/220/215614.pdf
      * http://www-users.math.umn.edu/~arnold/disasters/patriot.html

.left[
```
"Because of the way the Patriot computer performs its calculations and 
the fact that its registers are only 24 bits long, 
the conversion of time from an integer to a real number 
cannot be any more precise than 24 bits. 
This conversion results in a loss of precision 
causing a less accurate time calculation."
```
]

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
# Approximate Binary Fraction

* there are many different decimal numbers that share the same nearest approximate binary fraction. 
* `0.1` and `0.10000000000000001` and `0.1000000000000000055511151231257827021181583404541015625` are all approximated by the same binary representation (`3602879701896397 / 2 ** 55`).   
<span style="font-size:10pt">3602879701896397<sub>10</sub> = 1100110011001100110011001100110011001100110011001101<sub>2</sub></span>

.font-14[
```python3
>>> 0.1.hex()
'0x1.999999999999ap-4'
>>> 0.10000000000000001.hex()
'0x1.999999999999ap-4'
>>> 0.1000000000000000055511151231257827021181583404541015625.hex()
'0x1.999999999999ap-4'
```
]

* Starting with Python 3.1, the Python prompt and built-in `repr()` function in most systems can choose the .red[shortest] of these and simply display `0.1`.
* Since all of these decimal values share the same approximation, any one of them could be displayed while still preserving the invariant `eval(repr(x)) == x`.

---
# `decimal` module

* Real numbers like 1.1 and 2.2 do not have exact representations in binary floating point. 
   * `1.1 + 2.2` is displayed as `3.3000000000000003` with binary floating point.
   * `0.1 + 0.1 + 0.1 - 0.3` is `5.5511151231257827e-017` with binary floating point.


* `decimal`: based on the number `10` (10진법의)


* "computers must provide an arithmetic that works in the same way as the arithmetic that .red[people] learn at school"
   * the `decimal` module is based on a floating-point model which was designed .red[with people in mind]


* The `decimal` module provides support for .purple[fast] .red[correctly-rounded] decimal floating point arithmetic. 


* Decimal numbers can be .red[represented exactly] with the `decimal` module
```python3
>>> Decimal('1.1') + Decimal('2.2')
Decimal('3.3')
```



---
# `decimal` module

* the decimal module has a user alterable precision (defaulting to .red[28] places) which can be .red[as large as needed] for a given problem.
* a new Decimal's significance is determined solely by the number of input digits. 
* Context precision and rounding only come into play .red[during arithmetic operations].

.font-14[
```python3
>>> from decimal import *
>>> getcontext().prec = 6
>>> Decimal(1) / Decimal(7)
Decimal('0.142857')
>>> getcontext().prec = 28
>>> Decimal(1) / Decimal(7)
Decimal('0.1428571428571428571428571429')
>>>
>>> getcontext().prec = 6
>>> Decimal('3.0')
Decimal('3.0')
>>> Decimal('3.1415926535')
Decimal('3.1415926535')
>>> Decimal('3.1415926535') + Decimal('2.7182818285')
Decimal('5.85987')
>>> getcontext().rounding = ROUND_UP
>>> Decimal('3.1415926535') + Decimal('2.7182818285')
Decimal('5.85988')
```
]

---
# The context for arithmetic

* The `decimal` module incorporates a notion of .red[significant places] so that `1.30 + 1.20` is `2.50`, with the trailing zero kept to indicate significance.


* Both binary and decimal floating point are implemented in terms of published standards. 


* While the built-in `float` type exposes only a modest portion of its capabilities, the `decimal` module exposes all required parts of the standard. 


* When needed, the programmer has .red[full control over rounding and signal handling]. This includes an option to enforce exact arithmetic by using exceptions to block any inexact operations.


* The .red[context for arithmetic] is an environment specifying precision, rounding rules, limits on exponents, flags indicating the results of operations, and trap enablers which determine whether signals are treated as exceptions.
   * https://docs.python.org/3/library/decimal.html#rounding-modes
   * https://docs.python.org/3/library/decimal.html#signals
---

# `round(number[, ndigits])`


* the built-in `round` function has confusing behavior when rounding `0.5`.

.font-14[
```python3
print(round(0.5)) # This evaluates to 0 - what!
print(round(1.5)) # And this will be 2 - so confusing!
```
]


* results are rounded to the closest multiple of `10` to the power minus ndigits; 
   * if two multiples are equally close, rounding is done toward the .red[even] choice
   * `0.5` is equally close to `0` and `1` -> even number `0` is returned
   * `1.5` is equally close to `1` and `2` -> even number `2` is returned
 
 
* Use our function .red[roundHalfUp] to fix this.

.font-14[
```python3
def roundHalfUp(d):
    # Round to nearest with ties going away from zero.
    # https://www.cs.cmu.edu/~112/notes/notes-variables-and-functions.html
    
    import decimal
    rounding = decimal.ROUND_HALF_UP
    return int(decimal.Decimal(d).to_integral_value(rounding=rounding))


print(roundHalfUp(0.5)) # Now this will always round 0.5 up (to 1)
print(roundHalfUp(1.5)) # This still rounds up too!
```
]

---
# `decimal` module

* Decimal instances can be constructed from `integers`, `strings`, `floats`, or `tuples`.


* Construction from an integer or a float performs an .red[exact/lossless conversion] of the value of that `integer` or `float` represented with binary floating point. 
   * a new Decimal's significance is determined solely by the number of input digits.

.font-14[
```python3
>>> getcontext().prec = 6  # Context precision and rounding are only for arithmetic operations
>>> Decimal(0.1)  # equivalent to Decimal(float('0.1'))
Decimal('0.1000000000000000055511151231257827021181583404541015625')
```
]

* If value is a `tuple`, it should have three components, 
   * a sign (`0` for positive or `1` for negative), a tuple of digits, and an exponent. 
   * `Decimal((0, (1, 4, 1, 4), -3))` returns `Decimal('1.414')`.
 

* A decimal number is immutable, and it has a sign, coefficient digits, and an exponent. 


* Special values: `Infinity`, `-Infinity`, `NaN`, `-0`, `+0`


https://docs.python.org/3/library/decimal.html

---
# The Exact Value of a `float` 

```python3
>>> x = 3.14159
>>> x.as_integer_ratio()
(3537115888337719, 1125899906842624)
>>>
>>> x == 3537115888337719 / 1125899906842624
True
>>>
>>> x.hex()
'0x1.921f9f01b866ep+1'
>>>
>>> x == float.fromhex('0x1.921f9f01b866ep+1')
True
```

https://docs.python.org/3/tutorial/floatingpoint.html

---
# `sum` vs. `math.fsum()`

* `math.fsum()` helps mitigate loss-of-precision during summation. 
   * It tracks “lost digits” as values are added onto a running total. 
   * the errors do not accumulate to the point where they affect the final total

```python3
>>> sum([0.1] * 10) == 1.0
False
>>> math.fsum([0.1] * 10) == 1.0
True
```

---
# remainder and division operators

```python3
>>> (-7) % 4
1
>>> Decimal(-7) % Decimal(4)
Decimal('-3')
```
```python3
>>> -7 // 4
-2
>>> Decimal(-7) // Decimal(4)
Decimal('-1')
```


---
# `fractions` module

* The fractions module provides support for rational number arithmetic.

```python3
class fractions.Fraction(numerator=0, denominator=1)
class fractions.Fraction(other_fraction)
class fractions.Fraction(float)
class fractions.Fraction(decimal)
class fractions.Fraction(string)
```

https://docs.python.org/3/library/fractions.html

---
# `fractions` module

.row[
.col-5[
.font-13[
```python3
>>> from fractions import Fraction
>>> Fraction(16, -10)
Fraction(-8, 5)
>>> Fraction(123)
Fraction(123, 1)
>>> Fraction()
Fraction(0, 1)
>>> Fraction('3/7')
Fraction(3, 7)
>>> Fraction(' -3/7 ')
Fraction(-3, 7)
>>> Fraction('1.414213 \t\n')
Fraction(1414213, 1000000)
>>> Fraction('-.125')
Fraction(-1, 8)
>>> Fraction('7e-6')
Fraction(7, 1000000)
>>> Fraction(2.25)
Fraction(9, 4)
>>> Fraction(1.1)
Fraction(2476979795053773, 2251799813685248)
>>> from decimal import Decimal
>>> Fraction(Decimal('1.1'))
Fraction(11, 10)
```
]
]
.col-7[
* Beware that `Fraction.from_float(0.1)` is not the same value as `Fraction(1, 10)`.

.font-13[
   ```python3
>>> from decimal import Decimal
>>> from fractions import Fraction

>>> Fraction.from_float(0.1)  # equivalent to Fraction(0.1)
Fraction(3602879701896397, 36028797018963968)

>>> (0.1).as_integer_ratio()
(3602879701896397, 36028797018963968)

>>> Decimal.from_float(0.1)  # equivalent to Decimal(0.1)
Decimal('0.1000000000000000055511151231257827021181583404541015625')

>>> format(Decimal.from_float(0.1), '.17')
'0.10000000000000001'

>>> Fraction(1,10)
Fraction(1, 10)

>>> Fraction(Decimal('0.1'))
Fraction(1, 10)
```
]
]
]

---
# Find the closest Fraction

```python3
limit_denominator(max_denominator=1000000)
```
* Finds and returns the closest `Fraction` to `self` that has denominator at most `max_denominator`. 


* This method is useful 
   * for finding rational approximations to a given floating-point number:
   * or for recovering a rational number that’s represented as a float:

.font-14[```python3
>>> from fractions import Fraction
>>> Fraction('3.1415926535897932').limit_denominator(1000)
Fraction(355, 113)
>>>
>>> from math import pi, cos
>>> Fraction(cos(pi/3))
Fraction(4503599627370497, 9007199254740992)
>>> Fraction(cos(pi/3)).limit_denominator()
Fraction(1, 2)
>>> Fraction(1.1).limit_denominator()
Fraction(11, 10)
```
]

---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag, The MIT Press
* CMU 15-112: Fundamentals of Programming and Computer Science, Carnegie Mellon University