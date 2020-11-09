layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# Object-Oriented Prgramming in Python

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  


---
# Procedural -> Object-oriented

* Procedural Programming (before mid 80’)
   * Control-oriented Programming
   * Real world problem -> a set of .red[functions]
   * Data and functions are .purple[separately] treated
   * Fortran, Cobol, PL/1, Pascal, C (1972, Bell Lab)


* Object-oriented Programming (after mid 80’)
   * Real world problem -> a set of .red[classes]
   * Data and functions that operate on the data are .purple[**encapsulated] inside classes**
   * C++ (1983, Bell Lab)
   * Python (1991)
   * Java (1993)
   * and most Script Languages (Ruby, PHP, R,…)

---
# Procedural Programming

* Writing programs made of .red[functions] that perform specific tasks
* Procedures(i.e., functions) typically operate on data items that are .red[separate] from the procedures
* Data items commonly passed from one procedure to another
* Focus: to create .red[procedures] (or .red[fuctions]) that operate on the program’s data

---

# Object-Oriented Programming

* Focused on creating .red[objects] (instantces of clases)
* Object: entity that contains (i.e., encapsulates) data and procedures/functions
* Data is known as .red[data attributes] and procedures are known as .red[method attributes]
* Method attributes (or Methods) perform operations on the data attributes


* **Encapsulation**: 
  * combining data and code/procedures into a single object
* **Information Hiding**:
  * .red[Hide details] so that a programmer implementing the class is free to change the implementation without worrying that the change will break code that uses the class
  * hide implementation details to users
  * reveal only the interfaces (specifications)
 
---

# Abstract Data Type in Python

* An **abstract data type** is a set of .red[objects] and the .red[operations] on those objects
   * objects and operations are bound together
   * data attributes + method attributes


* We have been already used ADT
   * Objects are the core things that Python programs manipulate
   * Buit-in (abstract data) types: `int`, `float`, `str`, `list`, `dict`, and etc
   
   
* We can implement our own new abstract data type (.red[ADT]) using .red[classes]

---

# Abstract Data Type in General

* A class that uses .red[data abstraction] and .purple[encapsulation] defines an abstract data type 


* In an abstract data type, the class designer worries about .red[how the class is implemented]


* Programmers who use the class .red[need not know how] the abstract data type works internally
   * They can instead .red[think abstractly about what] the type does
   * We have used built-in types without giving any thoughts to how these types mihgt be implemented
---

# Data Abstraction and Encapsulation

* The fundamental ideas behind **classes** are .red[data abstraction] and .red[encapsulation]
* .red[Data abstraction] is a programming (and design) technique that relies on the **separation** of .purple[interface] and .blue[implementation] 
* The .purple[interface] of a class consists of 
   * the .red[operations] that users of the class can execute 
* The .blue[implementation] includes 
   * the class’ .red[data members], 
   * the .red[bodies of the functions] that constitute the interface, 
   * any (private) functions needed to define the class (not for general use)
* .red[Encapsulation]: combining data and code into a single object
   * enforces the separation of a class’ interface and implementation
   * a class that is encapsulated .red[hides its implementation]
   * users of the class can use the interface but have .red[no access to the implementation]

---
# Decomposition and Abstraction

* two mechanisms to help us manage complexity in a way that facilitates changes in real world


* .red[Decomposition] creates structure in a probem
   * design programs using many different classes


* .red[Abstraction] surpresses (i.e., hides) details


* The key is to suppress the **appropriate** details
   * create domain-speific types (i.e., ADTs) -> data abstraction
---
# Class

* code that specifies the data attributes and methods of a particular type of object
   * Similar to a .red[blueprint] of a house or a cookie cutter

--

# Instance

* an object created from a class
   * Similar to a .red[specific house] built according to the blueprint or .red[cookies] made with the cookie cutter
   * There can be many instances of one class


<img src="https://user-images.githubusercontent.com/39995503/96365740-ad3d6c00-117d-11eb-85ee-da8018054506.png" width=500>

---
# Class Definition

* set of statements that define a class’s methods and data attributes
   * Format: begin with `class Class_name:`
   * Class names often start with **uppercase** letter


