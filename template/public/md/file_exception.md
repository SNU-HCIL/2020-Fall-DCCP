layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Files I/O and Exception Handling

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---

# File System and File Handle

* Each OS has its own file system for creating and accessing files
   * controls how data is stored and retrieved
   * organizes and manages files on storage


* Python access files through a .red[file handle] (.purple[a variable referencing a file object])
   * .green[operating-system independence]
   
```python3
nameHandle = open('kids', 'w')
```

   * instructs the OS to create a file with the name `kids`, and
   * returns a .red[file handle] for that file (opened for .purple[writing])


* It is important to .red[close] the file when finished using it

```python3
nameHandle.close()
```
---
# Specifying the Location of a File

* in Python script (script mode)
   * If `open` function receives a filename that does not contain a path, assumes that file is .red[in same directory as the program] (i.e., your Python script file)


* in Python shell (interactive mode)
   * In Windows: in a directory where the Python shell is installed
   * In OS-X: it is usually '/Users/username/Documents' where `username` is your user ID


* If program is running and a file is created, it is created .red[in the same directory as the program]
  * Can specify alternative path and file name in the `open` function argument
  * Prefix the path string literal with the letter `r`


---
# Specifying the Location of a File

* Check and Change the .red[working directory]

```python3
import os

print(os.getcwd()) # prints '/Users/jinwook/Documents'
os.chdir(r'/Users/jinwook/Desktop')  # on my Mac
print(os.getcwd()) # prints '/Users/jinwook/Desktop'

f = open('foo.txt', 'w')
f.write('test\n')
f.close( )
```

* Specifying a full absolute path

```python3
>>> myfile = open("C:\\Users\\hjkim\\Desktop\\foo.txt", "w+")
>>> myfile.write('test\n')
5
>>> myfile.close( )
```

---
# Open Mode of File

```python3
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, 
     closefd=True, opener=None)
```
* Open a file and return a corresponding file object. 
* If the file cannot be opened, an `OSError` is raised. 
* https://docs.python.org/3/library/functions.html#open


|&nbsp;&nbsp;&nbsp;File Access Mode&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;I/O Mode&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;File Open Mode&nbsp;&nbsp;&nbsp;| 
|:--------:|:-----------------------------:|:---------------------------:|
|  .red[**r**]       |                        | rt&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;rb          | 
|  w       |                        | wt&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;wb              |
|  x       |                        | xt&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;xb              |
|  a       |        .red[**t**]               | at&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ab              |
|  r+      |        b               | r+t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;r+b            | 
|  w+      |                        | w+t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w+b           |
|  x+      |                        | x+t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;x+b           |
|  a+      |                        | a+t&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;a+b           | 

---
# Open Mode of File

* `'r'` : open for .red[reading] (default). raise `FileNotFoundError` if the file is not there
* `'w'` : open for .red[writing], .green[truncating the file first]. create one if the file is not there
* `'x'` : open for .red[exclusive creation]. raise `FileExistsError` if the file exists 
* `'a'` : open for writing, .red[appending] to the end. create one if the file is not there
* `'b'` : .red[binary] mode
* `'t'` : .red[text] mode (default)
* `'+'` : open for updating (reading and writing)


* `'r+'` : open for .red[reading]. raise `FileNotFoundError` if the file is not there. 
   * .blue[writing] is also possible (.green[but without truncating the file])
* `'w+'` : open for .red[writing], truncating the file first. create one if the file is not there
   * .blue[reading] is also possible
* `'x+'` : open for .red[exclusive creation]. raise `FileExistsError` if the file exists
   * .blue[reading] is also possible
* `'a+'` : open for writing, .red[appending] to the end. create one if the file is not there
   * .blue[reading] is also possible
---
# File Write in `'w'` and `'a'` mode

.row[
.col-7[
```python3
f = open ('foo.txt', 'w')
for i in range(1, 4):
   data = 'This is line %d. \n' % i
   f.write(data)

f.close()
```

```python3
f = open ('foo.txt', 'a')
for i in range(4, 7):
   data = 'This is line %d. \n' % i
   f.write(data)

f.close()
```
]
.col-5[

* after writing in `'w'` mode, `foo.txt`

```python3
This is line 1.\n
This is line 2.\n
This is line 3.\n
```

* after writing in `'a'` mode, `foo.txt`

```python3
This is line 1.\n
This is line 2.\n
This is line 3.\n
This is line 4.\n
This is line 5.\n
This is line 6.\n
```
]
]

---
# Reading from a File

* For reading lines from a file, you can .red[loop over the file object] 


* This is .green[memory efficient], .green[fast], and leads to .green[simple code]
     
```python3
f = open ('foo.txt', 'r')
for line in f:            # iterate over each line (as a string)
    print(line, end='')
f.close()
```

---
# Reading from a File

```python3
f = open ('foo.txt', 'r')
lines = f.readlines() #read all lines and return a list with the lines
for line in lines:
    print(line, end='')
f.close()
```

```python3
f = open ('foo.txt', 'r')
while True:
   line = f.readline()
   if not line:        # line is empty string at the end of the file
      break
   print(line, end='')
f.close()

```

---
# `readlines()` vs. `read()`

* `readlines()`: returns a list each element of which is one line of the file
```python3
>>> f = open('foo.txt', 'r')
>>> lines = f.readlines()
>>> lines
['This is line 1.\n', 'This is line 2.\n', 'This is line 3.\n']
>>> f.close()
>>> 
```

* `read()`: returns a single string (concatenating all lines of the file)
```python3
>>> f = open('foo.txt', 'r')
>>> result = f.read()
>>> result
'This is line 1.\nThis is line 2.\nThis is line 3.\n'
>>> f.close()
>>> 
```
---
# `close()`

* It is important to .red[close] the file when finished using it

```python3
nameHandle.close()
```

* If you’re not using the `with` keyword, then you should call `f.close()`
   * to close the file and immediately free up any system resources used by it


* If you don’t explicitly `close` a file, 
   * Python’s garbage collector will eventually destroy the object and close the open file for you
   * but the file may stay open for a while (the duration is implementation dependent)
   * you may .red[lose what you have written] to your file


---
# File Object's Position

.row[
.col-6[
```python3
>>> f.readline()
'Python is good.\n'
>>> f.tell() 
16  
>>> f.readline()
"Yes, it's great!\n"
>>> f.tell() 
33
>>> f.readline()
''
>>> f.tell()
33
>>> f.seek(0, 0)  
0  # returns to beginning_of_file
>>> f.readline()
'Python is good.\n'
>>> f.close()
>>> 
```


]
.col-6[
* in `foo.txt`

```python3
Python is good.
Yes, it's great!
```
* `tell()` 
   * returns the file object's current position
* `seek(offset, whence=SEEK_SET)`
   * change the stream position to the given byte offset 
   * offset is interpreted relative to the position indicated by whence
   * in text mode, only seeks relative to the beginning of the file are allowed (or to the end)

https://docs.python.org/3/library/io.html
]
]

---
# `text` mode vs. `binary` mode

* By default, files are opened in .red[text] mode, that means, you read and write .red[strings] from and to the file


* In .red[binary] mode: the data is read and written in the form of .red[bytes objects]. 
   * This mode should be used for all files that don’t contain text
   * e.g., JPEG or EXE files

```python3
>>> f = open('workfile', 'rb+')
>>> f.write(b'0123456789abcdef')
16                 # 16 bytes witten
>>> f.seek(5)      # Go to the 6th byte in the file
5
>>> f.read(1)      # read 1 byte
b'5'
>>> f.seek(-3, 2)  # Go to the 3rd byte before the end
13
>>> f.read(1)
b'd'
```
---
# Saving Objects to Bytes Stream

* .red[Serializing a object] is the process of converting the object to a stream of .red[bytes] that can be saved to a file for later retrieval. 
   * In Python, object serialization is called .red[pickling].
   
```python3
>>> import pickle
>>> phonebook = {'Chris':'555-1111', 'Katie':'555-2222', 'Joanne':'555-3333'} 
>>> output_file = open('phonebook.dat', 'wb')  # open in the binary mode
>>> pickle.dump(phonebook, output_file) 
>>> output_file.close() 
>>>
```
```python3
>>> import pickle
>>> input_file = open('phonebook.dat', 'rb')  # open in the binary mode
>>> pb = pickle.load(inputfile)
>>> pb
{'Chris': '555-1111', 'Joanne': '555-3333', 'Katie': '555-2222'}
>>> input_file.close()
>>>
```
---
# `open()` with `with` statement

* It is a good practice to use the `with` keyword when dealing with file objects 


* The file is properly .read[closed] after its suite finishes, 
   * even if an exception is raised at some point 


* Using `with` is also much .purple[shorter] than writing equivalent `try`-`finally` blocks

```python3
>>> with open('workfile') as f:
        read_data = f.read()

>>> # We can check that the file has been automatically closed.
>>> f.closed
True
```

https://docs.python.org/3/library/io.html

---
```python3
with open ('foo.txt', 'r') as f:
    for line in f:  # This is memory efficient, fast, and leads to simple code
        print(line, end='')
```

```python3
with open ('foo.txt', 'r') as f:
    lines = f.readlines() #read all lines and return a list with the lines
    for line in lines:
        print(line, end='')
```

```python3
filename = 'programming.txt'
with open(filename, 'a') as file_object:
    file_object.write("I also love finding meaning in large datasets.\n")
    file_object.write("I love creating apps that can run in a browser.\n")
```
---
# Exception Handling in Python

* Exceptions: .red[Errors] detected during execution!
* Most exceptions are not handled by programs, 
   * resulting in .red[crash] with error messages

```python3
>>> 10 * (1/0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
>>> 4 + spam*3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'spam' is not defined
>>> '2' + 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't convert 'int' object to str implicitly
```

* Lots of built-in exceptions
   * https://docs.python.org/3/library/exceptions.html#bltin-exceptions

---
# `try`-`except` Clause

```python3
def readInt():
    while True: # asks for input until a valid integer has been entered
        try:
            x = int(input("Please enter a number: "))
            return x
        except ValueError:
            print("Oops!  That was no valid number.  Try again...")
```
* If an exception occurs during execution of the `try` clause, the rest of the clause is skipped 
   * Then if its type matches the exception named after the `except` keyword, the .red[except clause is executed], 
   * and then .red[execution continues] after the try statement
* If an exception occurs which does .red[not match] the exception named in the `except` clause, 
   * it is passed on to outer `try` statements; 
   * if no handler is found, it is an .red[unhandled exception] and .red[execution stops] with an error message.

---
# Exceptions -> Crash

* A program .red[crashes] when an .red[unhandled exception] has been raised.

```python
filename = 'alice.txt'
with open(filename) as f_obj:  # crashes if alice..text does not exists
    contents = f_obj.read()
```

---
# Prevent Crash

* We can handle exceptions to prevent crashes

```python
try:
    filename = 'alice.txt'
    with open(filename) as f_obj:
        contents = f_obj.read()
except FileNotFoundError:
    msg = "Sorry, the file " + filename + " does not exist."
    print(msg)

print("Let's keep going!")  # exception handled -> prevent crash
```

---
# Handle Expected Exceptions!

* If you know that a line of code might rase an exception when executed,
   * you should handle the exception
   * unhandled exceptions should be the exception (you didn't know it would happen)!
   
```python3
successFailureRatio = numSuccesses/numFailures # ZeroDivisionError could occur
print('The success/failure ratio is', successFailureRatio)
print('Now here')
```

```python3
try:
    successFailureRatio = numSuccesses/numFailures # ZeroDivisionError could occur
    print('The success/failure ratio is', successFailureRatio)
except ZeroDivisionError:
    print('No failures, so the success/failure ratio is undefined.)
print('Now here')
```

---
# Raising Exceptions

* The `raise` statement allows the programmer to force a specified exception to occur

```python3
>>> raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere
```
* The sole argument to `raise` indicates the exception to be raised. 
   * This must be either an `exception` instance or an exception class (derived from Exception class/type). 
   * If an `exception` class is passed, it will be implicitly instantiated by calling its constructor with no arguments:
   
```python3
raise ValueError  # shorthand for 'raise ValueError()' -> constructor
```

---
# Raising Exceptions

* re-raise an exception
   * If you need to determine whether an exception was raised but don’t intend to handle it, a simpler form of the `raise` statement allows you to re-raise the exception:
   
```python3
>>> try:
...     raise NameError('HiThere')
... except NameError:
...     print('An exception flew by!')
...     raise
...
An exception flew by!
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
NameError: HiThere
>>>
```
---
# Exceptions as Control Flow Mechanism

* don't just think of exceptions as purely for handling errors


* they are a convenient flow-of-control mechanism that can be used to simplify programs


* a function usually signals the caller by returning a specific value (`-1` or `None`), but


* it is better to have a function .red[raise an exception] when something went wrong
   * when it cannot produce a result that is consistent with the function's specification


* `raise exceptionName(arguments)`
   * `exeptionName` can be built-in exceptions or your own exceptions
   * usually `arguemtns` is just a single `string`

---
# Exceptions for Control Flow

```python
def getRatios(vect1, vect2):
    """Assumes: vect1 and vect2 are equal length lists of numbers
       Returns: a list containing the meaningful values of vect1[i]/vect2[i]"""
    ratios = []
    for index in range(len(vect1)):
        try:
            ratios.append(vect1[index]/vect2[index])
        except ZeroDivisionError:
            ratios.append(float('nan')) #nan = Not a Number
        except:
            raise ValueError('getRatios called with bad arguments')
    return ratios

try:
    print(getRatios([1.0,2.0,7.0,6.0], [1.0,2.0,0.0,3.0]))
    print(getRatios([], []))
    print(getRatios([1.0, 2.0], [3.0]))
except ValueError as msg:
    print(msg)
```
---
# Control Flow w/o `try`-`except`

```python3
def getRatios(vect1, vect2): 
    """Assumes: vect1 and vect2 are lists of equal length of numbers
       Returns: a list containing the meaningful values of vect1[i]/vect2[i]"""
    ratios = []
    if len(vect1) != len(vect2):
        raise ValueError('getRatios called with bad arguments')
    for index in range(len(vect1)):
        vect1Elem = vect1[index]
        vect2Elem = vect2[index]
        if (type(vect1Elem) not in (int, float))\
           or (type(vect2Elem) not in (int, float)):
            raise ValueError('getRatios called with bad arguments')
        if vect2Elem == 0.0:
            ratios.append(float('NaN')) #NaN = Not a Number
        else:
            ratios.append(vect1Elem/vect2Elem)
    return ratios
```
---
# Exceptions in Called Functions

* Exception handlers don’t just handle exceptions if they occur immediately in the `try` clause, 
* but also if they occur inside functions that are called (even indirectly) in the `try` clause 

```python
def this_fails():
    x = 1/0

try:
    this_fails()
except ZeroDivisionError as err:  # We can store the error as a variable
    print('Handling run-time error:', err) 
```

---
# `else` clause

* an optional `else` clause is useful for code that .red[must be executed] if the `try` clause .red[does not raise any exception]
   * `else` clause must appear after all `except` clauses

```python3
try:
    filename='foo.txt'
    f = open(filename, 'r')
except OSError:
    print('cannot open', filename)
else:
    print(filename, 'has', len(f.readlines()), 'lines')
    f.close()
```
---
# Defining Clean-up Actions


* If a `finally` clause is present, the `finally` clause will execute as the last task before the `try` statement completes. 
* The `finally` clause runs .red[whether or not] the `try` statement produces an exception

```python
def divide(x, y):
    try:
        result = x / y
    except ZeroDivisionError:
        print("division by zero!")
    else:
        print("result is", result)
    finally:
        print("executing finally clause")

divide(2, 1)  # else + finally

divide(2, 0)  # except + finally

divide("2", "1")  # finally + Error Messages
```
---
# Defining Clean-up Actions

* `finally` clause to close a file correctly

```python3
f = open('foo.txt', 'w')
try:
   y = x/z
   f.write(str(y))
finally:
   f.close()
```

---
# Handling Multiple Exceptions

```python
try:
    a = [1, 2]
    print(a[3]) # raises/throws an exception
    b = 0       # this statment is not executed!
    c = a[0]/b  # this statment is not executed!
except ZeroDivisionError:
    print('cannot divide by zero')
except IndexError:
    print('invalid index')
```
---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag