layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Repetition Structures

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---

# Repetion Structures

* Often have to write code that performs the same task multiple times
    * Disadvantages to duplicating code
        * Makes program large
        * Time consuming to type in code
        * May need to be corrected in many places


* Repetition structure makes computer repeat included code as necessary
    * condition-controlled loops (`while`)
    * count-controlled loops (`for`)
    
---

# `while` Loop

* condition-controlled loop

```python3
while condition:
    statements
```

* While condition is true, do something
    * .red[condition] tested for true or false value
    * .red[statements] repeated as long as condition is true
    
* In flowchart, line goes back to previous part

.center[<img src="https://user-images.githubusercontent.com/39995503/91706842-eadc3a80-ebb9-11ea-8423-997d3e8643d2.png" width=300>]

---

# `while` Loop

* In order for a loop to stop executing, something has to happen .red[inside0 the loop to make the condition .red[false]
* .red[Iteration]: one execution of the body of a loop
* `while` loop is known as a .red[pretest] loop
    * Tests condition before performing an iteration
    * Will never execute if condition is false to start with
    * Requires performing some steps prior to the loop

---

# `while` Loop

```python
keep_going = 'y'

# Calculate a series of commissions.
while keep_going == 'y':
    # Get a salesperson's sales and commission rate.
    sales = float(input('Enter the amount of sales: '))
    comm_rate = float(input('Enter the commission rate: '))

    # Calculate the commission.
    commission = sales * comm_rate

    # Display the commission.
    print('The commission is $', \
    format(commission, ',.2f'), sep='')

    # See if the user wants to do another one.
    keep_going = input('Do you want to calculate another ' + \
                       'commission (Enter y for yes): ')
```

---

# Infinite Loops

* Loops must contain within themselves a way to terminate
    Something inside a while loop must eventually make the condition false


* Infinite loop: loop that does not have a way of stopping
    * Repeats until program is interrupted
    * Occurs when programmer forgets to include .red[stopping code] in the loop

```python3

count = 1;
while count > 0:
    print("iteration count = ", count);
    count = count + 1
```

---

# `for` Loop

* .red[count-controlled loop] iterates a specific number of times


* Use a `for` statement to write a count-controlled loop 
    * Designed to work with .red[sequence] of data items
    * Iterates once for each item in the sequence

```python3
for variable in [val1, val2, etc]:
    statements
```

.center[
<img src="https://user-images.githubusercontent.com/39995503/91708578-7b1b7f00-ebbc-11ea-9199-158e2514614d.png" width=300>
]

---

# `for` Loop

* .red[count-controlled loop] iterates a specific number of times

```python3
>>> for name in ['John', 'James', 'Jane']:
...     print(name)
... 
John
James
Jane

```
```python3
>>> # Measure some strings:
... words = ['cat', 'window', 'defenestrate']  # create a list object
>>> for w in words:
...     print(w, len(w))
...
cat 3
window 6
defenestrate 12
```
---
# `range` Class with `for` Loops

* The `range` class simplifies the process of writing a `for` loop
* `range` type object is an .red[iterable] object
    * Iterable object contains a .red[sequence] of values that can be iterated over
    * It is suitable as a target for functions and constructs that expect something from which they can obtain successive items until the supply is exhausted.

```python3
class range(stop)
class range(start, stop[, step])
```
   * If the `step` argument is omitted, it defaults to `1`. 
   * If the `start` argument is omitted, it defaults to `0`. 
   * `stop` is not included in the sequence
    
   * For a positive `step`, the contents of a `range` r are determined by the formula `r[i] = start + step*i` where `i >= 0` and `r[i] < stop`.
   * For a negative `step`, the contents of the `range` are still determined by the formula `r[i] = start + step*i`, but the constraints are `i >= 0` and `r[i] > stop`.
   
---

# `range` Class with `for` Loops

```python3
for num in [1, 2, 3, 4, 5]:
    print(num, end=' ') 
for num in range(1,5):
    print(num, end=' ')
# prints 1 2 3 4 5

for num in range(5):
    print(num, end=' ')
# prints 0 1 2 3 4

for num in range(1, 10, 2):
    print(num, end=' ')
# prints 1 3 5 7 9

for num in range(0, -10, -2):
    print(num, end=' ')
# prints 0 -2 -4 -6 -8

for num in range(0):
    print num
# prints nothing
```

---

# `for` Loop Example

```python
# Print the table headings.
print('Number\tSquare')
print('--------------')

# Print the numbers 1 through 10
# and their squares.

for number in range(1, 11):
    square = number**2
    print(number, '\t', square)
```

---

# `for` Loop Example

```python
print('This program displays a list of numbers')
print('(starting at 1) and their squares.')
end = int(input('How high should I go? '))

# Print the table headings.
print('Number\tSquare')
print('--------------')

# Print the numbers 1 through 10
# and their squares.

for number in range(1, end+1):
    square = number**2
    print(number, '\t', square)
```

---
# Calculating a Running Total

* Programs often need to calculate a total of a series of numbers
    * Typically include two elements:
       * A loop that reads each number in series
       * An .red[accumulator] variable
    * Known as program that keeps a running total:  accumulates total and reads in series
    * At end of loop, accumulator will reference the total