* Method definition looks like any other python .purple[function] definition


* `self` parameter of methods
   * required in every method in the class
   * .purple[references the specific object that the method is working on]
   * this is nothing more than a convention: the name `self` has absolutely no special meaning to Python


* Initializer method
   * Format: `def __init__ (self):`
   * .red[automatically executed when an instance of the class is created]
   * initializes object’s data attributes 
   * .purple[assigns `self` parameter to the object that was just created]
   * usually the first method in a class definition
   
---
# Example ADT - `Human`

* definition of `Human` class
   * data attributes: `name`, `friend`
   * method attributes: `__init__`, `say_name`, `say_goodnight`
   
   
.row[
.col-7[
```python3
class Human(object):
    def __init__(self, name, friend=None):
        self.name = name
        self.friend = friend
    def say_name(self):
        print("My name is "+self.name)
    def say_goodnight(self):
        if self.friend is None:
            print("Good night nobody.")
        else:
            print("Good night "+self.friend.name)
```
]
.col-5[

<img src="https://user-images.githubusercontent.com/39995503/96364823-82501980-1177-11eb-917d-c5c421e9f430.png" width=370>
]
]

https://simple.wikipedia.org/wiki/Object-oriented_programming

---
# Data/Method Attributes

* **Data attributes**: define the state of an object
   * `name`, `friend`


* **Private data attributes**: keep external code from accessing it
   * place two underscores (`__`) in front of attribute name
   * an object’s data attributes are better to be .red[private]
   * .red[private] attributes that cannot be accessed except from inside an object .red[don’t exist] in Python
   * but (limitedly) supported through .red[name mangling]


* **Public methods**: allow external code to manipulate the object
   * `say_name`(), `say_goodnight`()
   * define interfaces of a class/instance


* **Private methods**: used for object’s inner workings
   * external code cannot use (i.e., call/invoke) them
   * place two underscores (`__`) in front of method name
   * (limitedly) supported through .red[name mangling]

---
 
# Create an Instance

* To create a new instance of a class, call the initializer method (i.e., constructor)
   * Format: `My_instance = Class_Name()`


* To call any of the methods for the created instance, use .red[dot] notation
   * Format: `My_instance.method()`
   * Reference to `self` is passed automatically
   * Because the `self` parameter references the .red[specific instance] of the class, the method will affect that instance


---

# How to Use `Human` class

```python3
# Create a new Human object named stephen with name "Stephen"
stephen = Human("Stephen")

# Create a new Human object named joe with name "Joe" and stephen as a friend
joe = Human("Joe", stephen)

stephen.say_name()      # Shows 'My name is Stephen'
stephen.say_goodnight() # Shows 'Good night nobody.'
joe.say_name()          # Shows 'My name is Joe'
joe.say_goodnight()     # Shows 'Good night Stephen'
```
https://simple.wikipedia.org/wiki/Object-oriented_programming

---

# Working With Instances

* .red[Instance attribute]: belongs to a specific .red[instance] of a class
   * created when a method uses the `self` parameter to create an attribute


* If many instances of a class are created, each would have its own set of attributes


.center[<img src="https://user-images.githubusercontent.com/39995503/96367603-d3690900-1189-11eb-8ea3-89f8c4f0fb84.png" width=400>]

---
# Class and Instance Atrributes

* instance variables are for data unique to each instance 
* class variables are for attributes and methods shared by all instances of the class

```python3
class Dog:

    kind = 'canine'         # class variable shared by all instances

    def __init__(self, name):
        self.name = name    # instance variable unique to each instance

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.kind                  # shared by all dogs
'canine'
>>> e.kind                  # shared by all dogs
'canine'
>>> d.name                  # unique to d
'Fido'
>>> e.name                  # unique to e
'Buddy'
```

---
# Bundling named data items

.row[
.col-6[
* clients may add data attributes of their own to an instance object without affecting the validity of the methods

```python3
class Employee:
    pass

# Create an empty employee record
john = Employee() 
# Fill the fields of the record
john.name = 'John Doe'
john.dept = 'computer lab'
john.salary = 1000
```
]
.col-6[
* If the same attribute name occurs in both an instance and in a class, then attribute lookup prioritizes the instance:

```python3
>>> class Warehouse:
        purpose = 'storage'
        region = 'west'
>>> w1 = Warehouse()
>>> print(w1.purpose, w1.region)
storage west
>>> w2 = Warehouse()
>>> w2.region = 'east'
>>> print(w2.purpose, w2.region)
storage east
```
]
]

