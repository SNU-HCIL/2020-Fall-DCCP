layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Inheritance

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---

# Derive Specialized from General

* In the real world, many objects are a specialized version of more general objects

* Example: .red[grasshoppers] and .red[bees] are specialized types of .purple[insect]
   * In addition to the general insect characteristics, they have unique characteristics:
       * Grasshoppers can jump
       * Bees can sting, make honey, and build hives

---

# `Is a` Relationship (.purple[ISA])

* “Is a” relationship exists when one object is a specialized version of another object

* Specialized object has all the characteristics of the general object plus unique characteristics
   * Rectangle .red[is a] shape
   * Daisy .red[is a] flower
---

# Inheritance

* .red[Inheritance] is used to create an “.red[is a]” relationship between classes 


* .red[Superclass] (.purple[base class]): a general class 


* .red[Subclass] (.purple[derived class]): a specialized class
   * An extended version of the superclass
   * Inherits attributes and methods of the superclass
   * New attributes and methods can be added

---
# Inheritance - terminologies

* Synonyms

   * Attribute = Variable = Instance Variable = Data Member = Property = Representation
   
   * Method = Function = Operation = Member Function = Procedure = Behavior
   
   * SuperClass = ParentClass = BaseClass
   
   * SubClass = ChildClass = DerivedClass

---

# Inheritance

