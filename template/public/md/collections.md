layout: true

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# collections

<br/>

Jinwook Seo, Ph.D.  
Professor, Department of Computer Science and Engineering  
Seoul National University  

---
# `collections` module

* This module implements specialized container datatypes providing alternatives to Python’s general purpose built-in containers - `dict`, `list`, `set`, and `tuple`.
</br>
</br>
</br>

.font-15[
```
container           description
------------        -----------
deque               list-like container with fast appends and pops on either end
defaultdict         dict subclass that calls a factory function to supply missing values
OrderedDict         dict subclass that remembers the order entries were added
Counter             dict subclass for counting hashable objects
namedtuple()        factory function for creating tuple subclasses with named fields
ChainMap            dict-like class for creating a single view of multiple mappings
UserDict            wrapper around dictionary objects for easier dict subclassing
UserList            wrapper around list objects for easier list subclassing
UserString          wrapper around string objects for easier string subclassing
```
]

---
# `deque` (pronounced "deck")

* “double-ended queue”


* Deques are a generalization of `stacks` and `queues` 


* Deques support thread-safe, memory efficient appends and pops from either side of the deque 
   * with approximately the same `O(1)` performance in either direction.


* Once a .red[bounded length deque] is .purple[full], when new items are added, a corresponding number of items are .purple[discarded] from the opposite end.


.center[<img src="https://user-images.githubusercontent.com/39995503/100534176-52ecfc00-324f-11eb-9158-500f73bfead1.png" width=700/>]

---
# Stack and Queue

.row[
.col-6[
  
* `stack` 
   * .red[LIFO] (Last In First Out)
   * push(x)
   * pop()

</br>
</br>
<img src="https://upload.wikimedia.org/wikipedia/commons/b/b4/Lifo_stack.png" width=350/>
]
.col-6[
  
* `queue` 
   * .red[FIFO] (First In First Out)
   * enqueue(x)
   * dequeue()

</br>
</br>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/1280px-Data_Queue.svg.png" width=350/>
]
]

https://en.wikipedia.org/wiki/Stack_(abstract_data_type)
https://en.wikipedia.org/wiki/Queue_(abstract_data_type)
---
# Using Lists as Stacks
.row[
.col-4[
```python3
>>> stack = [3, 4, 5]
>>> stack.append(6)
>>> stack.append(7)
>>> stack
[3, 4, 5, 6, 7]
>>> stack.pop()
7
>>> stack
[3, 4, 5, 6]
>>> stack.pop()
6
>>> stack.pop()
5
>>> stack
[3, 4]
```
]
.col-8[

<img src="https://upload.wikimedia.org/wikipedia/commons/b/b4/Lifo_stack.png" width=300/>  
`stack` - .red[LIFO] (Last In First Out)
]
]

---
# Using Lists as Queue
.row[
.col-4[
```python3
>>> queue = [3, 4, 5]
>>> queue.append(6)
>>> queue.append(7)
>>> queue
[3, 4, 5, 6, 7]
>>> queue.pop(0)
3
>>> queue
[4, 5, 6, 7]
>>> queue.pop(0)
4
>>> queue.pop(0)
5
>>> queue
[6, 7]
>>> 
```
]
.col-8[
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/1280px-Data_Queue.svg.png" width=200>  
`queue` - .red[FIFO] (First In First Out)

* `pop(0)` is slow : `O(n)`

.font-14[
```python3
>>> from collections import deque
>>> queue = deque(["Eric", "John", "Michael"])
>>> queue.append("Terry")           # Terry arrives
>>> queue.append("Graham")          # Graham arrives
>>> queue.popleft()                 # The first to arrive now leaves
'Eric'
>>> queue.popleft()                 # The second to arrive now leaves
'John'
>>> queue                           # Remaining queue in order of arrival
deque(['Michael', 'Terry', 'Graham'])
```
]
]
]


---
# `deque` - Example

.font-14[
```python3
>>> from collections import deque
>>> d = deque('ghi')                 # make a new deque with three items
>>> for elem in d:                   # iterate over the deque's elements
...     print(elem.upper())
G
H
I

>>> d.append('j')                    # add a new entry to the right side
>>> d.appendleft('f')                # add a new entry to the left side
>>> d                                # show the representation of the deque
deque(['f', 'g', 'h', 'i', 'j'])

>>> d.pop()                          # return and remove the rightmost item
'j'
>>> d.popleft()                      # return and remove the leftmost item
'f'
>>> list(d)                          # list the contents of the deque
['g', 'h', 'i']
>>> d[0]                             # peek at leftmost item
'g'
>>> d[-1]                            # peek at rightmost item
'i'
>>> list(reversed(d))                # list the contents of a deque in reverse
['i', 'h', 'g']
```
]
---
# `deque` - Example (continued)

.font-14[
```python3
>>> 'h' in d                         # search the deque
True
>>> d.extend('jkl')                  # add multiple elements at once
>>> d
deque(['g', 'h', 'i', 'j', 'k', 'l'])
>>> d.rotate(1)                      # right rotation
>>> d
deque(['l', 'g', 'h', 'i', 'j', 'k'])
>>> d.rotate(-1)                     # left rotation
>>> d
deque(['g', 'h', 'i', 'j', 'k', 'l'])

>>> deque(reversed(d))               # make a new deque in reverse order
deque(['l', 'k', 'j', 'i', 'h', 'g'])
>>> d.clear()                        # empty the deque
>>> d.pop()                          # cannot pop from an empty deque
Traceback (most recent call last):
    File "<pyshell#6>", line 1, in -toplevel-
        d.pop()
IndexError: pop from an empty deque

>>> d.extendleft('abc')              # extendleft() reverses the input order
>>> d
deque(['c', 'b', 'a'])
```
]

---
# `deque` Recipies

* .red[Bounded length deques] provide functionality similar to the `tail` filter in Unix:

```python3
def tail(filename, n=10):
    'Return the last n lines of a file'
    with open(filename) as f:
        return deque(f, n)
```

---
# `deque` Recipies

```python
from collections import deque
import itertools

def moving_average(iterable, n=3):
    # moving_average([40, 30, 50, 46, 39, 44]) --> 40.0 42.0 45.0 43.0
    # http://en.wikipedia.org/wiki/Moving_average
    it = iter(iterable)
    d = deque(itertools.islice(it, n-1))
    d.appendleft(0)
    s = sum(d)
    for elem in it:
        s += elem - d.popleft()
        d.append(elem)
        yield s / n

  
r = [each for each in moving_average([40, 30, 50, 46, 39, 44])]
print(r)  # [40.0, 42.0, 45.0, 43.0]
```

---
# `deque` Recipies - Round-robin

* A .red[round-robin scheduler] can be implemented with input iterators stored in a `deque`.


* .red[Round-robin (RR)] is one of the algorithms employed by .red[process] and network .red[schedulers] in computing.
   * a round-robin scheduler generally employs .red[time-sharing], 
   * giving each job a time slot (its allowance of CPU time), 
   * and interrupting the job if it is not completed by then (preemptive)
   * time slices are assigned to each process in .red[equal] portions and in circular order, handling all processes .red[without priority].

<img src="https://upload.wikimedia.org/wikipedia/commons/7/76/Round_Robin_Schedule_Example.jpg" width=650/>

---
# `deque` Recipies - Round-robin

* Values are yielded from the active iterator in position zero. 
   * If that iterator is exhausted, it can be removed with `popleft()`; 
   * otherwise, it can be .red[cycled back] to the end with the `rotate()` method:


.font-15[
```python
from collections import deque
import itertools

def roundrobin(*iterables):
    "roundrobin('ABC', 'D', 'EF') --> A D E B F C"
    iterators = deque(map(iter, iterables))
    while iterators:
        try:
            while True:
                yield next(iterators[0])
                iterators.rotate(-1)
        except StopIteration:
            # Remove an exhausted iterator.
            iterators.popleft()

schedule = [slice for slice in roundrobin('ABC', 'D', 'EF')]
print(schedule)
```
]



---
# `defaultdict`

* a dictionary that always provides a .red[default value] (even when a key is not in the dictionary)
   * note: `KeyError` raised when a key is not there in a regular `dict` object


* `class collections.defaultdict([default_factory[, ...]])`
   * `defaultdict` is a subclass of the built-in `dict` class. 
   * Using `list` as the `default_factory`, it is easy to .red[group] a .purple[sequence of key-value pairs] into a .red[dictionary of lists]:i.e., default value is an empty list (`[]`)
   * the first parameter(`default_factory`) defaults to `None`

.font-15[
```python
from collections import defaultdict

s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1), ('blue', 4)]
d = defaultdict(list)  # 'list()' returns an empty list
for k, v in s:
    d[k].append(v)

result = sorted(d.items())
print(result)
# [('blue', [2, 4, 4]), ('red', [1]), ('yellow', [1, 3])]
```
]