* `pass` is a null operation -- when it is executed, nothing happens. 
   * useful as a .red[placeholder] when a statement is .red[required syntactically], but no code needs to be executed.

---
# Add/Remove/Modify Attributes

```python3
class Dog:
    kind = 'canine'         # class variable shared by all instances
    def __init__(self, name):
        self.name = name    # instance variable unique to each instance

>>> d = Dog('Fido')
>>> e = Dog('Buddy')
>>> d.kind = 'dog'          # adding an instance variable, kind to d
>>> e.kind = 'gangaji'      # adding an instance variable, kind to e
>>> d.kind                  # instance variable
'dog'
>>> e.kind                  # instance variable
'gangaji'
>>> Dog.kind                # class variable
'canine'
>>> d.__dict__
{'name': 'Fido', 'kind': 'dog'}
```

---
# Add/Remove/Modify Attributes
```python3
class Dog:
    kind = 'canine'         # class variable shared by all instances
    def __init__(self, name):
        self.name = name    # instance variable unique to each instance

>>> d = Dog('Fido')
>>> d.age = 1       # add an attribute 'age'
>>> d.sex = 'male'  # add an attribute 'sex'
>>> del d.age       # delete the attritue 'age'
```
* But the class definition doesn't change, only the object changes
* We may also use the following built-in functions
   * `setattr(obj, name, value)` : to set an attribute. If attribute does not exist, then it would be created.
   * `hasattr(obj, name)` : to check if an attribute exists or not
   * `getattr(obj, name[, default])` : to access the attribute of object
   * `delattr(obj, name)` : to delete an attribute.

---
# Built-in Special Variables

* `__dict__` : Dictionary containing the class’s namespace.
* `__doc__` : Class documentation string or None if undefined.
* `__name__` : Class name.
* `__module__` : Module name in which the class is defined. This attribute is `__main__` in interactive mode.
* `__bases__` : A possibly empty tuple containing the base classes, in the order of their occurrence in the base class list.

---
```python3
class Employee:
    'Common base class for all employees'
    empCount=0
    def __init__(self,name,salary):
       self.name=name
       self.salary=salary
       Employee.empCount+=1
    def displayCount(self):
       print("TotalEmployee%d" % Employee.empCount)
    def displayEmployee(self):
       print("Name:",self.name,",salary:",self.salary)

emp1=Employee("Zara",2000)
emp2=Employee("Manni",5000)
emp1.displayEmployee( )
emp2.displayEmployee( )
print("TotalEmployee%d" % Employee.empCount)
```
---
```python3
>>> Employee.__doc__
'Common base class for all employees'
>>> Employee.__name__
'Employee'
>>> Employee.__module__
'__main__'
>>> Employee.__bases__
(<class 'object'>,)
>>> Employee.__dict__
mappingproxy({'__module__': '__main__', '__doc__': 'Common base class for all employees', 'empCount': 2, '__init__': <function Employee.__init__ at 0x7f9b8fed2af0>, 'displayCount': <function Employee.displayCount at 0x7f9b8fed2b80>, 'displayEmployee': <function Employee.displayEmployee at 0x7f9b8fed2c10>, '__dict__': <attribute '__dict__' of 'Employee' objects>, '__weakref__': <attribute '__weakref__' of 'Employee' objects>})
>>> 
```
---
# Information Hiding with Private Members

* In C++ terminology, normally class members (including the data members) are .red[public], and all member functions are .red[virtual]. 


* .red[Private] instance variables that cannot be accessed except from inside an object
   * .red[information hiding]
   
   
* .red[Private] instance variables that cannot be accessed except from inside an object .red[don’t exist] in Python


* but there is limited support for such a mechanism, called .red[name mangling]
  * Any identifier of the form `__spam` (.red[at least two leading underscores, at most one trailing underscore]) is textually replaced with `_classname__spam`, where `classname` is the current class name with leading underscore(s) stripped. 