* inheritance provides a convenient mechanism for building groups of related .red[abstractions] (i.e., classes or ADT's)


* it allows programmers to greate a .red[type hierarchy]
   * each type inherits attributes from the types above it in the hierarchy


* The class `object` is at the top of the hierarchy
   * Everything in Python that exists at run time is an `object` (i.e., an instance of the class `object`)
   * Every derived class inherits the properties of `object`s

   
---
# The Standard Type Hierarchy

<img src="https://user-images.githubusercontent.com/39995503/97781422-8f84f380-1bce-11eb-887b-00d9118f268b.png" width=800>

modified the image at https://commons.wikimedia.org/wiki/File:Python_3._The_standard_type_hierarchy.png

---
# The Standard Type Hierarchy

* the types that are built into Python

.row[
.col-6[
```
None
NotImplemented
Ellipsis
numbers.Number
    numbers.Integral
        Integers(int)
        Booleans(bool)
    numbers.Real(float)
    numbers.Complex(complex)
Sequences
    Immutable sequences
        Strings
        Tuples
        Bytes
    Mutable sequences
        Lists
        Byte Arrays
```
]
.col-6[
```
Set types
    Sets
    Frozen sets
Mappings
    Dictionaries
Callable types
    User-defined functions
    Instance methods
    Generator functions, Asynchronous generator functions
    Coroutine functions
    Classes, Class instances
Custum classes
Class instances
I/O objects
Internal types
```
]
]

---
# `object` Class

* Mother of All Classes: at the top of the type hierarchy
* `object` class is a built-in data type
* When we defind a class (i.e., ADT), we always make it a .purple[subclass] of `object` class
* What does `object` class have?

```python3
dir(...)
    dir([object]) -> list of strings
    
    If called without an argument, return the names in the current scope.
    Else, return an alphabetized list of names comprising (some of) the attributes
    of the given object, and of attributes reachable from it.
    ...
>>> dir(object)
['__class__', '__delattr__', '__dir__', '__doc__', '__eq__', 
'__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', 
'__init__', '__init_subclass__', '__le__', '__lt__', '__ne__', 
'__new__', '__reduce__', '__reduce_ex__', '__repr__', 
'__setattr__', '__sizeof__', '__str__', '__subclasshook__']
```
---
```python3
>>> help(object)
Help on class object in module builtins:

class object
 |  The base class of the class hierarchy.
 |  
 |  When called, it accepts no arguments and returns a new featureless
 |  instance that has no instance attributes and cannot be given any.
 |  
 |  Built-in subclasses:
...
 |      ... and 86 other subclasses
 |  
 |  Methods defined here:
...
 |  __eq__(self, value, /)
 |      Return self==value.  
... 
 |  __init__(self, /, *args, **kwargs)
 |      Initialize self.  See help(type(self)) for accurate signature.  
 |  __le__(self, value, /)
 |      Return self<=value.  
 |  __lt__(self, value, /)
 |      Return self<value.  
 |  __ne__(self, value, /)
 |      Return self!=value.  
...   
 |  __sizeof__(self, /)
 |      Size of object in memory, in bytes.  
 |  __str__(self, /)
 |      Return str(self). 
```

---
# Person: base class
.row[
.col-7[
```python3
import datetime
class Person(object):
    def __init__(self, name):      
        self.name = name
        self.birthday = None
    def getName(self):
        return self.name
    def getLastName(self):
        lastBlank = self.name.rindex(' ')
        return self.name[lastBlank+1:]
    def setBirthday(self, birthdate):
        self.birthday = birthdate
    def getAge(self):
        if self.birthday == None:
            raise ValueError
        return (datetime.date.today() \
              - self.birthday).days
    def __lt__(self, other):
        return self.name < other.name
    def __str__(self): return self.name
        
```
]
.col-5[
```python3
me = Person('Michael Guttag')
him = Person('Brack Obama')
her = Person('Norah Jones')
print(him.getLastName())
him.setBirthday(\
   datetime.date(1961, 8, 4))
her.setBirthday(\
   datetime.date(1958, 8, 16))
print(him.getName(), 'is', \
   him.getAge(), 'days old.')
```
]
]

---
# Specially Named Methods

* Magic Methods


* `__init__` method
   * whenever `Person` is instantiated, `__init__` function is called with an argument
   * what arguments to supply
   * what properties those arguments should have


* `__lt__` method
   * .red[overloads] the `<` operator (.purple[operator overloading])
   * called whenever the first argument to the `<` operator is of type `Person`


* `__str__` method
   * called whenever an object of type `Person` has to be converted to a string


---
# SNUPerson: derived class
```python3
class SNUPerson(Person):
    
    nextIdNum = 0 # class variable to assign unique identification numbers
    
    def __init__(self, name):
        Person.__init__(self, name)
        self.idNum = SNUPerson.nextIdNum
        SNUPerson.nextIdNum += 1
        
    def getIdNum(self):
        return self.idNum
    
    def __lt__(self, other):
        return self.idNum < other.idNum
```
---
# SNUPerson: derived class

* inherits attributes from its parent class, `Person`
   * including all of the attributes that `Person` inherited from its parent class, `object`
   * `SNUPerson` is a .red[subclass] of `Person`
   * `Person` is its .red[superclass]


* subclass `SNUPerson` can 
   * add new attributes: 
      * <font color='green'>class variable</font>, `nextIdNum` (all instances share it)
      * <font color='purple'>instance variable</font>, `idNum` (each instance has each own)
      * <font color='purple'>instance method</font>, `getIdNum` (each instance has each own)
   * .red[override] (i.e., replace) attributes of the superclass
      * `__init__` : invokes `Person.__init__` first to initialize the .red[inherited] instance variable `self.name`
      * `__lt__`
---
# SNUPerson: derived class

```python3
p1 = SNUPerson('Jinwook Seo')
print(str(p1) + '\'s idnumber is ' + str(p1.getIdNum())
```
* in the `__init__` method, class variable `nextIdNum` is used to assign unique id numbers to instances
   * .red[class variable] belongs to the .red[class] `SNUPerson`, rather than to instances of the class
   
   
* `str(p1)` -> runtime system checks to see if there is an `__str__` method associated with `SNUPerson`
   * since there is not, it next checks to see if there is an `__str__` method associated with the superclass, `Person`
   * `__str__` of the `Person` class is called.
   
   
* `p1.getIdNum()` -> runtime system checks to se if there is an `getIdNum` method associated with `SNUPerson`
   * `getIdNum` of the `SNUPerson` class is called.
   
---
# SNUPerson: derived class

```python3
p1 = SNUPerson('Jinwook Seo')
p2 = Person('Se-jung Oh')

print('p2 < p1 =', p2 < p1)  # prints False (ordered by name)
print('p1 < p2 =', p1 < p2)  # AttributeError: 'Person'object has no attribute 'idNum'
```

* `print('p2 < p1 =', p2 < p1)` invokes the `__lt__` method associated with `p2` (`Person` class)
   * `p2.__lt__(p1)`
   
   
* `print('p1 < p2 =', p1 < p2)` invokes the `__lt__` method associated with `p1` (`SNUPerson` class)
   * `p1.__lt__(p2)`


* the .red[first] argument of the expression is used to determine which `__lt__` method to invoke

---
# Magic Methods in Python

```
__init __( )     for constructor
__del__( )       for destructor
__add__( )       for +
__sub__( )       for -
__mult __( )     for *
__div__( )       for /
__float__( )     for float function
__str __( )      for print( )
__repr __( )     for creating computer readable form
__hash__( )      for making hashable objects
__lt __( )       for <
__le__( )        for <=
__gt __( )       for >
__ge __( )       for >=
__eq __( )       for ==
__iter __( )     for iterable object
__next__( )      for iterable object
```

---
# Multiple Levels of Inheritance

.row[
.col-7[

* `Student`: derived from `SNUPerson`
* `UGrad`: derived from `Student`
* `Grad`: derived from `Student`

```python3
class Student(SNUPerson):  # intermediate class
    pass    # a class with no methods (yet)

class UGrad(Student):
    def __init__(self, name, classYear):
        SNUPerson.__init__(self, name)
        self.year = classYear
    def getClass(self):
        return self.year
    
class Grad(Student):
    pass    # a class with no methods (yet)
```

]
.col-5[
<img src="https://user-images.githubusercontent.com/39995503/97712500-de188c00-1b01-11eb-97df-08286faaac1c.png" width=250>

]
]

* `pass` is a null operation -- when it is executed, nothing happens. 
   * useful as a .red[placeholder] when a statement is .red[required syntactically], but no code needs to be executed.

---
# Multiple Levels of Inheritance

```python3
p5 = Grad('Kiroong Choe')
p6 = UGrad('Bumwoo Kim')

print(p5, 'is a graduate student -->', type(p5) == Grad)
# prints "Kiroong Choe is a graduate student --> True
print(p5, 'is a undergraduate student -->', type(p5) == UGrad)
# prints "Kiroong Choe is a undergraduate student --> False
```

* `class type(object)`
   * with one argument, return the type of an object. 
   * The `isinstance()` built-in function is recommended for testing the type of an object, because it takes subclasses into account.
* Use `isinstance()` to check an instance’s .red[type]: 
   * `isinstance(obj, int)` will be `True` only if `obj.__class__` is `int` or some class derived from `int`.  
* Use `issubclass()` to check class `inheritance`: 
   * `issubclass(bool, int)` is `True` since `bool` is a subclass of `int`. However, `issubclass(float, int)` is `False` since `float` is not a subclass of `int`.
   
---
# add `isStudent(self)` method

* where to add it: `Student` or `SNUPerson`?

* add to the `Student` class?

```python3
def isStudent(self):
    return type(self) == Grad or type(Self) == UGrad
```
* what happens if a new type of students (e.g., `TransferStudent`) were introduced later


* add to the `SNUPerson` class?

```python3
def isStudent(self):
    return isinstance(self, Student)
```

* The `isinstance()` built-in function is recommended for testing the type of an object, because it takes subclasses into account.



---
# TansferStudent class

.row[
.col-7[
```python3

class TransferStudent(Student):
    def __init__(self, name, fromSchool):
        SNUPerson.__init__(self, name)
        self.fromSchool = fromSchool
    def getOldSchool(self):
        return self.fromSchool
```
]
.col-5[
<img src="https://user-images.githubusercontent.com/39995503/97800800-96b60b00-1c7b-11eb-9493-65d8ba93da06.png", width=250>


]
]

* If `isStudent` were added to the `Student` class,

```python3
def isStudent(self):
    return type(self) == Grad or \
           type(self) == UGrad or \
           type(self) == TransferStudent
```

---
# Liskov Substitution Principle

* If `S` is a .red[subtype] of `T`, then objects of type `T` may be replaced with objects of type `S` without altering the correctness of the program.


* subclasses should be thought of as .red[extending] the behavior of their superclasses


* when subclass overrrides methods from the superclass
   * important behaviors of the supertype must be supported by subtypes
   * if client code works correctly using the supertype, it should also work correctly when an instance of the subtype is .red[substituted] for the instance of the supertype
   * e.g., it should be possible to write client code using the specification of `Student` and have it work correctly on a `TransferStudent`

---
# Liskov Substitution Principle

```python3
class Calculator():
    def calculate(self, a, b): # returns a number
        return a * b

class DividerCalculator(Calculator):
    def calculate(self, a, b): # returns a number or raises an Error
        return a / b           

print(Calculator().calculate(3, 4))
print(DividerCalculator().calculate(3, 4))
print(Calculator().calculate(5, 0)) 
print(DividerCalculator().calculate(5, 0)) # 0 will cause an Error
```

* We cannot replace `Calculator` object with `DividerCalculator` object
   * The inheritance violates the Substitution Principle!
   
   
---
# Iterators

* Most container objects can be looped over using a `for` statement
* This style of access using .red[iterators] is clear, concise, and convenient. 
* The use of .red[iterators] pervades and unifies Python.

```python3
for element in [1, 2, 3]:
    print(element)
for element in (1, 2, 3):
    print(element)
for key in {'one':1, 'two':2}:
    print(key)
for char in "123":
    print(char)
for line in open("myfile.txt"):
    print(line, end='')
```

* Behind the scenes, the `for` statement calls `iter()` on the container object. 
   * The function returns an .red[iterator] object 
   * The .red[iterator] object defines the method `__next__()` which accesses elements in the container one at a time.


---
# Iterators

* When there are no more elements, `__next__()` raises a `StopIteration` exception which tells the `for` loop to terminate. 

* You can call the `__next__()` method using the `next()` built-in function

```python3
>>> s = 'abc'
>>> it = iter(s)  # returns an iterator
>>> it
<iterator object at 0x00A1DB50>
>>> next(it)
'a'
>>> next(it)
'b'
>>> next(it)
'c'
>>> next(it)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
    next(it)
StopIteration
```

---
# add `iterator` behavior to classes

* Define an `__iter__()` method which returns an object with a `__next__()` method. 
* If the class defines `__next__()`, then `__iter__()` can just return `self`:

.row[
.col-6[
```python3
class Reverse:
    """Iterator for looping 
       over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)
    def __iter__(self):
        return self
    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]
```
]
.col-6[
```python3
>>> rev = Reverse('spam')
>>> iter(rev)
<__main__.Reverse object at 0x00A1DB50>
>>> for char in rev:
...     print(char)
...
m
a
p
s
```
]
]

---
# Example: Iterable Object

```python3
class MyCollection:
    def__init__(self):
        self.size=10
        self.data=list(range(self.size))
    def__iter__(self):
        self.index=0
        return self
    def__next__(self):
        if self.index>=self.size: 
            raise StopIteration
        n=self.data[self.index]
        self.index+=1
        return n

coll=MyCollection()
for x in coll:
    print(x)
```

---
# Generators

* Generators are a simple and powerful tool for creating .red[iterators]. 
* They are written like regular functions but use the `yield` statement whenever they want to return data. 
* the `__iter__()` and `__next__()` methods are created .red[automatically]
* when generators terminate, they automatically raise `StopIteration`.
* Each time the builtin function`next()` is called on it, the generator .red[resumes] where it left off 
   * it .red[remembers] all the data values and which statement was last executed. 
   * the local variables and execution state are automatically saved between calls
   
```python
def reverse(data):
    for index in range(len(data)-1, -1, -1): # stop (-1) is not included
        yield data[index]

for char in reverse('golf'):
    print(char)
```
---
# Example: Generators

```python3
# Generator function
def gen():
    yield 1
    yield 2
    yield 3

#Generator object 
g=gen()
print(type(g)) #<class'generator'>

#use next() function
n=next(g); print(n) #1
n=next(g); print(n) #2
n=next(g); print(n) #3

#for loop 
for x in gen():  # if g is used instead, nothing prints 
    print(x)     # because iterator for g has exhaused!
```
---
# Example: Generators

.row[
.col-6[
```python3
def firstn(n):
    num, nums = 0, []
    while num < n:
        nums.append(num)
        num += 1
    return nums
    
sum_of_first_n = sum(firstn(1000000))
```
* huge memory needed!

]
.col-6[
```python3
def firstn(n):
    num = 0
    while num < n:
        yield num
        num += 1
    
sum_of_first_n = sum(firstn(1000000))
```

* yield 1 and pass it to `sum`
* yield 2 and pass it to `sum`
...
* yield 1000000 and pass it to `sum`

* lazy (=on demand) generation of items
]
]

---
# Comprehension of Iterable Object

* list comprehension

```python3
>>> twice = [ x*2 for x in range(10)]
>>> twice
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

* set comprehension

```python3
>>> stwice = { x*2 for x in range(10)}
>>> stwice
{0, 2, 4, 6, 8, 10, 12, 14, 16, 18}
```

* generator comprehension

```python3
>>> gtwice = ( x*2 for x in range(10) )
>>> gtwice
<generator object <genexpr> at 0x7fbe9e0f5580>
```
---
# Generator Expressions

* Some simple `generators` can be coded succinctly as expressions using a syntax similar to list comprehensions
   * with .red[parentheses] instead of square brackets

```python3
# generator expression
g=(n*n for n in range(21))  # g is a generator object

print(type(g))      # <class 'generator'>

mylist = list(g)    # create a list using g
                    # iterator for g has exhausted

g=(n*n for n in range(21))  # g is a generator object

for i in range(10): # print the first 10
    value = next(g)
    print(value)

for x in g:         # print the remaining 10
    print(x)
```

---
# Generator Expressions

* Some simple `generators` can be coded succinctly as expressions using a syntax similar to list comprehensions
   * with .red[parentheses] instead of square brackets
   * the `generator` is used right away by an enclosing function

```python3
>>> sum(i*i for i in range(10))                 # sum of squares
285

>>> xvec = [10, 20, 30]
>>> yvec = [7, 5, 3]
>>> sum(x*y for x,y in zip(xvec, yvec))         # dot product
260

>>> unique_words = set(word for line in page for word in line.split())

>>> valedictorian = max((student.gpa, student.name) for student in graduates)

>>> data = 'golf'
>>> list(data[i] for i in range(len(data)-1, -1, -1))
['f', 'l', 'o', 'g']
```

---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag
