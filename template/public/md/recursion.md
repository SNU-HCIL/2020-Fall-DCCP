layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Recursion

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---
# Concept of Recursion

* Recursive function: a function that calls itself


* Recursive function must have a way to control the number of times it repeats
   * Usually involves an `if-else` statement which defines 
     * (**BASE case**) when the function should return a value and 
     * (**RECURSIVE case**) when it should call itself


* .red[Depth of recursion]: the number of times a function calls itself

```python3
# 1! = 1          (base case)
# n! = n x (n-1)! (recursive case)

def factorial(n):
    if n == 1:    # base case
        return 1
    else:         # recursive case
        return n * factorial(n-1)
```

---
# Call Stack or Stack Frames

```python3
# 1! = 1          (base case)
# n! = n x (n-1)! (recursive case)

def factorial(n):
    if n == 1:    # base case
        return 1
    else:         # recursive case
        return n * factorial(n-1)
```

.center[<img src="https://user-images.githubusercontent.com/39995503/98465226-23784000-220b-11eb-9a7a-7ab3f5db1a73.png" width=800/>]

---
# Using Recursion 

* Since each call to the recursive function .red[reduces] the problem:
   * Eventually, it will get to the base case which does not require recursion, and the recursion will stop
   
   
* Usually the problem is reduced by making one or more parameters smaller at each function call

---
# Pros and Cons

* Recursion is a powerful tool for solving repetitive problems


* Recursion is never required to solve a problem
  * Any problem that can be solved recursively can be solved iteratively with a loop


* Recursive algorithms usually less efficient than iterative ones
  * Due to .red[overhead of function calls]


---
# Direct and Indirect Recursion

* .red[Direct] recursion: when a function directly calls itself
   * `factorial` is of direct recursion


* .red[Indirect] recursion: 
   * when function `A` calls function `B`, which in turn calls function `A`


---
# Summing a list

```python
def sumlist(items):
   if items == []:
       return 0
   else:
       return items[0] + sumlist(items[1:])

result = sumlist([1,2,3,4,5])
print(result)
```

---
# The Fibonacci Series

* 0,1,1,2,3,5,8,13,21,34,55,89,144, ...

* Fibonacci series: has two base cases
```
if n = 0 then Fib(n) = 0
if n = 1 then Fib(n) = 1
if n > 1 then Fib(n) = Fib(n-1) + Fib(n-2)
```

<img src="https://upload.wikimedia.org/wikipedia/commons/d/db/34%2A21-FibonacciBlocks.png" width=250/>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/2e/FibonacciSpiral.svg/2880px-FibonacciSpiral.svg.png" width=250/>
<img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/GoldenSpiralLogarithmic_color_in.gif" width=200/>


The Fibonacci spiral: an approximation of the golden spiral created by drawing circular arcs connecting the opposite corners of squares in the Fibonacci tiling (from Wikipedia)

---
# The Fibonacci Series

```python
def fib(n):
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        return fib(n-1) + fib(n-2)

result = fib(5)
print(result)
```

---
# Recursive Call Tree

<img src="https://user-images.githubusercontent.com/39995503/98466810-4576c000-2215-11eb-9857-4625244878da.png" width=700/>

* evaluation sequence: .red[depth-first] trace of this tree
   * try "Visualize" in the previous slide
   * you can draw the change of stack frames

---
# The Towers of Hanoi

* Mathematical game commonly used to illustrate the power of recursion
   * Uses three pegs and a set of discs in decreasing sizes
 
 
* Goal of the game: move all discs from one peg to another peg
   * Only one disc can be moved at a time
   * A disc cannot be placed on top of a smaller disc
   * All discs must be on a peg except while being moved

