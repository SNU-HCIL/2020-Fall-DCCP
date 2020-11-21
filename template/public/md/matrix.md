layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Numbers and Matrix

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---

# `round(number[, ndigits])`


* the built-in `round` function has confusing behavior when rounding 0.5.

.font-14[
```python3
print(round(0.5)) # This evaluates to 0 - what!
print(round(1.5)) # And this will be 2 - so confusing!
```
]


* results are rounded to the closest multiple of 10 to the power minus ndigits; 
   * if two multiples are equally close, rounding is done toward the .red[even] choice
   * 0.5 is equally close to 0 and 1 -> even number 0 is returned
   * 1.5 is equally close to 1 and 2 -> even number 2 is returned
 
 
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

* `decimal`: based on the number `10` (10진법의)

* "computers must provide an arithmetic that works in the same way as the arithmetic that .red[people] learn at school"

* the decimal module is based on a floating-point model which was designed .red[with people in mind]
* The decimal module provides support for .purple[fast] .red[correctly-rounded] decimal floating point arithmetic. 
* It offers several advantages over the `float` datatype:
   * Decimal numbers can be .red[represented exactly] with enough precision, but not in binary floating point representation.
   * `1.1 + 2.2` is displayed as `3.3000000000000003` with binary floating point.
   * `0.1 + 0.1 + 0.1 - 0.3` is `5.5511151231257827e-017` with binary floating point.

---
# `decimal` module

* Unlike hardware based binary floating point, the decimal module has a user alterable precision (defaulting to .red[28] places) which can be .red[as large as needed] for a given problem:
```python3
>>> from decimal import *
>>> getcontext().prec = 6
>>> Decimal(1) / Decimal(7)
Decimal('0.142857')
>>> getcontext().prec = 28
>>> Decimal(1) / Decimal(7)
Decimal('0.1428571428571428571428571429')
```

---
# `decimal` module

* Decimal instances can be constructed from `integers`, `strings`, `floats`, or `tuples`.

* Construction from an integer or a float performs an exact conversion of the value of that `integer` or `float` represented with binary floating point. 

* A decimal number is immutable. 
* It has a sign, coefficient digits, and an exponent. To preserve significance, the coefficient digits do not truncate trailing zeros. 

* Decimal numbers include special values such as `NaN` which stands for “Not a number”, positive and negative `Infinity`, and `-0`:

https://docs.python.org/3/library/decimal.html

---
# `decimal` module

* If value is a tuple, it should have three components, 
   * a sign (0 for positive or 1 for negative), a tuple of digits, and an integer exponent. 
   * `Decimal((0, (1, 4, 1, 4), -3))` returns `Decimal('1.414')`.
 
* If value is a `float`, the binary floating point value is .red[losslessly converted] to its exact decimal equivalent. 
   * This conversion can often require 53 or more digits of precision. 

```python3
>>> Decimal('1.1')
Decimal('1.1')
>>> Decimal(float('1.1'))
Decimal('1.100000000000000088817841970012523233890533447265625')
>>> Decimal(1.1)
Decimal('1.100000000000000088817841970012523233890533447265625') 
```


---
# Fraction

https://docs.python.org/3/library/fractions.html
https://docs.python.org/3/tutorial/floatingpoint.html

---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag, The MIT Press
* CMU 15-112: Fundamentals of Programming and Computer Science, Carnegie Mellon University