---
# Accesing Private Members

```python
class Human(object):
    def __init__(self, name):
        self.name = name
        self.__invisible = 'Do not look at me directly'
    def __printInvisible(self):   # this is private
        print(self.__invisible)
    def printInvisible(self):
        print(self.__invisible)
    def __printInvisible__(self): # this is not private
        print(self.__invisible)
# Create a new Human object named stephen with name "Stephen"
stephen = Human("Stephen")
stephen.printInvisible()
stephen.__printInvisible__() # works well
print(stephen.__invisible)  
# AttributeError: 'Human' object has no attribute '__invisible'
stephen.__printInvisible() 
# AttributeError: 'Human' object has no attribute '__printInvisible'
```
---
# `__str__` method

* Object’s state: the values of the object’s attributes at a given moment


* `__str__` method: displays the object’s state
   * automatically called when the object is passed as an argument to the `print` function
   * automatically called when the object is passed as an argument to the `str` function
---
```python
class IntSet(object):
    def __init__(self):
       self.vals = []
    def insert(self, e):
       if e not in self.vals:
           self.vals.append(e)
    def __str__(self):
       self.vals.sort()
       result = ''
       for e in self.vals:
           result = result + str(e) + ','
       return '{' + result[:-1] + '}' 
       
s = IntSet()
s.insert(3)
s.insert(4)
print(s)
```

---
# Accessor and Mutator

* Typically, all of a class’s data attributes are private and provide methods to access and change them


* Accessor methods (getter): 
   * return a value from a class’s attribute without changing it
   * provide a safe way for code outside the class to .red[retrieve] the value of attributes


* Mutator methods (setter): 
   * store or change the value of a data attribute
   * provide a safe way for code outside the class to .red[change] the value of attributes

---
# Accessor and Mutator

```python
class Human(object):
    def __init__(self, name, friend=None):
        self.__name = name
        self.__friend = friend
    def get_name():
        return self.__name
    def set_name(self, name):
        self.__name = name

# Create a new Human object named stephen with name "Stephen"
stephen = Human("Stephen")
print(stephen.get_name())
stephen.set_name("Stephen Clinton")
print(stephen.get_name())
```
---
# Passing Objects as Arguments

* Methods and functions often need to accept objects as arguments


* When you pass an object as an argument, you are actually passing a .red[reference] to the object
   * The receiving method or function has access to the actual object
   * Methods of the object can be called within the receiving function or method, and data attributes may be changed using mutator methods


* all instances of user-defined classes can be used as dictionary (`dict`) keys
   * they are 'hashable'

---
# Instance vs. Class Variables
# Instance vs. Class Methods

* `class SNUStudent`


* **Instance Variable**: variable belonging to an instacne
   * `Name`, `Student_ID` , `Courses`, `GPA`


* **Class Variable**: variable shared by all instances of a Class
   * `University_name`


* **Instance Method**: method for an instance
   * `s.gpa()`: return gpa of an instance s
   * `s.taken_course()`: return list of courses that s has taken


* **Class Method**: method for the entire class
   * `SNUStudent.num_students()`: return the number of students of the class type
   * `SNUStudent.avg_gpa()`: return the average gpa of all SNU students
   
---
# Class Method

```python
class A(object):

    def foo(self):
        print('executing foo')
        
    @classmethod          # decorator
    def class_foo(cls):   # use cls instead of self
        print('executing class_foo')

a = A()
A.class_foo()
a.foo()
a.class_foo()
```
---

# The Software Development Process: The WaterFall Model

* **.purple[Analyze] the Problem**
   * Figure out exactly the problem to be solved.
* **Determine .purple[Specifications]**
   * Describe exactly what your program will do. (not How , but What)
   * Includes describing the inputs, outputs, and how they relate to one another.
* **Create a .purple[Design]**: Formulate the overall structure of the program. 
   * 'how' of the program gets worked out - algorithms
* **.purple[Implement] the Design**: coding!
   * Translate the design into a programming language.
* **.purple[Test/Debug] the Program**: Try out your program to see if it worked.
   * Your goal is to find errors, so try everything that might “break” your program!
