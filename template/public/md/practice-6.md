layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #6

---


template: base
layout: true

.mb-3[
## 오늘의 실습
]

---

#### 을 위한 사전지식

.row[
.col-4[

* **Raising Exceptions** 
]
.col-8[

```python3
raise BaseException('Exception Raised!')
```

]
]

https://docs.python.org/3/library/exceptions.html#bltin-exceptions

.row[
.col-6[
* **Exception Handling** 

.row[
.col-4[

```python3
try:
    코드1
except:
    코드2
else:
    코드3
finally:
    코드4
```
]
.col-8[

```python
divisor = int(input())
try:
    print(1 / divisor)
except:
    print('Wrong Div')
else:
    print('No Error')
finally:
    print('End')
```

]
]

]
.col-6[
<img width='100%' src="https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile28.uf.tistory.com%2Fimage%2F9949F74E5A427C321F44C1" title="exception" />
]
]
    

---

#### 을 위한 사전지식


* **Dictionary**: Key와 Value를 한 쌍으로 갖는 자료형
```python3
{Key1:Value1, Key2:Value2, Key3:Value3, ... }
```
```python3
my_dict = {'name':'pey', 'phone':'0119993323', 'birth': '1118'}
```
    
.row[
.col-6[
* **Dictionary 쌍 추가하기**

```python
my_dict = {}

my_dict['name'] = 'pey'
my_dict['height'] = 111.8
my_dict[999] = [1, '@']

print(my_dict)
```

]
.col-6[
* **Dictionary 쌍 삭제하기**

```python
my_dict = {'name':'pey', 999:[1, '@']}

del my_dict['name']
del my_dict[999]

print(my_dict)
```

]
]
    
---


#### 을 위한 사전지식

    
.row[
.col-6[

* **Finding Keys in Dictionary**

```python
my_dict = {'name':'pey',
           'phone':'0119993323',
           'birth':'1118'}
           
key = input()

if key in my_dict:
    print(key, my_dict[key])
else:
    print('No such key...')
```

]
.col-6[

* **Dictionary Iteration**

```python3
my_dict = {3:'pey', 1:1/3, 2:2, -1:''}

for key in my_dict:
    print(key, my_dict[key])
```

* **Dictionary Sorted Iteration**

```python
my_dict = {3:'pey', 1:1/3, 2:2, -1:''}

for key in sorted(my_dict):
    print(key, my_dict[key])
```

]
]
   
---
class: center, middle
   
---

#### 실습문제 #1.  Hanoi Commander

* **Modified Tower of Hanoi**
    * 자연수 `M` 개의 **Rods** 과 크기가 `1 ~ N` 인 자연수 `N`개의 **Disks**
    * Rule
        * 한 번에 하나의 Disk 만 옮길 수 있습니다.
        * 크기가 큰 Disk이 작은 Disk 위에 있어서는 안됩니다.
    * Example for `N=5`, `M=3`
    <img src="https://cdn.kastatic.org/ka-perseus-images/5b5fb2670c9a185b2666637461e40c805fcc9ea5.png" title="hanoi" />

---

#### 실습문제 #1.  Hanoi Commander

* **Initial Condition**
    * `N` 개의 Disks가 모두 Rod `1` 에 크기 오름차순으로 쌓여져 있습니다.
* **Command Types**
    * `move <rod1> <rod2>`
        * `<rod1>`: Source Rod in range of `1 ~ M`
        * `<rod2>`: Destination Rod in range of `1 ~ M`, not equal to `<rod1>`
        * Source Rod의 가장 위에 올려진 Disk를 Destination Rod로 이동
        * 이동하는 Disk가 자신보다 크기가 작은 Disk 위에 올려지면 안됩니다.
    * `done <rod>`
        * `<rod>`: Target Rod in range of `1 ~ M`
        * Target Rod에 `N` 개의 모든 Disks가 크기 오름차순으로 쌓여 있는지 판단
                
---

#### 실습문제 #1.  Hanoi Commander

* **Terminal Condition**
    * **`Success`**
        * `done` 수행 후 모든 Disks가 오름차순으로 쌓여 있을 경우
    * **`Failure`**
        * 프로그램 수행 중 오류가 났을 경우
            * `N`과 `M` 입력 과정 중 오류가 났을 경우 (Input Error)
            * Command 도중 오류가 났을 경우 <br>
            (Invalid Command / Value / Syntax Error)
            * 기타 오류
        * `done` 수행 후 모든 Disks가 오름차순으로 쌓여 있지 않을 경우
* **Rod/Disk의 개수와 Command 리스트**가 주어졌을 때<br>
`Success or Failure` 및 terminated **Line Number**를 출력합니다.

---

#### 실습문제 #1.  Hanoi Commander

* **입력 방식**
    * 첫 번째 줄에 Disk의 개수 `N`, Rod 개수 `M` 과 이 주어집니다. 
    * 두 번째 줄부터 한 줄씩 Command가 입력됩니다.
* **출력 방식**: `Success or Failure` 및 terminated **Line Number**를 출력합니다.


.row[
.col-3[
 ###### **Input Example #1**
 
```python3
3 3
move 1 2
move 1 3
move 2 3
move 1 3
done 3
```
 
 ###### **Output Example #1**
 
```python3
Failure in Line 5
```
]
.col-3[
 ###### **Input Example #2**
 
```python3
3 4
move 1 2
move 1 3
move 1 4
move 3 4
move 2 4
done 4
```
 
 ###### **Output Example #2**
 
 ```python3
Success in Line 7
```
]
.col-3[
 ###### **Input Example #3**
 
 ```python3
9 1
move 1 1
done 1

```
 
 ###### **Output Example #3**
 
 ```python3
Failure in Line 2
```
]
.col-3[
 ###### **Input Example #4**
 
 ```python3
10 2
done 1
move 1 -1

```
 
 ###### **Output Example #4**
 
 ```python3
Success in Line 2
```
]
]
