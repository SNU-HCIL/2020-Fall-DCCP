layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Linear Algebra

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---
# Matrix

* A matrix is a rectangular array of numbers (or other mathematical objects) for which operations such as addition and multiplication are defined.

* any doubly subscripted array of elements arranged in rows and columns

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/599e7d283086f53898bbe2c0f48b6cfcdcda019e" width=700/>

* A is an `m`x`n` matrix, with `m` .purple[rows] and `n` .purple[columns]


* Matrices are usually symbolized using upper-case letters (such as A in the examples above)
   * while the corresponding lower-case letters, with two subscript indices (e.g., `a`<sub>11</sub>, or `a`<sub>1,1</sub>), represent the entries.
---
# Matrix

* Row Vector
* Column Vector 

<img src="https://user-images.githubusercontent.com/39995503/99903187-2cd2d380-2d06-11eb-98d9-63c518533af0.png" width=300/>

---
# Main Types of Matrix

<img src="https://user-images.githubusercontent.com/39995503/99903513-4ecd5580-2d08-11eb-9792-5d8cc5a64661.png" width=400/>

.blue[Identity matrix]

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/6931c1e33e3f9c90392237ce0e1a42bd3e6c71ea"/>


---
# Basic Operations

* Addition  

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/9e600aa691a93ceb33f0fdac290002d1391d6688"/>

* Scalar multiplication  

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/cf7fe1075c8c575225e74096007bef9205c88964"/>

* Transposition  

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/51f6dba024e104b412ed0562163ca9a11fcb9463"/>

---
# Matrix multiplication

* multiply each row by each column

* If `A` is an `m`-by-`n` matrix and `B` is an `n`-by-`p` matrix, then their matrix product `AB` is the `m`-by-`p` matrix:

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/c903c2c14d249005ce9ebaa47a8d6c6710c1c29e"/>

For exmaple, <img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/8435ba88efca5a73e7d1b122bb19f99ef136d71e"/>

<img src="https://upload.wikimedia.org/wikipedia/commons/e/e5/MatrixMultiplication.png" width=350/>


---
# Creating a 2D Lists

* Matrix is represented as a 2D `list` in Python


* Static Allocation

.font-14[
```python3
a = [ [ 2, 3, 4 ] , [ 5, 6, 7 ] ]
print(a)
```
]

* Dynamic Allocation (using shallow copy -> Wrong!)

.font-14[
```python
# Try, and FAIL, to create a variable-sized 2d list
rows = 3
cols = 2

a = [ [0] * cols ] * rows # Error: creates shallow copy
                          # Creates one unique row, the rest are aliases!

print("This SEEMS ok.  At first:")
print("   a =", a)

a[0][0] = 42
print("But see what happens after a[0][0]=42")
print("   a =", a)
```
]

https://www.cs.cmu.edu/~112/notes/notes-2d-lists.html

---
# Creating 2D Lists

* Dynamic Allocation (append rows -> Right!)

.font-14[

```python
# Create a variable-sized 2d list
rows = 3
cols = 2

a = []
for row in range(rows):
    a += [[0]*cols]

print("This IS ok.  At first:")
print("   a =", a)

a[0][0] = 42
print("And now see what happens after a[0][0]=42")
print("   a =", a)
```
]

https://www.cs.cmu.edu/~112/notes/notes-2d-lists.html
---
# Creating 2D Lists

.row[
.col-6.font-14[

* use a list comprehension

```python
rows = 3
cols = 2

#This is what's called a "list comprehension"
a = [ ([0] * cols) for row in range(rows) ]

print("This IS ok.   At first:")
print("   a =", a)

a[0][0] = 42
print("And now see what happens after a[0][0]=42")
print("   a =", a)
```
]
.col-6.font-14[

* define a function

```python
def make2dList(rows, cols):
    return [ ([0] * cols) for row in range(rows) ]

rows = 3
cols = 2

a = make2dList(rows, cols)

print("This IS ok.  At first:")
print("   a =", a)

a[0][0] = 42
print("And now see what happens after a[0][0]=42")
print("   a =", a)
```
]
]

https://www.cs.cmu.edu/~112/notes/notes-2d-lists.html

---
# Getting 2D List Dimensions

```python
# Create an "arbitrary" 2d List
a = [ [ 2, 3, 5] , [ 1, 4, 7 ] ]
print("a = ", a)

# Now find its dimensions
rows = len(a)
cols = len(a[0])
print("rows =", rows)
print("cols =", cols)
```
https://www.cs.cmu.edu/~112/notes/notes-2d-lists.html

---
# Copying and Aliasing 2d Lists