* **.purple[Maintain] the Program**
   * Continue developing the program in response to the needs of your users.
   * Most SW developments are never completely finished, they evolve over time.

---
# Techniques for Designing Classes

* UML diagram: standard diagrams for graphically depicting object-oriented systems
   * Stands for Unified Modeling Language


* General layout of Class Diagram: box divided into three sections
   * Top section: name of the class
   * Middle section: list of data attributes
   * Bottom section: list of class methods

.center[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/41/BankAccount1.svg/1920px-BankAccount1.svg.png" width=350>]

---
# Example Class Diagram

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/UML_diagrams_overview.svg/1920px-UML_diagrams_overview.svg.png" width=800>

---
# Finding Classes in Problem

* When developing object oriented program, first goal is to identify classes
   * Typically involves identifying the real-world objects that are in the problem


* Technique for identifying classes:
   * Get written description of the problem domain
   * Identify all .red[nouns] in the description, each of which is a potential class
   * Refine the list to include only classes that are relevant to the problem


* refer to **Chapter 10** for a specific example

---
# Finding Classes in Problem

* Get written description of the problem domain
   * May be written by you or by an expert


* Should include any or all of the following:
   * Physical objects simulated by the program
   * The role played by a person 
   * The result of a business event
   * Recordkeeping items
   

* Example:

```
Joe’s Automotive Shop services foreign cars and specializes in servicing cars made by
Mercedes, Porsche, and BMW. When a customer brings a car to the shop, the manager gets
the customer’s name, address, and telephone number. The manager then determines the make,
model, and year of the car, and gives the customer a service quote. The service quote shows
the estimated parts charges, estimated labor charges, sales tax, and total estimated charges.
```

---
# Finding Classes in Problem

.row[
.col-8[
* Identify all nouns 
   * each of which is a potential class


* Should include noun phrases and pronouns


* Some nouns may appear multiple times
]
.col-4[
```
address
BMW
car
cars
customer
estimated labor charges
estimated parts charges
foreign cars
Joe’s Automotive Shop
make
manager
Mercedes
model
name
Porsche
sales tax,
service quote
shop
telephone number
total estimated charges
year
```
]
]

---
# Finding Classes in Problem

.row[
.col-8[

* Refine the list to include only classes that are relevant to the problem
   * Keep your .red[goal] in mind: "to print service quotes for customers"
   * Remove nouns that mean the same thing
   * Remove nouns that represent items that the program does not need to be concerned with
   * Remove nouns that represent objects, not classes
   * Remove nouns that represent simple values that can be assigned to a variable
]
.col-4[

~~address~~  
~~BMW~~  
car  
~~cars~~  
customer  
~~estimated labor charges~~  
~~estimated parts charges~~  
~~foreign cars~~  
~~Joe’s Automotive Shop~~  
~~make~~  
~~manager~~  
~~Mercedes~~  
~~model~~  
~~name~~  
~~Porsche~~  
~~sales tax~~  
service quote  
~~shop~~  
~~telephone number~~  
~~total estimated charges~~  
~~year~~  

]
]

---
# Identify Responsibilities of Class

* A classes responsibilities are:
   * The things the class is responsible for knowing -> .red[data attributes]
   * The actions the class is responsible for doing -> .red[method attribute]


* To find out a class’s responsibilities look at the problem domain
   * Deduce required information and actions


<img src="https://user-images.githubusercontent.com/39995503/96371187-74ac8b00-119b-11eb-82b9-ea9b8fb53f05.png" width=200>
<img src="https://user-images.githubusercontent.com/39995503/96371202-82faa700-119b-11eb-97d6-d37e6f51418f.png" width=200>
<img src="https://user-images.githubusercontent.com/39995503/96371239-a9b8dd80-119b-11eb-9ada-e75ded46f4f6.png" width=250>
---
# Acknowledgement

* The Python Tutorial, https://docs.python.org/3/tutorial/index.html
* Lecture Notes, Professor Hyungjoo Kim
* Starting out with Python, Professor Tony Gaddis and Pearson Education, Ltd.
* Introduction to Computation and Programming Using Python, John V. Guttag