---
.font-15[
```python3
from collections import defaultdict

s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1), ('blue', 4)]
d = defaultdict(list)
for k, v in s:
    d[k].append(v)

result = sorted(d.items())
print(result)
# [('blue', [2, 4, 4]), ('red', [1]), ('yellow', [1, 3])]
```
]

is *faster* and *simpler* than (using a regular `dict`)

.font-14[
```python3
s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1), ('blue', 4)]
d = {}
for k, v in s:
    d.setdefault(k, []).append(v)

result = sorted(d.items())
print(result)
```
]
.font-14[
```python3
dict.setdefault(key[, default])
    If key is in the dictionary, return its value. 
    If not, insert key with a value of default and return default. default defaults to None.
```
]

---
# `defaultdict`

* Setting the `default_factory` to `int` makes the `defaultdict` useful for .red[counting]
   * `int()` returns `0`:i.e., default value is `0`

.font-15[
```python
from collections import defaultdict

s = 'mississippi'
d = defaultdict(int)
for k in s:
    d[k] += 1

result = sorted(d.items())
print(result)
# [('i', 4), ('m', 1), ('p', 2), ('s', 4)]
```
]

* When a letter is first encountered, it is missing from the mapping, so the `default_factory` function calls `int()` to .red[supply a default] count of `zero`. 
   * The function `int()` which always returns `zero` is just a special case of .red[constant functions]


---
# `defaultdict`

* A faster and more flexible way to create .red[constant functions] is to use a `lambda` function which can supply any constant value (not just zero):

```python
from collections import defaultdict

def constant_factory(value):
    return lambda: value
    
d = defaultdict(constant_factory('<missing>'))
# d = defaultdict(lambda:'<missing>')  # you can do just like this

d.update(name='John', action='ran')
print('%(name)s %(action)s to %(object)s' % d)
# John ran to <missing>
d['object']='Jane'
print('%(name)s %(action)s to %(object)s' % d)
# John ran to Jane
```

---
# `defaultdict`

* Setting the `default_factory` to `set` makes the `defaultdict` useful for building a .red[dictionary of sets]:
   * no duplicates in a set by definition

.font-15[
```python
from collections import defaultdict

s = [('red', 1), ('blue', 2), ('red', 3), ('blue', 4), ('red', 1), ('blue', 4)]
d = defaultdict(set) # 'set()' returns an empty set -> default value
for k, v in s:
    d[k].add(v)

result = sorted(d.items())
print(result)
#[('blue', {2, 4}), ('red', {1, 3})]
```
]

---
# `OrderedDict`

* If you want to make a dictionary that keeps .red[insertion order], use `OrderedDict`

```python
from collections import OrderedDict

d = {'x':100, 'y':200, 'z':300, 'l':500}
print(d.items())

od = OrderedDict(sorted(d.items(), key = lambda x:x[0]))
print(od.items())

od = OrderedDict(sorted(d.items(), key = lambda x:x[1]))
print(od.items())
```

* `OrderedDict` has become less important now that the built-in `dict` class gained the ability to .red[remember insertion order] (guaranteed in Python 3.7).

---
# `OrderedDict`

* The regular `dict` was designed to be very good at .red[mapping] operations. 
   * Tracking insertion order was secondary.


* The `OrderedDict` was designed to be good at .red[reordering] operations. 
   * Space efficiency, iteration speed, and the performance of update operations were secondary.


* `OrderedDict` can .red[handle frequent reordering operations better] than `dict`. 
   * This makes it suitable for .red[tracking recent accesses] (e.g., in an .red[LRU] cache).


* The .red[equality] operation for `OrderedDict` checks for matching order.

.font-14[
```python3
>>> dict1 = {'A':1, 'B':2, 'C':3}
>>> dict2 = {'A':1, 'C':3, 'B':2}
>>> dict1 == dict2
True
>>> from collections import OrderedDict
>>> odict1 = OrderedDict({'A':1, 'B':2, 'C':3})
>>> odict2 = OrderedDict({'A':1, 'C':3, 'B':2})
>>> odict1 == odict2
False
>>> 
```
]

---
# `OrderedDict`

* `OrderedDict` has a `move_to_end()` method to efficiently .red[reposition] an element to an endpoint.


```python3
>>> d = OrderedDict.fromkeys('abcde')
>>> d.move_to_end('b')             # move to the end
>>> ''.join(d.keys())
'acdeb'
>>> d.move_to_end('b', last=False) # move to the beginning
>>> ''.join(d.keys())
'bacde'
```

---
# `OrderedDict`

* It is straightforward to create an ordered dictionary variant that .red[remembers the order the keys were last inserted]. 
   * If a new entry overwrites an existing entry, the original insertion position is changed and moved to the end:


```python3
class LastUpdatedOrderedDict(OrderedDict):
    'Store items in the order the keys were last added'

    def __setitem__(self, key, value):
        super().__setitem__(key, value)
        self.move_to_end(key)
```

---
# `Counter`

* A `Counter` is a `dict` subclass for counting hashable objects. 
* A counter tool is provided to support convenient and rapid .red[tallies]. 

.font-15[
```python3
>>> # Tally occurrences of words in a list
>>> cnt = Counter()
>>> for word in ['red', 'blue', 'red', 'green', 'blue', 'blue']:
...     cnt[word] += 1
>>> cnt
Counter({'blue': 3, 'red': 2, 'green': 1})

>>> # Find the ten most common words in Hamlet
>>> import re
>>> words = re.findall(r'\w+', open('hamlet.txt').read().lower()) # \w : word letter
>>> Counter(words).most_common(10)
[('the', 1143), ('and', 966), ('to', 762), ('of', 669), ('i', 631),
 ('you', 554),  ('a', 546), ('my', 514), ('hamlet', 471), ('in', 451)]
```
]

---
# `Counter`

* creating a Counter object
```python3
>>> c = Counter()                           # a new, empty counter
>>> c = Counter('gallahad')                 # a new counter from an iterable
>>> c = Counter({'red': 4, 'blue': 2})      # a new counter from a mapping
>>> c = Counter(cats=4, dogs=8)             # a new counter from keyword args
```

* counting missing elements
```python3
>>> c = Counter(['eggs', 'ham'])
>>> c['bacon']                              # count of a missing element is 0
0
```

* iterating over elements
```python3
>>> c = Counter(a=4, b=2, c=0, d=-2)
>>> sorted(c.elements())          # repeating each as many times as its count
['a', 'a', 'a', 'a', 'b', 'b']
```
---
* getting *n* most common elements

```python3
Counter('abracadabra').most_common(3)
[('a', 5), ('b', 2), ('r', 2)]
```
* `subtract`, and math operations

.font-15[
```python3
>>> c = Counter(a=4, b=2, c=0, d=-2)
>>> d = Counter(a=1, b=2, c=3, d=4)
>>> c.subtract(d)
>>> c
Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
>>> c = Counter(a=3, b=1)
>>> d = Counter(a=1, b=2)
>>> c + d                       # add two counters together:  c[x] + d[x]
Counter({'a': 4, 'b': 3})
>>> c - d                       # subtract (keeping only positive counts)
Counter({'a': 2})
>>> c & d                       # intersection:  min(c[x], d[x]) 
Counter({'a': 1, 'b': 1})
>>> c | d                       # union:  max(c[x], d[x])
Counter({'a': 3, 'b': 2})
```
]

---
# Common `Counter` Usage

```python3
sum(c.values())                 # total of all counts
c.clear()                       # reset all counts
list(c)                         # list unique elements
set(c)                          # convert to a set
dict(c)                         # convert to a regular dictionary
c.items()                       # convert to a list of (elem, cnt) pairs
Counter(dict(list_of_pairs))    # convert from a list of (elem, cnt) pairs
c.most_common()[:-n-1:-1]       # n least common elements
+c                              # remove zero and negative counts
```

* Unary addition and subtraction
   * keeping only .red[positive] counts

```python3
>>> c = Counter(a=2, b=-4)
>>> +c               # adding an empty counter
Counter({'a': 2})
>>> -c               # subtracting from an empty counter
Counter({'b': 4})
```

---
# `namedtuple` Factory Function

* Named tuples .red[assign meaning to each position] in a tuple and allow for .red[more readable, self-documenting] code. 
   * can be used wherever regular tuples are used, and they add the ability to .red[access fields by name] instead of position index.


* collections.`namedtuple`(`typename`, `field_names`, *, rename=False, defaults=None, module=None)
   * Returns a new tuple subclass named `typename`. 
   * It is used to create tuple-like objects that have fields (`field_names`) accessible by attribute lookup as well as being indexable and iterable.

.font-14[

```python
from collections import namedtuple

Point = namedtuple('pt', ['x','y'])
p = Point(y=11, x=22)
print(p)  # prints "pt(x=22, y=11)"

print(p[0] + p[1])
print(p.x + p.y)  # we can do this with "names"

p[0] = 40  # raise "TypeError" (tuple is immutable)
```

]


---
# Acknowledgement

* https://docs.python.org/3/library/collections.html