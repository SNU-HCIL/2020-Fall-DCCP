layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #3

---


template: base
layout: true

.mb-3[
# 오늘의 실습
]

---

#### 을 위한 사전지식


* **while loop**
    * 조건식의 결과가 `True` 인 동안 실행문장을 반복함
    * 반복문을 빠져 나오기 위해 `break` 를 사용


.row[

.col-6[

```python
count = 0
while count < 5:
    print ('재미있는 파이썬', count)
    count = count + 1
```
]
.col-6[

```python
count = 0
while True:
    if count >= 5:
        break
    print ('재미있는 파이썬', count)
    count = count + 1
```
]
]

---

#### 을 위한 사전지식


.row[

.col-6[

* **for loop**
    * 리스트나 튜플, 문자열의 첫 번째 요소부터 차례로 변수에 대입되어 실행문장을 반복함
        * `[0, 1, 2, 3, 4]`
        * `"01234"`
        * `range(0, 5)`
        
```python3
class range(stop)
class range(start, stop)
class range(start, stop, step)
```

]
.col-6[

```python3
for count in [0, 1, 2, 3, 4]:
    print ('재미있는 파이썬', count)
```
```python3
for count in '01234':
    print ('재미있는 파이썬', count)
```
```python3
for count in (0, 1, 2, 3, 4):
    print ('재미있는 파이썬', count)
```
```python3
for count in range(0, 5, 1):
    print ('재미있는 파이썬', count)
```
```python
for count in range(5):
    print ('재미있는 파이썬', count)
```
]
]
        
---

#### 을 위한 사전지식

.row[

.col-6[

* **nested loop**
    * 반복문 여러 개 겹쳐있는 구조
    * 인덱스 변수는 index의 첫 글자를 따서 `i`를 자주 사용
        * `i`, `j`, `k`, ...
* 2중 for문 예시
    * 바깥쪽 루프 (`i`) 세로 방향
    * 안쪽 루프 (`j`) 가로 방향
    
]
.col-6[

<img src="https://github.com/lucetre/PythonProjects/blob/master/1.PNG?raw=true" width="100%"/>



]
]

.row[

.col-7[

    
```python3
for i in range(5):
    for j in range(5):
        print('j:', j, sep='', end=' ')
    print('i:', i, '\\n', sep='') 
```
    
]
.col-5[

<img src="https://github.com/lucetre/PythonProjects/blob/master/2.PNG?raw=true" width="120%"/>


]
]
    
   
   

---

#### 을 위한 사전지식



* **nested loop** 예시
    * 계단식으로 별이 하나씩 증가하게 출력하려면 어떻게 해야 할까요?
    * `end=''`를 지정하여 줄바꿈을 하지 않음

.row[

.col-4[
    
```
*
**
***
****
*****
******
*******
********
*********
**********
```
]

.col-8[

```python3
for i in range(10):
    for j in range(10):
        if j <= i:
            print('*', end='')
    print()
```

```python3
for i in range(10):
    for j in range(i+1):
            print('*', end='')
    print()
```

]
]
   
   
---




#### 실습문제 #1. Fibonacci Number

.row[
.col-2[
```
n     F(n)
............
0     0
1     1
2     1
3     2
4     3
5     5
6     8
7     13
8     21
9     34
10    55
```
]
.col-10[

* 피보나치 수 `F(n)` 는 다음과 같은 초기값 및 점화식으로 정의되는 수열입니다. 
    * `F(0) = 0`
    * `F(1) = 1`
    *  `0` 을 포함한 자연수 `n` 에 대해 `F(n+2) = F(n+1) + F(n)`
    
    
* `0` 을 포함한 자연수 `n` 을 입력 받아 피보나치 수 `F(n)`를 출력하는 프로그램을 작성해 봅시다.
    * `n` 의 입력 범위는 `0` 에서 `10,000` 까지의 정수입니다.
    * 수업시간에 다뤘던 반복문 (for 또는 while loop)을 적극적으로 활용해 보세요!
]
]

---

#### 실습문제 #1. Fibonacci Number

입력 방식: 한 줄에 걸쳐 `0` 이상 `10,000` 이하의 정수 `n` 이 주어집니다.<br>
출력 방식: 첫 번째 줄에 `n` 번째 피보나치 수 `F(n)`를 출력합니다.

* **입출력 예시**
.row[
.col-4[
 ##### Input Example #1
 
```python3
1
```
 
 ##### Output Example #1
 
```python3
1
```
]
.col-4[
 ##### Input Example #2
 
```python3
10
```
 
 ##### Output Example #2
 
 ```python3
55
```
]
.col-4[
 ##### Input Example #3
 
 ```python3
100
```
 
 ##### Output Example #3
 
 ```python3
354224848179261915075
```
]
]
 


---

#### 실습문제 #2. Square Roots via Newton’s Method

* `2`의 제곱근은 얼마일까요?
    * `√2 = 1.41421 35623 73095 04880 16887 24209 69807 85696 71875 37694 80731...`
    
    
* 실수의 지수승을 계산하는 연산자 `**`
```Python
print(2 ** 0.5)
```

* 실수의 제곱근을 계산하는 함수 `math.sqrt()`
```python
import math
print(math.sqrt(2))
```

---

#### 실습문제 #2. Square Roots via Newton’s Method

* **Newton-Raphson Method for** <img src="https://latex.codecogs.com/gif.latex?\large&space;x^{2}&space;=&space;a" title="\large x^{2} = a" />
    * 제곱근의 근삿값 계산
    
    
.row[
.col-6[

* **How can we solve?**

1. `근사 초기값 설정` <img src="https://latex.codecogs.com/gif.latex?x_0>0" title="x_0>0" />
2. `자연수 n 에 대한 근사값 업데이트` <img src="https://latex.codecogs.com/gif.latex?x_n" title="x_n" />
<div width="100%" style="text-align:center;margin-bottom:20px">
    <img src="https://latex.codecogs.com/gif.latex?\large&space;x_n=\frac{1}{2}\left&space;(&space;x_{n-1}&space;&plus;&space;\frac{a}{x_{n-1}}&space;\right&space;)" title="\large x_n=\frac{1}{2}\left ( x_{n-1} + \frac{a}{x_n} \right )" />
</div>
3. `수렴 조건 충족 시 중단`
<div width="100%" style="text-align:center">
    <img src="https://latex.codecogs.com/gif.latex?\large&space;-\varepsilon&space;<&space;\frac{{x_n}^{2}-a}{a}&space;<&space;\varepsilon" title="\large -\varepsilon < \frac{{x_n}^{2}-a}{a} < \varepsilon" />
</div>


]
.col-6[
    <img src="https://github.com/lucetre/PythonProjects/blob/master/fig.png?raw=true" width="110%" />
    
]
]

* 양의 실수 `a`, 근사 초기값 `x_0`, 수렴 조건 임계값 `ε` 이 주어졌을 때, <br>`√a` 를 근사하는 프로그램을 작성해 봅시다.

---


#### 실습문제 #2. Square Roots via Newton’s Method

입력 방식: 각 줄에 양의 실수 `a` 와 `x_0` 가 입력되고 `1e-10` 이상의 실수 `ε`가 주어집니다.<br>
출력 방식: 근사 과정 `x_n` (`x_0` 포함)을 한 줄씩 소수점 이하 12자리까지 출력합니다.

* **입출력 예시**

.row[
.col-4[
 ##### Input Example #1
 
```python3
2
1
1e-6
```
 
 ##### Output Example #1
 
```python3
1.000000000000
1.500000000000
1.416666666667
1.414215686275
1.414213562375
```
]
.col-4[
 ##### Input Example #2
 
```python3
0.01
0.1
1
```
 
 ##### Output Example #2
 
 ```python3
0.100000000000
```
]
.col-4[
 ##### Input Example #3
 
```python3
1048576
1000
1e-10
```
 
 ##### Output Example #3
 
 ```python3
1000.000000000000
1024.288000000000
1024.000040488613
1024.000000000001
```
]
]


---


#### 실습문제 #2. Square Roots via Newton’s Method
 
* <img src="https://latex.codecogs.com/gif.latex?\large&space;\lim_{n\rightarrow&space;\infty&space;}x_n&space;=&space;\sqrt{a}" title="\large \lim_{n\rightarrow \infty }x_n = \sqrt{a}" />
* Newton-Rapson method에 대한 자세한 설명은 아래를 참조하시기 바랍니다.
    * https://math.mit.edu/~stevenj/18.335/newton-sqrt.pdf

---

#### 실습문제 #3. Number Diamond
 
* 크기 `n` 의 **숫자 다이아몬드**를 출력해 봅시다. (nested loop를 활용해 보세요!)
* **입출력 예시**
    * 입력 방식: 한 줄에 걸쳐 10 미만의 자연수 `n` 이 주어집니다.
    * 출력 방식: `2n-1` 줄에 걸쳐 숫자 다이아몬드를 출력합니다.


.row[
.col-3[
 ##### Input  #1
 
```python3
1
```
 
 ##### Output #1
 
```python3
1
```
]
.col-3[
 ##### Input #2
 
```python3
2
```
 
 ##### Output #2
 
 ```python3
 1
121
 1
```
]
.col-3[
 ##### Input #3
 
```python3
3
```
 
 ##### Output #3
 
 ```python3
  1
 121
12321
 121
  1
```
]
.col-3[
 ##### Input #4
 
```python3
4
```
 
 ##### Output #4
 
 ```python3
   1
  121
 12321
1234321
 12321
  121
   1
```
]
]
