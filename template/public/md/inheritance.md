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

# `ISA` Relationship

* “.red[Is a]” relationship exists when one object is a specialized version of another object


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

   * Attribute = Variable = Instance Variable = Data Member = Data Attribute = Property = Representation
   
   * Method = Function = Operation = Member Function = Method Attribute = Procedure = Behavior
   
   * Super Class = Parent Class = Base Class
   
   * Sub Class = Child Class = Derived Class

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

.font-14[
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
]

---
.font-12[
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
]

---
# Person: base class
.row[
.col-7[
.font-14[
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
        return (datetime.date.today() - self.birthday).days
    def __lt__(self, other):
        return self.name < other.name
    def __str__(self): 
        return self.name      
```
]
]
.col-5[
.font-14[
```python3
me = Person('Michael Guttag')
him = Person('Brack Obama')
her = Person('Norah Jones')
print(him.getLastName())
him.setBirthday(datetime.date\
                (1961, 8, 4))
her.setBirthday(datetime.date\
                (1958, 8, 16))
print(him.getName(), 'is', him.getAge(),\
      'days old.')
```
]
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
      * `__init__` : invokes `Person.__init__` first to initialize the **inherited** instance variable `self.name`
      * `__lt__` : overrides the `__init__` of the super class, `Person`
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
   
   
* `p1.getIdNum()` -> runtime system checks to see if there is an `getIdNum` method associated with `SNUPerson`
   * `getIdNum` of the `SNUPerson` class is called.
   
---
# SNUPerson: derived class

.font-15[
```python3
p1 = SNUPerson('Jinwook Seo')
p2 = Person('Se-jung Oh')

print('p2 < p1 =', p2 < p1)  # prints False (ordered by name)
print('p1 < p2 =', p1 < p2)  # AttributeError: 'Person'object has no attribute 'idNum'
```
]

* the .red[first] argument of the expression is used to determine which `__lt__` method to invoke


* `print('p2 < p1 =', p2 < p1)` invokes the `__lt__` method associated with `p2` (`Person` class)
   * `p2.__lt__(p1)`
   
   
* `print('p1 < p2 =', p1 < p2)` invokes the `__lt__` method associated with `p1` (`SNUPerson` class)
   * `p1.__lt__(p2)`

---
# Magic Methods in Python

```
__init__()      for constructor
__del__()       for destructor
__add__()       for +
__sub__()       for -
__mul__()       for *
__div__()       for /
__float__()     for float function
__str__()       for print( )
__repr__()      for creating computer readable form
__hash__()      for making hashable objects
__lt__()        for <
__le__()        for <=
__gt __()       for >
__ge__()        for >=
__eq__()        for ==
__iter__()      for iterable object
__next__()      for iterable object
```

---
# Multiple Levels of Inheritance

.row[
.col-7[

* `Student`: derived from `SNUPerson`
* `UGrad`: derived from `Student`
* `Grad`: derived from `Student`

.font-14[
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
]
.col-5[
<img src="https://user-images.githubusercontent.com/39995503/98498699-c7ed9700-228a-11eb-8616-b672d4a6d9f4.png" width=250>

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
# prints "Kiroong Choe is a graduate student --> True"
print(p5, 'is a undergraduate student -->', type(p5) == UGrad)
# prints "Kiroong Choe is a undergraduate student --> False"
```

* `class type(object)`
   * with one argument, return the type of an object. 
   * The `isinstance()` built-in function is recommended for testing the type of an object, because it takes subclasses into account.
* Use `isinstance(obj, Class)` to check an instance’s .red[type]: 
   * `isinstance(obj, int)` will be `True` only if `obj.__class__` is `int` or some class derived from `int`.  
* Use `issubclass(sub, sup)` to check class `inheritance`: 
   * `issubclass(bool, int)` is `True` since `bool` is a subclass of `int`. However, `issubclass(float, int)` is `False` since `float` is not a subclass of `int`.

---
# `type`, `isinstance`, `issubclass`
.row[
.col-7[
.font-15[
```python
class A(object): pass
class B(A): pass
a = A()
b = B()
print(type(a) == A) # True
print(type(b) == A) # False
print(type(a) == B) # False
print(type(b) == B) # True
print()
print(isinstance(a, A)) # True
print(isinstance(b, A)) # True (surprised?)
print(isinstance(a, B)) # False
print(isinstance(b, B)) # True
print()
print(issubclass(B, A)) # True
print(issubclass(A, B)) # False
```
]
]
.col-5[
<img src="https://user-images.githubusercontent.com/39995503/98459846-1561f980-21e2-11eb-8167-663aaa8a90f4.png" width=300>
]
]

---
# add `isStudent(self)` method

* `type` vs. `isinstance`
* `isinstance()` built-in function is recommended for testing the type of an object, because it takes subclasses into account.

.row[
.col-6[

* if we use `type` function,

.font-14[
```python3
def isStudent(self):
    return type(self) == Grad or \
           type(self) == UGrad
```
]
]
.col-6[

* if we use `isinstance` function,

.font-14[
```python3
def isStudent(self):
    return isinstance(self, Student)
```
]
]
]

* what happens if a new type of students (e.g., `TransferStudent`) were added later?
   * we have to change the definition of the `isStudent` function with `type`
   * but we don't have to change the definition with `isinstance`   
   

* we can use `isinstance` function with the help of the `Student` class,
   * the utility of the intermediate class, `Student`
   * without the `Student` class, the code using `isinstance` doesn't work


* better to add the `isStudent` method to `SNUPerson` than to `Student`
   * can call it with any `SNUPerson` instances other than `Student` instances




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
<img src="https://user-images.githubusercontent.com/39995503/98498890-611cad80-228b-11eb-9d3c-e65df85735b9.png", width=300>


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
   * The inheritance violates the Liskov Substitution Principle!

<p style="font-size:12px">
https://www.pythonforeveryone.com/articles/liskov-substitution-principle-python.html
</p>

---
# ADT Example: Vector2D

.row[
.col-8[
.font-14[
```python
class Vector2D:
    def __init__(self, a, b):
       # overrriding object's __init__ method
       self.x = a
       self.y = b

    def __str__(self):
       # overriding object's __str__ method
       return 'Vector2D object with (x=%d, y=%d)' % (self.x, self.y)

    def __add__(self, other):
       # operator overloading (+)
       return Vector2D(self.x + other.x, self.y + other.y)

v1 = Vector2D(2, 10)
v2 = Vector2D(5, -2)

print(v1)       # __str__ is called
print(v1 + v2)  # __add__ is called
print(issubclass(Vector2D, object)) # True
```
]
]
.col-4[
<img src="https://user-images.githubusercontent.com/39995503/98460453-f49ca280-21e7-11eb-825b-0605b47fd4cb.png" width=100/>


<img src="https://icon-library.com/images/2018/6207641_halftone-dots-vector-coordinates-hd-png-download.png" width="250"/>
]
]

---
# `__str__()` vs. `__repr__()`


* `__str__()` is called by `str()` and `print()` to compute the .red[informal] string representation of an object

* `__repr__()` is called by `repr()` to compute the .red[official] (or canonical) string representation of an object

* `__repr__()` is called if `__str__()` is not defined

```python3
>>> f1 = Vector2D(1,2)
>>> print(f1)      # __str__ is called
Vector2D object with (x=1, y=2)
>>> f1             # __repr__ is called (__repr__ of the object class)
<__main__.Vector2D object at 0x7fa89613c850>
>>> [f1]           # __repr__ is called (__repr__ of the object class)
[<__main__.Vector2D object at 0x7fa89613c850>]
>>> 
```

---
# `__str__`() vs. `__repr__`()


.font-14[
```python
class Vector2D:
    def __init__(self, a, b):
       # overrriding object's __init__ method
       self.x = a
       self.y = b

    def __str__(self):
       # overriding object's __str__ method
       return 'Vector2D object with (x=%d, y=%d)' % (self.x, self.y)
       
    def __repr__(self):
       # overriding object's __repr__ method
       print('__repr__ is called')
       return 'Vector2D(%d, %d)' % (self.x, self.y)

    def __add__(self, other):
       # operator overloading (+)
       return Vector2D(self.x + other.x, self.y + other.y)

v1 = Vector2D(2, 10)
v2 = Vector2D(5, -2)
print(v1)       # __str__ is called -> "Vector2D object with (x=2, y=10)"
L = [v2]        # __repr__ is called
print(L)        # "[Vector2D(5, -2)]"
```
]

---
# ADT Example: Fraction (1/4)

.font-12[

```python
from math import gcd
class Fraction(object):
    def __init__(self,num,den):
        self.num=num
        self.den=den
        self.simplify()
    def toString(self):
        return str(self.num)+"/"+str(self.den)
    def add(self,other):
        num1=self.num*other.den
        num2=other.num*self.den
        return Fraction(num1+num2, self.den*other.den)
    def mul(self,other):
        ...
    def toFloat(self):
        ...
    def simplify(self):
        gcdVal = gcd(self.num, self.den)
        self.num, self.den = self.num//gcdVal, self.den//gcdVal
        
f1=Fraction(4,6)
f2=Fraction(5,9)
print(f1) # <__main__.Fractionobjectat0x1010349b0>
print(f1.toString()) # 2/3
print(f1.add(f2).toString()) # 11/9
```
]

* We want to `print` `Franction` object in the same way was we print `int` or `float`

---
# ADT Example: Fraction (2/4)

.font-12[
```python
from math import gcd
class Fraction(object):
    def __init__(self,num,den):
        self.num=num
        self.den=den
        self.simplify()
    def __str__(self):
        return str(self.num)+"/"+str(self.den)
    def add(self,other):
        num1=self.num*other.den
        num2=other.num*self.den
        return Fraction(num1+num2, self.den*other.den)
    def mul(self,other):
        ...
    def toFloat(self):
        ...
    def simplify(self):
        gcdVal = gcd(self.num, self.den)
        self.num, self.den = self.num//gcdVal, self.den//gcdVal
        
f1=Fraction(4,6)
f2=Fraction(5,9)
print(f1)    #2/3 (print calls __str__()
print(f1.add(f2))    #11/9
print(f1.__str__())  #2/3
```
]

* We want to add two `Fraction` objects with the operator `+`
* We want to multiply two `Fraction` objects with the operator `*`

---
# ADT Example: Fraction (3/4)

.font-12[
```python
from math import gcd
class Fraction(object):
    def __init__(self,num,den):
        self.num=num
        self.den=den
        self.simplify()
    def __str__(self):
        return str(self.num)+"/"+str(self.den)
    def __add__(self,other):
        num1=self.num*other.den
        num2=other.num*self.den
        return Fraction(num1+num2, self.den*other.den)
    def __mul__(self,other):
        num=self.num*other.num
        den=self.den*other.den
        return Fraction(num, den)
    def toFloat(self):
        ...
    def simplify(self):
        gcdVal = gcd(self.num, self.den)
        self.num, self.den = self.num//gcdVal, self.den//gcdVal
        
f1=Fraction(4,6)
f2=Fraction(5,9)
f3=Fraction(3,5)
print(f1)    # 2/3
print(f1+f2) # 11/9 (calls __add__())
print(f1*f3) # 2/5  (calls __mul__())
```
]

* We want to add two `Fraction` objects with the operator `+`

---
# ADT Example: Fraction (4/4)

.font-12[
```python
from math import gcd
class Fraction(object):
    def __init__(self,num,den):
        self.num=num
        self.den=den
        self.simplify()
    def __str__(self):
        return str(self.num)+"/"+str(self.den)
    def __add__(self,other):
        num1=self.num*other.den
        num2=other.num*self.den
        return Fraction(num1+num2, self.den*other.den)
    def __mul__(self,other):
         num=self.num*other.num
         den=self.den*other.den
         return Fraction(num, den)
    def __float__(self):
        return self.num/self.den
    def __eq__(self,other):
        return (self.num==other.num) and (self.den==other.den)        
    def simplify(self):
        gcdVal = gcd(self.num, self.den)
        self.num, self.den = self.num//gcdVal, self.den//gcdVal
        
f1=Fraction(4,6)
f2=Fraction(5,9)
print(float(f1)) # 0.6666666666666666 (calls __float__())
print(f1==f2)  # False
```
]


---
# Make a Class Hashable 

.font-12[
```python3
from math import gcd
class Fraction(object):
    def __init__(self,num,den):
        self.num=num
        self.den=den
        self.simplify()
    def __str__(self):
        return str(self.num)+"/"+str(self.den)
    def __add__(self,other):
        num1=self.num*other.den
        num2=other.num*self.den
        return Fraction(num1+num2, self.den*other.den)
    def __mul__(self,other):
         num=self.num*other.num
         den=self.den*other.den
         return Fraction(num, den)
    def __float__(self):
        return self.num/self.den
    def __eq__(self,other):
        return (self.num==other.num) and (self.den==other.den)        
    def simplify(self):
        gcdVal = gcd(self.num, self.den)
        self.num, self.den = self.num//gcdVal, self.den//gcdVal

f1=Fraction(4,6)
s=set()
s.add(f1)  # TypeError: unhashable type: 'Fraction'
```
]

---
# Make a Class Hashable 

* We can add `int` and `float` to a `set`, but we cannot add a `Franction` 
   * Why? 
   * `set.add()` calls `__hash__()`
   * `__hash__()` of `object` class is called because `Franction` doesn't have it
   * `Fraction` object is not hashable
   
```python3
   def __hash__(self, /) # __hash__() of the object class
      return hash(self)  # TypeError: unhashable type: 'Fraction'
```
* We have to .red[override] `__hash__()` method inherited from `object` class

---
# Make a Class Hashable 

.font-12[
```python3
from math import gcd

class Fraction(object):
    def __init__(self,num,den):
        self.num=num
        self.den=den
        self.simplify()
    def __str__(self):
        return str(self.num)+"/"+str(self.den)
    def __add__(self,other):
        num1=self.num*other.den
        num2=other.num*self.den
        return Fraction(num1+num2, self.den*other.den)
    def __mul__(self,other):
         num=self.num*other.num
         den=self.den*other.den
         return Fraction(num, den)
    def __float__(self):
        return self.num/self.den
    def __eq__(self,other):
        return (self.num==other.num) and (self.den==other.den)        
    def simplify(self):
        gcdVal = gcd(self.num, self.den)
        self.num, self.den = self.num//gcdVal, self.den//gcdVal
    def getHashables(self):
        return (self.num,self.den)  # tuple is hashable
    def __hash__(self):  # override __hash__() of the object class
        return hash(self.getHashables())
```
]

---
# Abstract Base Classes (ABCs)

* Abstract base classes are classes that contain one or more .red[abstract methods].


* An abstract method is a method that is .red[declared, but contains no implementation] 
   * pure virtual function in C++
 
 
* An abstract base class defines an interface for subsequent derived classes to overrride


* Abstract base classes .red[should not be instantiated], and **.red[require] subclasses to provide implementations  for the abstract methods**.


* Python comes with a module which provides the infrastructure for defining Abstract Base Classes (ABCs)

---
# Abstract Base Classes

* When do we need an `ABC`?

.center[<img src="https://user-images.githubusercontent.com/39995503/97950211-81ef8980-1dd9-11eb-95d5-a457fde81098.png" width=450/>]

* It makes sense for each subclass of the `Shape` class to have its own `draw()` and `area()` methods
* A `Shape` is just a (abstract) concept, not a real thing, it doesn't make sense to have instances of `Shape` 
---
# Abstract Base Class 

.row[
.col-6[
```python3
from abc import ABC, abstractmethod
class Shape(ABC):
    
    @abstractmethod
    def draw(self):
        pass
    
    @abstractmethod
    def area(self):
        pass

class Triangle(Shape)
    
    def draw(self):
        # some actual code 
        # to draw a triangle
    
    def area(self):
        # some actual code 
        # to calucate the area
```
]
.col-6[
<img src="https://user-images.githubusercontent.com/39995503/97951246-dfd1a080-1ddc-11eb-9e65-bb6826783ed4.png" width=400>

]
]

---
# Abstract Base Class 

* A `Shape` is just a (abstract) concept, not a real thing, it doesn't make sense to have instances of `Shape`

* If you try to instantiate the ABC `Shape`,

.font-14[
```python3
Traceback (most recent call last):
  File "/Users/jinwook/Documents/abc.py", line 22, in <module>
    s = Shape()
TypeError: Can't instantiate abstract class Shape with abstract methods area, draw
```
]

* If you try to instantiate the class `Triangle` without implementing the `draw` method,

.font-14[
```python3
Traceback (most recent call last):
  File "/Users/jinwook/Documents/abc.py", line 19, in <module>
    t = Triangle()
TypeError: Can't instantiate abstract class Triangle with abstract method draw
```
]

---
# ABC Example

Imagine we run a car dealership.
We sell all types of vehicles, from motorcycles to trucks.
We set ourselves apart from the competition by our prices.
Specifically, how we determine the price of a vehicle on our lot: $5,000 x number of wheels a vehicle has.
We love buying back our vehicles as well.
We offer a flat rate (i.e., base sales price) - 10% of the miles driven on the vehicle.
For trucks, that rate is $10,000. For cars, $8,000. For motorcycles, $4,000.

If we wanted to create a sales system for our dealership using Object-oriented techniques,
How would we do so?
What would the objects be?
We might have a Sale class, a Customer class, an Inventory class, and so forth, but
we'd almost certainly have a `Car` , `Truck` , and `Motorcycle` class.
What would these classes look like?


---
# Initial Design - Car & Truck

.row[
.col-6[
.font-14[
```python3
class Car(object):
    def __init__(self,wheels,miles,make,model,year,sold_on):
        #Return a new Car object
        self.wheels=wheels
        self.miles=miles
        self.make=make
        self.model=model
        self.year=year
        self.sold_on=sold_on
    def sale_price(self):
        #Return the sale price for this car as a float amount
        if self.sold_on is not None:
             return 0.0   #Already sold
        return 5000.0*self.wheels
    def purchase_price(self):
        # Return the price for which we would pay to purchase the car
        if self.sold_on is None:
             return 0.0  #Not yet sold
        return 8000-(.10*self.miles) # this car was purchased in our shop
```
]
]
.col-6[
.font-14[
```python3
class Truck(object):
    def __init__(self,wheels,miles,make,model,year,sold_on):
        #Return a new Car object
        self.wheels=wheels
        self.miles=miles
        self.make=make
        self.model=model
        self.year=year
        self.sold_on=sold_on
    def sale_price(self):
        #Return the sale price for this truck a float amount
        if self.sold_on is not None:
             return 0.0   # Already sold
        return 5000.0*self.wheels
    def purchase_price(self):
        # Return the price for which we would pay to purchase the truck
        if self.sold_on is None:
             return 0.0  # Not yet sold
        return 1000-(.10*self.miles) # this truck was purchased in our shop
```
]
]
]

* They share so much data and functionality in common 
* There must be an .red[abstraction] we can introduce here

---
# Conceptualize the Vehicle Class

* A `Vehicle` is not a real-world object, 
* but it is rather a concept that some real-world objects embody

.font-14[
```python3
class Vehicle(object):
    base_sale_price=0
    def __init__(self,wheels,miles,make,model,year,sold_on):
        self.wheels=wheels
        self.miles=miles
        self.make=make
        self.model=model
        self.year=year
        self.sold_on=sold_on
    def sale_price(self):
        if self.sold_on is not None:
            return 0.0 # Already sold
        return 5000.0*self.wheels
    def purchase_price(self):
        if self.sold_on is None:
            return 0.0 # Notyetsold
        return self.base_sale_price-(.10*self.miles)
```
]


---
# Conceptualize the Vehicle Class

* A `Vehicle` is just a concept, not a real thing, so what does it mean to say the following:

```python3
v = Vehicle(4, 0, 'Hyundai', 'Genesis', 2020, None)
print(v.purchase_price())
```

* It should be illegal!
  
* `Vehicle` should really be an .red[ABC]



---
# Conceptualize the Vehicle Class

.row[
.col-7[
.font-14[
```python3
from abc import ABC, abstractmethod
class Vehicle(ABC):
    base_sale_price=0
    wheels=0
    
    def __init__(self,wheels,miles,make,model,year,sold_on):
        self.miles=miles
        self.make=make
        self.model=model
        self.year=year
        self.sold_on=sold_on
    def sale_price(self):
        if self.sold_on is not None:
            return 0.0 # Already sold
        return 5000.0*self.wheels
    def purchase_price(self):
        if self.sold_on is None:
            return 0.0 # Notyetsold
        return self.base_sale_price-(.10*self.miles)
   
    @abstractmethod
    def vehicle_type(self) 
        pass  
        # subclass should define this method  
```
]
]
.col-5[

<img src="https://user-images.githubusercontent.com/39995503/98464278-17897f80-2205-11eb-8c50-a40ecaed0110.png" width=300/>

]
]

---
# Vehicle, Car, Truck, Motorcycle

.row[
.col-7[
.font-15[
```python3
car Car(Vehicle):
   base_sale_price = 8000
   wheels = 4
   
   def vehicle_type(self)
      return 'car'
```

```python3
car Truck(Vehicle):
   base_sale_price = 10000
   wheels = 4
   
   def vehicle_type(self)
      return 'truck'
```

```python3
car Motorcycle(Vehicle):
   base_sale_price = 4000
   wheels = 2
   
   def vehicle_type(self)
      return 'motorcycle'
```
]
]
.col-5[

<img src="https://user-images.githubusercontent.com/39995503/98464403-042ae400-2206-11eb-9fa9-7e574886e1b9.png" width=350/>
]
]

---
# Iterators

* Most container objects can be looped over using a `for` statement
* This style of access using .red[iterators] is clear, concise, and convenient. 
* The use of .red[iterators] pervades and unifies Python.

.font-15[
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
]

* Behind the scenes, the `for` statement calls `iter()` on the container object. 
   * The function returns an .red[iterator] object 
   * The .red[iterator] object defines the method `__next__()` which accesses elements in the container one at a time.


---
# Iterators

* When there are no more elements, `__next__()` raises a `StopIteration` exception which tells the `for` loop to terminate. 

* You can call the `__next__()` method using the `next()` built-in function

.font-15[
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
]

* You can also use iterator with other iterable objects, e.g., tuple, list, dict.

---
# add `iterator` behavior to classes

* Define an `__iter__()` method which returns an object that has a `__next__()` method. 
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

```python
class MyCollection:
    def __init__(self):
        self.size=10
        self.data=list(range(self.size))
    def __iter__(self):
        self.index=0
        return self
    def __next__(self):
        if self.index>=self.size: 
            raise StopIteration
        n=self.data[self.index]
        self.index+=1
        return n

coll = MyCollection()
for x in coll:
    print(x)
```

---
# Generators

* They are written like regular functions but use the `yield` statement whenever they want to return data. 


* Generators are a simple and powerful tool for creating .red[iterators].
   * `__iter__()` and `__next__()` methods are created .red[automatically]


* when generators terminate, they automatically raise `StopIteration`.


* Each time the builtin function`next()` is called on it, the generator .red[resumes] where it left off 
   * it .red[remembers] all the data values and which statement was last executed. 
   * the local variables and execution state are .red[automatically saved between calls].


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

* .red[lazy] (=on demand) generation of items

* minimal memory load!
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
