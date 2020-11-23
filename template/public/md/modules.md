layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Modules and Packages

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---
# Why Modules?

* If you quit from the Python interpreter and enter it again, the definitions you have made (functions and variables) are lost.
   * if you want to write a somewhat longer program, you have to save your program as a file (i.e., creating a .purple[script])
   * such a file (.py) is called a .red[module]
   
   
* A module is a file containing Python definitions and statements. 
* .red[The file name is the module name] with the suffix .py appended. 
* Within a module, the module’s name (as a string) is available as the value of the global variable `__name__`


* definitions from a module can be imported 
   * into other modules or 
   * into the `main` module: the collection of variables that you have access to in a script executed at the top level (outside any function definitions) and in interactive mode.

---
# How to Use a Module

.row[
.col-6[

in `fibo.py`

.font-12[

```python3
# Fibonacci numbers module

def fib(n):    # write Fibonacci series up to n
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

def fib2(n):   # return Fibonacci series up to n
    result = []
    a, b = 0, 1
    while a < n:
        result.append(a)
        a, b = b, a+b
    return result
```
]
]
.col-6[

.red[import] the module

.font-14[
```python3
>>> import fibo
>>> fibo.fib(1000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
>>> fibo.fib2(100)
[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
>>> fibo.__name__
'fibo'
```
]

* If you intend to use a function often, you can assign it to a .purple[local name]:

.font-14[
```python3
>>> fib = fibo.fib
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```
]
]
]

---
# Variant of the `import` statement

* it is possible to import names from a module directly into the importing module’s symbol table
```python3
>>> from fibo import fib, fib2
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```


* it is possible to import all names that a module defines
```python3
>>> from fibo import *
>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```


* the practice of importing `*` from a module or package is frowned upon, since it often causes .purple[poorly readable code]
   * it introduces an unknown set of names into the interpreter, possibly hiding some things you have already defined.

---
# Variant of the `import` statement

* If the module name is followed by `as`, then the name following `as` is bound directly to the imported module.
```python3
>>> import fibo as fib
>>> fib.fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```


* This is effectively importing the module in the same way that `import fibo` will do, 
   * with the only difference of it being available as `fib`.


* It can also be used when utilising `from` with similar effects:
```python3
>>> from fibo import fib as fibonacci
>>> fibonacci(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
```

---
# Symbol Table of a Module

* Each module has its own .red[private symbol table], 
   * which is used as the global symbol table by all functions defined in the module
   * the author of a module can use global variables in the module without worrying about accidental clashes with a user’s global variables


* You can touch a module’s global variables with the same notation used to refer to its functions, `modname.itemname`.
   * but you don't want to do this 

---
# Executing Modules as Scripts

* When you run a Python module with
```python3
python fibo.py <arguments>
```


* the code in the module will be executed, just as if you imported it, 
   * but with the `__name__` set to `__main__` (not `fibo`)


* if you add this at the end of your module:

```python3
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))
```


.row[
.col-6[
* you can do this:
```python3
$ python fibo.py 50
0 1 1 2 3 5 8 13 21 34
```
]
.col-6[
* If the module is imported, the code will not run:
```python3
>>> import fibo
>>>
```
]
]

---
# Executing Modules as Scripts

* Usually, people can add the following at the end of your module

```python3
if __name__ == "__main__":
    # add code for running directly in the shell
    print("this mod is run directly")
else:
    print("this mod is imported into another module")
```

.row[
.col-6.font-14[

in the foo module (i.e., foo.py)
```python3
# foo.py
import bar
print("foo.__name__ set to ", __name__)
```
]
.col-6.font-14[

in the bar module (i.e., bar.py)
```python3
# bar.py
print("bar.__name__ set to ", __name__)
```
]
]

.font-14[
```python3
$ python bar.py
bar.__name__ set to __main__
$ python foo.py
bar.__name__ set to bar
foo.__name__ set to __main__
```
]

---
# Module Search Path

* When a module named `spam` is imported, the interpreter first searches for a `built-in` module with that name. 
* If not found, it then searches for a file named `spam.py` in a list of directories given by the variable `sys.path`. 


* `sys.path` is initialized from these locations:
   * The directory containing the input script (or the current directory when no file is specified).
   * `PYTHONPATH` (a list of directory names, with the same syntax as the shell variable `PATH`).
   

* After initialization, Python programs can modify `sys.path`. 
   * The directory containing the script being run is placed at the beginning of the search path, ahead of the standard library path. 
   * This means that scripts in that directory will be loaded instead of modules of the same name in the standard library directory. 
   * This is an error unless the replacement is intended.
   
---
# Module Search Path

* The variable `sys.path` is a list of strings that determines the interpreter’s search path for modules. 
* It is initialized to a default path taken from the environment variable PYTHONPATH
* You can modify it using standard list operations:


```python3
>>> import sys
>>> sys.path
['/Users/jinwook/Documents', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python39.zip',   '/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/lib-dynload', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages']
>>> sys.path.append('/Users/jinwook/Downlaods')
>>> sys.path
['/Users/jinwook/Documents', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python39.zip', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/lib-dynload', '/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages', '/Users/jinwook/Downlaods']
>>> 
```


---
# Packages

* Package is a collection of modules
* Packages are a way of structuring Python’s module namespace by using “dotted module names”. 
   * For example, the module name `A.B` designates a submodule named `B` in a package named `A`


* Can save the authors of multi-module packages (e.g., NumPy or Pillow) from having to worry about each other’s module names


* Suppose you want to design a collection of modules (a “package”) for the uniform handling of sound files and sound data. 
   * There are many different sound file formats (usually recognized by their extension, for example: .wav, .aiff, .au), 
   * so you may need to create and maintain a growing collection of modules for the conversion between the various file formats.
   

* What could a possible structure for your package be?

---
# Example: `sound` package

.font-14[
```
sound/                          Top-level package
      __init__.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```
]



---
# Import Modules from a Package

* `__init__.py` files are required to make Python treat directories containing the file as packages.
   * In the simplest case, `__init__.py` can just be an empty file, 
   * but it can also execute initialization code for the package
   
   
```python3
import sound.effects.echo
sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)
```
```python3
from sound.effects import echo
echo.echofilter(input, output, delay=0.7, atten=4)
```
```python3
from sound.effects.echo import echofilter
echofilter(input, output, delay=0.7, atten=4)
```

---
# Popular Python Packages

* DB Binding Libraries
   * PyMySQL package
   * MySQLdb package
   * SQLAlchemy package


* Scientific Libraries
   * SciPy package
    

* Web Development Libraries
   * Django package
   * Flask package


* Machine Learning Libraries
   * NumPy package
   * Pandas package
   * Matplotlib package
   * SKLearn package
   * NLTK package

---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag