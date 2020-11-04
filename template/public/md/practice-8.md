layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #8

---


template: base
layout: true

.mb-3[
## Recap
]

---

#### Class

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

#### How to Use `Human` class

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

#### Specially Named Methods

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

#### SNUPerson: derived class
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

#### SNUPerson: derived class

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
      * `__lt__` : overrides the `__init__` of the super class, Person
---

template: base
layout: true

.mb-3[
## 오늘의 실습
]

---

#### 문제의 구성

* 1개의 문제가 3개의 소문제로 구성되어 있음 (Easy, Normal, Hard)
* class를 활용하여 코딩하는 것이 의도

#### 진행 방식

* 첫 번째 소문제는 실습시간에 live 힌트 제공 (따로 업로드 안함)
* 두 번째 소문제는 평소처럼 진행
* 세 번째 소문제는 보너스 문제처럼 실습 중 질문 불허

[참고 자료](https://ncase.me/trust/)
   
---

template: base
layout: true

.mb-3[
## 오늘의 실습

#### subproblem 1
]

---

* 이 문제에서 등장하는 사람은 모두 Giver 혹은 Taker

```python3
GGTGT
```

* 각 사람은 왼쪽부터 순서대로 id를 0부터 N-1까지 부여
* 위의 예시의 경우 0번 사람이 Giver, 1번 사람이 Giver, 2번 사람이 Taker, 3번 사람이 Giver, 4번 사람이 Taker인 상황
* 같은 Giver(혹은 Taker)라도 id가 다르면 다른 사람

---

* 이후로는 여러 줄에 걸쳐 어떤 사람들이 상호작용하는지 주어짐
* 각 줄은 1:1 상호작용을 하는 사람 두명의 id를 나타냄

```python3
0 1
0 2
2 4
done
```

* 총 3번의 1:1 상호작용
* 첫 번째 상호작용은 0번 사람과 1번 사람이, 두 번째 상호작용은 0번 사람과 2번 사람이, 세 번째 상호작용은 2번 사람과 4번 사람이 함
* 입력은 "done"이라는 sentinel이 주어지기 전까지 계속 받아야 함

---

* 각 상호작용마다 두 명의 사람은 각자 `give`와 `take`라는 두 가지 옵션 중 무엇을 할 지를 결정
* 각 사람이 무엇을 선택했는지에 따라 다음과 같이 score를 얻게 됨
* 모든 사람의 초기 score는 0

사람 A | 사람 B | 결과
--------|--------|-------
give | give | 둘 다 2점씩 얻는다
give | take | A는 1점을 잃고, B는 3점을 얻는다
take | give | A는 3점을 얻고, B는 1점을 잃는다
take | take | 둘 다 점수 변화가 없다

---

```python3
0 1
0 2
2 4
done
```

* Giver는 무조건 `give`라는 선택
* Taker는 무조건 `take`라는 선택

1. 0번 사람(Giver)과 1번 사람(Giver)가 서로 `give`하여 2점씩 얻습니다. (사람 별 점수: 2 2 0 0 0)
2. 0번 사람(Giver)과 2번 사람(Taker)가 각각 `give`, `take`하여 0번 사람은 1점을 잃고, 2번 사람은 3점을 얻습니다. (사람 별 점수: 1 2 3 0 0)
3. 2번 사람(Taker)과 4번 사람(Taker)가 서로 `take`하여 점수 변화가 없습니다. (사람 별 점수: 1 2 3 0 0)

---

* 다음과 같이 각 사람의 id, type, score를 포함해서 출력
* 점수에 따라 내림차순으로 정렬하고, 점수가 같은 사람끼리는 id에 따라 오름차순으로 정렬
* 입력의 두번째 줄은 무시 (3번째 소문제에서 사용됨)

.row[
.col-6[

**Input**
```
GGTGT
0 0 0 0 0
0 1
0 2
2 4
done
```
]
.col-6[
**Output**
```
2: Taker (3pts)
1: Giver (2pts)
0: Giver (1pts)
3: Giver (0pts)
4: Taker (0pts)
```
]
]

---

template: base
layout: true

.mb-3[
## 오늘의 실습

#### subproblem 2
]

---

* Matcher라는 타입이 추가됩니다.

Matcher는 각 사람별로 그 사람이 직전에 한 행동이 무엇인지를 기억하고 있습니다. Matcher는 상호작용을 할 때 처음 보는 사람에게는 `give`하지만, 아는 사람에게는 그 사람이 직전에 한 행동을 그대로 돌려줍니다.

.row[
.col-2[

```python3
MGT
0 0 0
0 1
0 2
0 1
0 2
```
]
.col-10[
1. 0번 사람(Matcher)과 1번 사람(Giver)가 상호작용합니다. 0번은 1번을 처음 보기 때문에 `give`합니다. 모두 `give`를 내고 2점씩 얻습니다. (점수: 2 2 0)
2. 0번 사람(Matcher)과 2번 사람(Taker)가 상호작용합니다. 0번은 2번을 처음 보기 때문에 `give`합니다. 각각 `give`, `take`하여 -1점, 3점을 얻습니다. (점수: 1 2 3)
3. 0번 사람(Matcher)과 1번 사람(Giver)가 상호작용합니다. 0번은 1번이 직전에 `give`했다는 걸 기억하고 있기 때문에 이번에도 `give`합니다. 모두 `give`를 내고 2점씩 얻습니다. (점수: 3 4 3)
4. 0번 사람(Matcher)과 2번 사람(Taker)가 상호작용합니다. 0번은 2번이 직전에 `take`했다는 걸 기억하고 있기 때문에 `take`를 냅니다. 모두 `take`를 내고 점수 변화가 없습니다. (점수: 3 4 3)
]
]

---

* Matcher는 어떤 사람이 **직전에** 한 행동을 그대로 돌려준다는 것을 명심하세요.
    * 어떤 사람들이 matcher에게 `give`도 했다가 `take`도 했다가 한다면, matcher도 똑같이 따라서 그 사람의 직전 행동에 따라 `give`를 주거나 `take`를 주거나 할 것입니다.

.row[
.col-6[
**Input**
```
MGT
0 0 0
0 1
0 2
0 1
0 2
done
```
]
.col-6[
**Output**
```
1: Giver (4pts)
0: Matcher (3pts)
2: Taker (3pts)
```
]
]

---

template: base
layout: true

.mb-3[
## 오늘의 실습

#### subproblem 3
]

---

* 모든 사람이 일정 횟수마다 한 번씩 "실수"를 하여 자신이 하려던 선택과 반대되는 선택을 합니다.
    * 예를 들어, 3번에 한 번씩 실수하는 Giver가 있다면, 이 사람은 give, give, take, give, give, take... 순서대로 행동하게 됩니다. 


* 입력의 2번째 줄에 사람수와 같은 개수의 0 이상의 정수가 주어집니다. 각각의 숫자는 해당하는 사람이 실수하는 빈도수를 나타냅니다.


* 실수하는 빈도수가 0이면 실수하지 않습니다. 실수하는 빈도수가 1이면, 모든 선택을 실수합니다. 빈도수가 2이면, 2번에 한번 꼴로 실수합니다.
    * 실수하는 빈도수가 n(>0)이면, i=1, 2, 3, ...번째 선택을 할 때, `i % n == 0`이면 실수합니다.

---

다음과 같은 경우를 봅시다.

.row[
.col-2[
```python3
MMM
3 2 2
0 1
0 1
0 2
0 1
0 2
0 1
```
]
.col-10[

사람 A | A의 원래 의도 | A의 상호작용 수 | A의 실수 | A의 실제 선택 | 사람 B | B의 원래 의도| B의 상호작용 수 | B의 실수 | B의 실제 선택
-----|-------|-------|-------|-------|-------|-------|-------|----|----
0 | give | 1 | N | give | 1 | give | 1 | N | give
0 | give | 2 | N | give | 1 | give | 2 | Y | take
0 | give | 3 | Y | take | 2 | give | 1 | N | give
0 | take | 4 | N | take | 1 | give | 3 | N | give
0 | give | 5 | N | give | 2 | take | 2 | Y | give
0 | give | 6 | Y | take | 1 | take | 4 | Y | give

]
]

---

.row[
.col-6[
**Input**
```
MMM
3 2 2
0 1
0 1
0 2
0 1
0 2
0 1
done
```

]
.col-6[
**Output**
```
0: Matcher (12pts)
1: Matcher (3pts)
2: Matcher (1pts)
```
]
]