.row[
.col-6.font-14[

* using `copy.copy` (shallow copy) -> Wrong!

```python
import copy

# Create a 2d list
a = [ [ 1, 2, 3 ] , [ 4, 5, 6 ] ]

# Try to copy it
b = copy.copy(a) # Error:  creates shallow copy

# At first, things seem ok
print("At first...")
print("   a =", a)
print("   b =", b)

# Now modify a[0][0]
a[0][0] = 9
print("But after a[0][0] = 9")
print("   a =", a)
print("   b =", b)
```
]
.col-6.font-14[

* using `copy.deepcopy` -> Right!

```python
import copy

# Create a 2d list
a = [ [ 1, 2, 3 ] , [ 4, 5, 6 ] ]

# Try to copy it
b = copy.deepcopy(a) # Correct!

# At first, things seem ok
print("At first...")
print("   a =", a)
print("   b =", b)

# Now modify a[0][0]
a[0][0] = 9
print("And after a[0][0] = 9")
print("   a =", a)
print("   b =", b)
```
]
]

https://www.cs.cmu.edu/~112/notes/notes-2d-lists.html
---
# deepcopy preserves aliases!

.row[
.col-6.font-14[

* Limitations of `copy.deepcopy`

```python
a = [[0]*2]*3 # makes 3 shallow copies of (aliases of) the same row
a[0][0] = 42  # appears to modify all 3 rows
print(a)      # prints [[42, 0], [42, 0], [42, 0]]

# now do it again with a deepcopy

import copy
a = [[0]*2]*3        # makes 3 shallow copies of the same row
a = copy.deepcopy(a) # meant to make each row distinct
a[0][0] = 42         # so we hope this only modifies first row
print(a)             # STILL prints [[42, 0], [42, 0], [42, 0]]

# deepcopy preserves any already-existing aliases perfectly!
# best answer: don't create aliases in the first place, unless you want them.
```
]
.col-6.font-14[

* alias-breaking `deepcopy`

```python
# Advanced: now one more time with a simple deepcopy alternative that does
# what we thought deepcopy did...
# NOTE: this uses recursion. We'll go over how that works in the future.

import copy

def myDeepCopy(a):
    if isinstance(a, list):
        return [myDeepCopy(element) for element in a]
    else:
        return copy.copy(a)

a = [[0]*2]*3     # makes 3 shallow copies of the same row
a = myDeepCopy(a) # once again, meant to make each row distinct
a[0][0] = 42      # so we hope this only modifies first row
print(a)          # finally, prints [[42, 0], [0, 0], [0, 0]]

# now all the aliases are gone!   
```
]
]

https://www.cs.cmu.edu/~112/notes/notes-2d-lists.html

---
# Tracing a 2D List

```python
def sumMatrix(m):
   sum = 0
   for row in range(len(m)):
      for col in range(len(m[row])):
         sum = sum + m[row][col]
   return sum

matrix = [ [ 1, 2, 3, 4 ],
           [ 5, 6, 7, 8 ],
           [ 9, 10, 11, 12 ]]

print(sumMatrix(matrix))

# Python style code!
print(sum([elem for row in matrix for elem in row]))
```

---
# Vector Operations in Python

* add 2D vectors 
  * [u<sub>1</sub>, v<sub>1</sub>] + [u<sub>2</sub>, v<sub>2</sub>] = [u<sub>1</sub> + u<sub>2</sub>, v<sub>1</sub> + v<sub>2</sub>]

```python3
# resV = x + y + z
>>> x = [1, 2]
>>> y = [2, 3]
>>> z = [3, 4]
>>> [e for e in zip(x, y, z)]
[(1, 2, 3), (2, 3, 4)]
>>> resV = [sum(e) for e in zip(x, y, z)]
>>> resV
[6, 9]
>>> 
```

---
# Vector Operations in Python

* add more vectors 

.row[
.col-6.font-15[
```python
def vectorAddition(*args):
    print(args)
    return [sum(t) for t in zip(*args)]

x = [1, 2]
y = [2, 3]
z = [3, 4]
w = [4, 5]

resV = vectorAddition(x, y, z, w)
print(resV)
```
]
.col-6[

result:
```python3
([1, 2], [2, 3], [3, 4], [4, 5])
[10, 14]
```
]
]

---
# Vector Operations in Python

* add more vectors 

.row[
.col-6.font-15[
```python
def vectorAddition(*args):
    print(args)
    return [sum(t) for t in zip(*args)]

rowVectors = [[1, 2], [2, 3], [3, 4], [4, 5]]

resV = vectorAddition(*rowVectors)
print(resV)
```
]
.col-6[

result:
```python3
([1, 2], [2, 3], [3, 4], [4, 5])
[10, 14]
```
]
]

---
# Vector Operations in Python

* Scalar multiplication  

α x

.font-15[
```python
x = [1,2,3]
alpha = 3
resV = [alpha * val for val in x]
print(resV)
```
]

α (x + y) = α x + α y

.font-15[
```python
x = [1, 2, 3]
y = [4, 5, 6]
alpha = 3
print([e for e in zip(x, y)])

resV = [alpha * sum(e) for e in zip(x, y)]
print(resV)
```
]

---
# Matrix Operations in Python

* add two matrixes

```python
matrixA = [[3, 6], [4, 5]]
matrixB = [[5, 8], [6, 7]]

print(list(zip(matrixA, matrixB)))
# [([3, 6], [5, 8]), ([4, 5], [6, 7])] 

print([rows for rows in zip(matrixA, matrixB)])
# [([3, 6], [5, 8]), ([4, 5], [6, 7])] 

print([[pair for pair in zip(*rows)] for rows in zip(matrixA, matrixB)])
# [[(3, 5), (6, 8)], [(4, 6), (5, 7)]] 

resM = [[sum(pair) for pair in zip(*rows)] for rows in zip(matrixA, matrixB)]
print(resM)
# [[8, 14], [10, 12]] 
```

---
# Matrix Operations in Python

* matrix equality testing

.font-15[
```python
matrixA = [[1,2], [3,4]]
matrixB = [[1,2], [3,4]]
print([pair[0] == pair[1] for rows in zip(matrixA, matrixB) for pair in zip(*rows)])
print(all([pair[0] == pair[1] for rows in zip(matrixA, matrixB) for pair in zip(*rows)]))

matrixA = [[1,2,3], [3,4,5]]
matrixB = [[1,2,3], [3,4,5]]
print([pair[0] == pair[1] for rows in zip(matrixA, matrixB) for pair in zip(*rows)])
print(all([pair[0] == pair[1] for rows in zip(matrixA, matrixB) for pair in zip(*rows)]))

matrixA = [[1,2,3], [3,4,5]]
matrixB = [[1,2,5], [7,4,5]]
print([pair[0] == pair[1] for rows in zip(matrixA, matrixB) for pair in zip(*rows)])
print(all([pair[0] == pair[1] for rows in zip(matrixA, matrixB) for pair in zip(*rows)]))
```
]

---
# `all(iterable)` and `any(iterable)`

* `all(iterable)`
   * Return `True` if .red[all] elements of the iterable are true (or if the iterable is empty). 

```python3
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True
```

* `any(iterable)`
   * Return `True` if .red[any] element of the iterable is true. If the iterable is empty, return `False`. 

```python3
def any(iterable):
    for element in iterable:
        if element:
            return True
    return False
```

---
# Matrix Operations in Python

* transpose a matrix

```python3
>>> matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
]
>>> list(zip(*matrix))  # unpacking and zip
[(1, 5, 9), (2, 6, 10), (3, 7, 11), (4, 8, 12)]
>>>
>>> result1=[list(e) for e in zip(*matrix)]  # list comprehension
>>> result1
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
>>> result2=[[t for t in e] for e in zip(*matrix)] # list comprehension
>>> result2
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```
---
# Matrix Operations in Python

* multiply two matrixes

.font-15[
```python
matrixA = [[1, 2, 3], 
           [4, 5, 6]] # 2X3 matrix
matrixB = [[7, 8], 
           [9, 10], 
           [11, 12]] # 3X2 matrix

resM = [[sum(a*b for a,b in zip(rowA, colB)) for colB in zip(*matrixB)] for rowA in matrixA]
print(resM)
```
]

1. for each row vector in matrixA (`for rowA in matrixA`)
2. for each column vector in matrixB (`for colB in zip(*matrixB)`)
3. for each pair of elements at the same index from the two vectors   
   (`for a,b in zip(rowA, colB)`)
4. get the summation (`sum(a*b ... `)

---
# `numnpy` package

.row[
.col-6[

```python3
import numpy as np

matrixA = [[1, 2, 3], 
           [4, 5, 6]] # 2X3 matrix
matrixB = [[7, 8], 
           [9, 10], 
           [11, 12]] # 3X2 matrix

result = np.matmul(matrixA, matrixB)
# result = np.dot(matrixA, matrixB)
print(result)
# prints "[[ 58  64]
#          [139 154]]"
```
]
.col-6[
```python3
import numpy as np

matrixA = [[1, 2, 3], 
           [4, 5, 6]] # 2X3 matrix
matrixB = [[7, 8], 
           [9, 10], 
           [11, 12]] # 3X2 matrix

npmA=np.array(matrixA)
npmB=np.array(matrixB)

result = npmA@npmB

print(result)
# prints "[[ 58  64]
#          [139 154]]"
```
]
]

https://numpy.org/

---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag, The MIT Press
* CMU 15-112: Fundamentals of Programming and Computer Science, Carnegie Mellon University