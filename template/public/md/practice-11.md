layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #11

---


template: base
layout: true

.mb-3[
# 오늘의 실습
]

---

#### 을 위한 사전지식

* **List Comprehension**
    * 리스트를 만드는 간결한 방법
    * https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions
* **Fraction Module**
    * 유리수 산술 지원
    * https://docs.python.org/3/library/fractions.html
* **Decimal Module**
    * 빠르고 정확하게 자리 올림 하는 십진 부동 소수 산술
    * https://docs.python.org/3/library/decimal.html
* 수업 자료
    * [Linear Algebra](http://dccp.hcil.snu.ac.kr:8888/linear_algebra)
    * [Decimal & Fraction](http://dccp.hcil.snu.ac.kr:8888/decimal_fraction)
    
---

#### 실습문제 #1. Matrix Calculator

**입력 방식**: 두 줄에 걸쳐 임의의 크기의 2차원 정수 행렬 `A` 와 `B` 가 입력됩니다. <br>
**출력 방식**: 각각의 줄에 `-A`, `A^T`, `A+B`, `A-B`, `AB` 를 출력하세요. <br> (수행될 수 없는 연산이라면 `Error`를 출력)

* **입출력 예시**

.row[
.col-6[
 ##### Input Example #1
 
```python3
[[1,2,3,4]]
[[1],[2],[3],[4]]
```
 ##### Output Example #1
 
```python3
[[-1,-2,-3,-4]]
[[1],[2],[3],[4]]
Error
Error
[[30]]
```
]
.col-6[
 ##### Input Example #2
 
```python3
[[1,2,3],[4,5,6],[7,8,9]]
[[1,0,0],[0,1,0],[0,0,1]]
```
 ##### Output Example #2
 
 ```python3
[[-1,-2,-3],[-4,-5,-6],[-7,-8,-9]]
[[1,4,7],[2,5,8],[3,6,9]]
[[2,2,3],[4,6,6],[7,8,10]]
[[0,2,3],[4,4,6],[7,8,8]]
[[1,2,3],[4,5,6],[7,8,9]]
```
]
]


---

#### 실습문제 #2. Square Roots via Newton’s Method (Revisit)

* `2`의 제곱근은 얼마일까요?
    * `√2 = 1.41421 35623 73095 04880 16887 24209 69807 85696 71875 37694 80731...`
    
.row[
.col-8[
* **Newton-Raphson Method for** <img src="https://latex.codecogs.com/gif.latex?\large&space;x^{2}&space;=&space;a" title="\large x^{2} = a" />
    1. `근사 초기값 설정` <img src="https://latex.codecogs.com/gif.latex?x_0>0" title="x_0>0" />
    2. `자연수 n 에 대한 근사값 업데이트` <img src="https://latex.codecogs.com/gif.latex?x_n" title="x_n" />
<div width="100%" style="text-align:center;margin-bottom:20px">
    <img src="https://latex.codecogs.com/gif.latex?\large&space;x_n=\frac{1}{2}\left&space;(&space;x_{n-1}&space;&plus;&space;\frac{a}{x_{n-1}}&space;\right&space;)" title="\large x_n=\frac{1}{2}\left ( x_{n-1} + \frac{a}{x_n} \right )" />
</div>
    3. `수렴 조건 충족 시 중단`
<div width="100%" style="text-align:center">
    <img src="https://latex.codecogs.com/gif.latex?\large&space;-\varepsilon&space;<&space;\frac{{x_n}^{2}-a}{a}&space;<&space;\varepsilon" title="\large -\varepsilon < \frac{{x_n}^{2}-a}{a} < \varepsilon" />
</div> <br>
* 양의 정수 `a`, 근사 초기값 `x_0`, 수렴 조건 임계값 `ε` 이 주어졌을 때 `√a` 를 근사

]
.col-4[
 ##### Input Example
 
```python3
2
1
1e-12
```
 ##### Output Example
 
```python3
1.000000000000
1.500000000000
1.416666666667
1.414215686275
1.414213562375
1.414213562373
```
]
]

---

#### 실습문제 #2. Square Roots via Newton’s Method (Revisit)

1. 소수점으로 출력하는 것이 아닌 **분수 형태**로 출력
2. **참값 `√a` 에 대해 근사값의 분모만큼으로 제한했을 때의 분수**를 함께 출력
    * `limit_denominator(max_denominator=???)` Fraction Module 참고
    
    
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/sqrt.jpg?raw=true" width="100%" />
.row[
.col-4[
 ##### Input Example
 
```python3
2
1
1e-12
```
]
.col-8[
 ##### Output Example
 
```python3
1 1
3/2 3/2
17/12 17/12
577/408 577/408
665857/470832 665857/470832
886731088897/627013566048 442729449143/313056995720
```
]
]

---


#### 실습문제 #2. Square Roots via Newton’s Method (Revisit)

입력 방식: 각 줄에 양의 정수 `a` 와 `x_0` 가 입력되고 `1e-10` 이상의 실수 `ε`가 주어집니다. <br>
출력 방식: **분수 형태의 근사값 `x_n`** 과 분모를 제한한 **분수 형태의 참값 `y_n`** 를 출력 <br>(`x_0`와 `y_0` 포함, 분모가 1일 경우 생략)

* **입출력 예시**

.row[
.col-6[
 ##### Input Example #1
 
```python3
10
3
1e-6
```
 
 ##### Output Example #1
 
```python3
3 3
19/6 19/6
721/228 721/228
1039681/328776 1039681/328776
```
]
.col-6[
 ##### Input Example #2
 
```python3
4
1
0.01
```
 
 ##### Output Example #2
 
 ```python3
1 2
5/2 2
41/20 2
3281/1640 2
```
]
]

---

#### 실습문제 #3. Ant Experiment

* 개미 몇 마리가 길이 `1` 인 1차원 테이블 위에 놓여 있습니다.
    * 각각의 개미는 좌표와 운동방향을 가지고 있습니다. 
        * 좌표: `0 ~ 1` 사이 소수점 형태의 실수
        * 운동방향: `+` 또는 `-` (각각 `0` →`1` 방향, `1` →`0` 방향)
    * 동일한 좌표의 개미는 없으며 테이블 양 끝에 위치한 개미도 없습니다.
    * 모든 개미의 속력은 초속 `1` 입니다.
* **개미의 이동 규칙**
.row[
.col-6[
1. 개미가 테이블의 끝에 도달함과 동시에 떨어져 죽습니다.
2. 서로 다른 개미가 이동하다가 만나면 마주친 장소로부터 서로 방향을 바꾸어 이동합니다.
]
.col-6[
<img src="http://1.bp.blogspot.com/-o6cIUbB1mLM/Ug8DuJ_0F-I/AAAAAAAANSg/YZl9yTZ9N88/s1600/ants-puzzle.gif" width="100%" />
]
]

---

#### 실습문제 #3. Ant Experiment

* 가장 먼저 개미가 떨어지는 시간은 언제일까요?
* 가장 나중에 개미가 떨어지는 시간은 언제일까요?

<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant0.png?raw=true" width="100%" />


---

#### 실습문제 #3. Ant Experiment

* 가장 먼저 개미가 떨어지는 시간은 언제일까요?
* 가장 나중에 개미가 떨어지는 시간은 언제일까요?

<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant0.png?raw=true" width="100%" />
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant1.png?raw=true" width="100%" />

---

#### 실습문제 #3. Ant Experiment

* 가장 먼저 개미가 떨어지는 시간은 언제일까요?
* 가장 나중에 개미가 떨어지는 시간은 언제일까요?

<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant0.png?raw=true" width="100%" />
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant1.png?raw=true" width="100%" />
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant2.png?raw=true" width="100%" />

---

#### 실습문제 #3. Ant Experiment

* 가장 먼저 개미가 떨어지는 시간은 언제일까요?
* 가장 나중에 개미가 떨어지는 시간은 언제일까요?

<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant2.png?raw=true" width="100%" />

---

#### 실습문제 #3. Ant Experiment

* 가장 먼저 개미가 떨어지는 시간은 언제일까요? `0.25`
* 가장 나중에 개미가 떨어지는 시간은 언제일까요?

<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant2.png?raw=true" width="100%" />
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant3.png?raw=true" width="100%" />

---

#### 실습문제 #3. Ant Experiment

* 가장 먼저 개미가 떨어지는 시간은 언제일까요? `0.25`
* 가장 나중에 개미가 떨어지는 시간은 언제일까요?

<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant2.png?raw=true" width="100%" />
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant3.png?raw=true" width="100%" />
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant4.png?raw=true" width="100%" />

---

#### 실습문제 #3. Ant Experiment

* 가장 먼저 개미가 떨어지는 시간은 언제일까요? `0.25`
* 가장 나중에 개미가 떨어지는 시간은 언제일까요?

<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant4.png?raw=true" width="100%" />

---

#### 실습문제 #3. Ant Experiment

* 가장 먼저 개미가 떨어지는 시간은 언제일까요? `0.25`
* 가장 나중에 개미가 떨어지는 시간은 언제일까요?

<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant4.png?raw=true" width="100%" />
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant5.png?raw=true" width="100%" />

---

#### 실습문제 #3. Ant Experiment

* 가장 먼저 개미가 떨어지는 시간은 언제일까요? `0.25`
* 가장 나중에 개미가 떨어지는 시간은 언제일까요? `0.90`

<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant4.png?raw=true" width="100%" />
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant5.png?raw=true" width="100%" />
<img src="https://github.com/lucetre/PythonProjects/blob/master/dccp/practice/practice-11/ant6.png?raw=true" width="100%" />

---

#### 실습문제 #3. Ant Experiment

* 입력 방식
    * **개미들의 좌표**: `0 ~ 1` 사이의 소수점 형태의 실수가 띄어쓰기로 구분 
    * **개미들의 이동방향**: '+' 또는 '-'가 띄어쓰기 구분
* 출력 방식
    * 첫 번째 줄에 가장 먼저 개미가 떨어지는 시간을 소수점 20자리까지 출력 
    * 두 번째 줄에 가장 늦게 개미가 떨어지는 시간을 소수점 20자리까지 출력
* **입출력 예시**

.row[
.col-4[
 ##### Input Example #1
 
```python3
0.25 0.5 0.7 0.9
- + - -
```
 ##### Output Example #1
 
```python3
0.90000000000000000000
0.25000000000000000000
```
]
.col-8[
 ##### Input Example #2
 
```python3
0.00001 0.1010000001 0.123 0.1320984 0.89821390
- + - + -
```
 ##### Output Example #2
 
```python3
0.89899999990000000000
0.00001000000000000000
```
]
]