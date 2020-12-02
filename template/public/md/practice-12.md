layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #12

---


template: base
layout: true

.mb-3[
## Recap
]

---

#### Stack and Queue

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


---


#### `deque` (pronounced "deck")

* “double-ended queue”


* Deques are a generalization of `stacks` and `queues` 


* Deques support thread-safe, memory efficient appends and pops from either side of the deque 
   * with approximately the same `O(1)` performance in either direction.


* Once a .red[bounded length deque] is .purple[full], when new items are added, a corresponding number of items are .purple[discarded] from the opposite end.


.center[<img src="https://user-images.githubusercontent.com/39995503/100534176-52ecfc00-324f-11eb-9158-500f73bfead1.png" width=700/>]


---

#### `deque` - Example

.font-12[
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

#### `deque` - Example (continued)

.font-12[
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

#### `Counter`

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

#### `Counter`

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

#### Common `Counter` Usage

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

template: base
layout: true

.mb-3[
## 오늘의 실습
]

---

#### 문제의 구성

* 2개의 문제
* 각각 Deque, defaultdict, Counter 등을 활용하여 푸는 것이 의도

---

template: base
layout: true

.mb-3[
## 오늘의 실습

#### Problem 1
]

---
이 문제에서는 유명한 [요세푸스 문제](https://en.wikipedia.org/wiki/Josephus_problem)를 풀어보겠습니다. n명의 사람들이 동그랗게 둘러 앉아 있습니다. 각 사람에게는 1, 2, 3, ..., n의 번호가 부여되어 있습니다. 또한 n보다 작은 자연수 k가 주어집니다. 게임이 시작하면 1번 사람이 바통을 들고 있다가 k번째 옆 사람에게 넘겨줍니다. 바통을 받은 사람은 게임에서 빠지고, 그 옆 사람이 바통을 이어받은 뒤 또 다시 k번째 옆 사람에게 넘겨줍니다. 이런 식으로 마지막 1명이 남을 때까지 계속됩니다.

예를 들어, n=5이고 k=3이라면 다음과 같이 진행됩니다. (**굵은 글씨**는 바통을 가지고 있다는 뜻입니다)

1. **1** 2 3 4 5 → 1 **2** 3 4 5 → 1 2 **3** 4 5 → 1 2 3 **4** 5 → 4 out → 1 2 3 **5**
2. 1 2 3 **5** → **1** 2 3 5 → 1 **2** 3 5 → 1 2 **3** 5 → 3 out → 1 2 **5**
3. 1 2 **5** → **1** 2 5 → 1 **2** 5 → 1 2 **5** → 5 out → **1** 2
4. **1** 2 → 1 **2** → **1** 2 → 1 **2** → 2 out → **1**

따라서, n=5이고 k=3일때 마지막으로 남는 사람은 1입니다.

---

Queue (혹은 Deque)를 사용하여 요세푸스 게임을 시뮬레이션하는 프로그램을 작성하세요. 주어진 n과 k에 대해 가장 마지막으로 남는 사람의 번호를 출력하면 됩니다. list를 사용해서 `.pop(0)`과 같이 시간이 오래 걸리는 메소드를 사용하면 시간 초과가 될 수 있습니다.

**Input**
1 이상의 자연수 n과 k가 띄어쓰기를 기준으로 구분되어 주어집니다. k는 항상 n보다 작습니다.
```
5 3
```

**Output**
```
1
```

---

template: base
layout: true

.mb-3[
## 오늘의 실습

#### Problem 2
]

---

당신은 슈퍼마켓을 운영하고 있습니다. 지금은 내일의 매장 오픈을 준비하기 위해 발주(=품목을 주문)를 할 시간입니다. 발주를 하는 방법은 다음과 같습니다.

1. 어제 팔린 품목들의 목록을 보고, 가장 많이 팔린 A개의 품목을 팔린 개수만큼 주문합니다.
    * 동률(tie)이 있다면 모두 포함시킵니다. 즉, A번째로 많이 팔린 품목과 동일한 개수만큼 팔린 다른 품목들이 있다면 해당하는 품목들도 모두 포함시켜서, 각각 팔린 개수만큼 주문합니다.
    * 남은 품목의 수보다 A가 더 크다면 모든 품목에 대해 위와 같이 주문합니다.
2. 위 1번 과정에서 주문되지 않은 품목들 중, 가장 적게 팔린 B개의 품목은 아예 주문하지 않습니다.
    * 마찬가지로 동률이 있다면 모두 포함시킵니다. 즉, B번째로 적게 팔린 품목과 동일한 개수만큼 팔린 다른 품목들이 있다면 해당하는 품목들도 모두 포함시켜서, 아무것도 주문하지 않습니다.
    * 남은 품목의 수보다 B가 더 크다면 모든 품목에 대해 위와 같이 주문합니다.
3. 위의 두 가지 경우에 속하지 않는 품목은 모두 C개씩 주문합니다.

---

당신은 위와 같은 방법으로 재고를 구축한 뒤 오늘의 장사를 시작합니다. (편의상 어제 팔고 남은 재고는 없다고 가정합니다. ) 오늘의 주문 목록이 들어올 때, (1) 주문이 모두 끝나고 남은 재고가 어떻게 되는지, 그리고 (2) 재고가 없어 팔지 못한 항목은 없는지를 계산하세요.


**Input**


```
1 1 1
apple banana pineapple orange
apple apple apple banana pineapple banana
apple orange orange banana banana
```

* 입력의 첫 줄에는 A B C가 띄어쓰기로 구분되어 주어집니다. A B C는 모두 0 이상의 정수입니다.
* 입력의 두 번째 줄에는 품목들이 띄어쓰기로 구분되어 주어집니다. 주어지는 품목들은 모두 서로 다릅니다.
* 입력의 세 번째 줄에는 어제 주문 된 품목들이 띄어쓰기로 구분되어 주어집니다.
* 입력의 네 번째 줄에는 오늘 주문 된 품목들이 띄어쓰기로 구분되어 주어집니다.

---

**Explanation**

* apple, banana, pineapple, orange의 4개 품목이 있습니다.
* 어제는 apple이 3개, banana가 2개, pineapple이 1개 팔렸습니다.
* 오늘의 재고를 주문합니다.
    * 가장 많이 팔린 A=1개의 품목, 즉 apple을 팔린 개수만큼 3개 삽니다.
    * 가장 적게 팔린 B=1개의 품목, 즉 orange를 아예 주문하지 않습니다.
    * 나머지인 banana와 pineapple을 C=1개씩 주문합니다.
    * 따라서 오늘의 재고는 apple 3개, banana 1개, pineapple 1개입니다.
* 오늘은 apple 1개, orange 2개, banana 2개를 주문 받았습니다.
    * apple은 3개 중 1개를 팔고 2개가 남았습니다.
    * orange는 재고에 없기 때문에 2개를 팔지 못했습니다.
    * banana는 재고에 있던 1개를 팔고, 1개는 재고가 부족해서 팔지 못했습니다.
    * 따라서 남은 재고는 apple 2개, banana 0개, pineapple 1개, orange 0개입니다.
    * 재고가 팔지 못한 개수는 apple 0개, banana 1개, pineapple 0개, orange 2개입니다.

---

**Output**

첫 줄에는 남은 재고를, 두 번째 줄에는 재고가 없어 팔지 못한 개수를 각각 한 줄에 출력합니다.
순서는 input에서 주어진 품목의 순서(=apple, banana, pineapple, orange)와 동일해야 합니다.

```
2 0 1 0
0 1 0 2 
```