.center[<a href="http://towersofhanoi.info/Animate.aspx"> <img src="https://user-images.githubusercontent.com/39995503/98466044-612b9780-2210-11eb-9d39-787fc96d5d2a.png" width=400/> </a>]
.center[http://towersofhanoi.info/Animate.aspx]

<p style="font-size:12px;">
The game is based on a legend where a group of monks in a temple in Hanoi have a similar set of pegs with 64 discs. The job of the monks is to move the discs from the first peg to the third peg. According to the legend, when the monks have moved all of the discs from the first peg to the last peg, the world will come to an end. If the monks move the discs at a rate of 1 per second, it will take them approximately 585 billion years to move all 64 discs!
</p>

---
# The Towers of Hanoi

* Problem statement: move `n` discs from peg 1 (`from_peg`) to peg 3 (`to_peg`) using peg 2 as a temporary peg


* Recursive solution:
   * If `n` == 1: 
      * Move disc from from_peg to to_peg
   * Otherwise:
      * Move `n-1` discs from peg 1 to peg 2, using peg 3
      * Move remaining disc from peg 1 to peg 3
      * Move `n-1` discs from peg 2 to peg 3, using peg 1

---
# The Towers of Hanoi

```python
def move_discs(num, from_peg, to_peg, temp_peg):
   if num == 1:
       print('Move a disc from peg', from_peg, 'to peg', to_peg)
   else:
       move_discs(num - 1, from_peg, temp_peg, to_peg)
       print('Move a disc from peg', from_peg, 'to peg', to_peg)
       move_discs(num - 1, temp_peg, to_peg, from_peg)

# Set up some initial values.
num_discs = 3
from_peg = 1
to_peg = 3
temp_peg =2

move_discs(num_discs, from_peg, to_peg, temp_peg)
print('All the pegs are moved!')
```

---
# Recursive vs. Iterative

* Reasons not to use recursion:
   * Less efficient: entails function calling overhead that is not necessary with a loop
   
   
* Usually a solution using a loop is .red[more evident] than a recursive solution
   * Recursive function is usually .red[more succint] than the iterative
   * Some problems are more easily solved with recursion than with a loop
   * Example: .red[Fibonacci], where the mathematical definition lends itself to recursion

---
# Maximum Recursion Depth

* Python stops it at `1000` calls, the default “maximum recursion depth.”

.row[
.col-6[
```python
def reverse(s):
    '''reverse the string s'''
    return reverse(s[1:]) + s[0]

reverse('Python')
```
]
.col-6[

* We get this exception:
.font-12[
```
Traceback (most recent call last):
  File "/Users/jinwook/Documents/liskov.py", line 5, in <module>
    reverse('Python')
  File "/Users/jinwook/Documents/liskov.py", line 3, in reverse
    return reverse(s[1:]) + s[0]
  File "/Users/jinwook/Documents/liskov.py", line 3, in reverse
    return reverse(s[1:]) + s[0]
  File "/Users/jinwook/Documents/liskov.py", line 3, in reverse
    return reverse(s[1:]) + s[0]
  [Previous line repeated 1022 more times]
RecursionError: maximum recursion depth exceeded
```
]
]
]

--

```python3
def reverse(s):
    '''reverse the string s'''
    if s == "":
        return s
    else: 
        return reverse(s[1:]) + s[0]

```

---
# Maximum Recursion Depth

* Python stops it at `1000` calls, the default “maximum recursion depth.”


* to prevent **.red[stack overflow]**
   * if call stack keeps growing, the program crashes

```python3
>>> import sys
>>> sys.getrecursionlimit()
1000
>>> sys.setrecursionlimit(1500)
```

---
# Iterative Versions

* Recursion is never required to solve a problem
  * Any problem that can be solved recursively can be solved with a loop

```python3
def factorial(n):
    result = 1
    for i in range1, n+1):
        result = result * i
    return result
```

```python3
def fib(n):
    x = 0
    next_x = 1
    for i in range(1, n+1):
        x, next_x = next_x, x + next_x
        
    return x
```

---
# Tail Recursion

* A recursive function is .red[tail recursive] when recursive call is the .red[last] thing executed by the function.

* We can convert non tail recursive to tail recursive

.row[
.col-6[
```python
# not tail recursive 
def factorial(n):
    if n == 1:    # base case
        return 1
    else:         # recursive case
        return n * factorial(n-1)

print(factorial(5))
```
]
.col-6[
```python
# tail recursive 
def factorial(n, result = 1):
    if n == 1:    # base case
        return result
    else:         # recursive case
        return factorial(n-1, n*result)

print(factorial(5))
```
]
]

---
# Tail-call Optimization

* The tail recursive functions can be optimized -> .red[Tail-call optimization]
   * We can remove the recursion -> save memory, run faster
   * Modern compilers supports tail-call optimization
   
   
* Tail-call optimization is not supported in Python, 
   * but we can apply it by changing the code inside the function


.row[
.col-6[
.font-14[
```python
# tail recursive 
def factorial(n, result = 1):
    if n == 1:    # base case
        return result
    else:         # recursive case
        return factorial(n-1, n*result)

print(factorial(5))
```
]
]
.col-6[
.font-14[
```python3
# tail recursion removed! 
# this code doesn't work; no goto in Python
def factorial(n, result=1):
    START: 
    if n == 0:
        return result
    else:
        #  return factorial(n-1, n*result)
        result = n * result
        n = n - 1
        goto START

print(factorial(5))
```
]
]
]

---
# Tail-call Optimization

* The tail recursive functions can be optimized 

.row[
.col-6[
.font-14[
```python3
# tail recursion removed! 
# this code doesn't work; no goto in Python
def factorial(n, result=1):
    START: 
    if n == 0:
        return result
    else: 
        # return factorial(n-1, n*result)
        result = n * result
        n = n - 1
        goto START

print(factorial(5))
```
]

* This doesn't work!
   * no `goto` in Python
]
.col-6[
```python
# tail recursion removed! 
def factorial(n, result=1):
    while True:
        if n == 0:
            return result
        else:
            result = n * result
            n = n - 1
            
print(factorial(5))
```
]
]

---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag