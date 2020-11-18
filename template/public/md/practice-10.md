layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #10


---
template: base
layout: true

.mb-3[
## 오늘의 실습
#### 을 위한 배경지식 
]

---


**Comparing Two Algorithms**

* Suppose you are designing a web site to process user data (e.g., financial records).


* Suppose database program A takes f<sub>A</sub>(`n`)=30`n`+8 microseconds to process any `n` records, while program B takes f<sub>B</sub>(`n`)=`n`<sup>2</sup>+1 microseconds to process the `n` records.


* Which program do you choose, knowing you’ll want to support millions of users? 

.center[**A!**]

.center[<img src="https://user-images.githubusercontent.com/39995503/99189767-2d1f1c00-27a6-11eb-8e39-44d2c599341b.png" width=200/>]

---
**Order of Growth**

<img src="https://user-images.githubusercontent.com/39995503/99189254-a6693f80-27a3-11eb-82ad-072f6a984ce5.png" width=400/>

---
**Order of Growth**

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Comparison_computational_complexity.svg/2560px-Comparison_computational_complexity.svg.png" width=400/>

---
**Computer Time Examples**

* Assume time = 1 ns (10<sup>-9</sup> second) per op, problem size = `n` bits, #ops: a function of `n` as shown.

.center[<img src="https://user-images.githubusercontent.com/39995503/99189382-4626cd80-27a4-11eb-8b3a-261c5fe90ce5.png" width=350/>]

---
**Concept of Order of Growth**

<img src="https://user-images.githubusercontent.com/39995503/99189486-bc2b3480-27a4-11eb-9286-cd04ba8ff8f9.png" width=600/>

---
**Big-O Notation: *O(g)* **

* at most order g

<img src="https://user-images.githubusercontent.com/39995503/99189577-23e17f80-27a5-11eb-896d-67541adf882d.png" width=600/>

---
**Examples of "Big-O" Proof **

<img src="https://user-images.githubusercontent.com/39995503/99189620-6dca6580-27a5-11eb-9ca6-69a051d0f8af.png" width=600/>

---
**Order of Growth **

<img src="https://user-images.githubusercontent.com/39995503/99189254-a6693f80-27a3-11eb-82ad-072f6a984ce5.png" width=350/>

<img src="https://user-images.githubusercontent.com/39995503/99190063-cc90de80-27a7-11eb-8a72-507f32c4d2af.png" width=700/>

* You will learn a lot about complexity of algorithms in .red[Data Structure] class, .red[Algorithms] class, and so on….!!!

---
**Recursion**

* method of solving a problem where the solution depends on solutions to smaller instances of the same problem
* 쉽게 말해...
    * **더 작은 부분을 풀어내는 자기 자신을 참조(호출)함으로써 큰 문제를 풀 수 있는 방법**
    * 머릿속에 호출 스택을 그리면서 재귀를 설계해야 한다
* 오늘 실습에서 다룰 내용:
    * 재귀 완전정복!
    * merge sort 구현으로 직접해보기
---
**Recursion**

* 재귀함수 구조를 설계할 때는 다음과 같은 2가지만 생각하면 된다
    1. 이 함수가 풀려는 문제는 무엇인가?
        * 왜 이 함수를 만들었지?
        * 무엇을 반환하고 싶은거지?
    2. 이 함수가 풀려는 문제를 어떻게 쪼개거나 축소할 수 있는가?
        * 언제, 어떻게 재귀함수를 호출해야 하지?
    3. 문제를 더 이상 쪼갤 수 없는 시점은 어디인가?
        * base case가 어디지?
* 요약
    * **함수의 반환값, 문제 축소, 축소 불가능한 시점**


---
**Recursion**

* 예시로 이해하기 - **2의 n제곱을 구하는 함수** `two_exp(n)`

1. 함수 `two_exp(n)`가 풀려는 문제는 무엇인가?
    - 당연히 2의 n제곱을 구하는 것이다
2. 그 문제를 어떻게 쪼개거나 축소할 수 있는가?
    - naive한 접근
        - 2의 (n-1)을 구하는 더 작은 문제를 풀고
        - 거기다 2를 곱하면 어떨까?
3. 문제를 더 이상 쪼갤 수 없는 시점은 어디인가?
    - 2의 1제곱은 2임이 자명하니까, `n`이 1일 때는 더이상 못 쪼개고 2를 반환해줘야 한다

---
**Recursion** 

* 이 내용을 함수로 바꾸면?
```python3
def two_exp(n):
    if n == 1:         # 문제를 더  이상 쪼갤 수 없는 시점에서
        return 2       # base case 값을 반환한다
    return 2 * two_exp(n - 1) # 더 작은 문제 n-1짜리를 풀고 2를 곱해 현재 문제를 푼다
```
    
* 걸리는 시간: `O(n)`
* 다소 효율적이지 못한 재귀 설계

---
**Recursion**

* 예시로 이해하기 - **2의 n제곱을 구하는 함수** `two_exp(n)`

1. 함수 `two_exp(n)`가 풀려는 문제는 무엇인가?
    - 당연히 2의 n제곱을 구하는 것이다
2. 그 문제를 어떻게 쪼개거나 축소할 수 있는가? (달라진 부분)
    - 조금 더 효율적인 접근
        - 2의 [n/2]을 구하는 더 작은 문제를 풀고 (가우스 기호)
        - n이 홀수면 `two_exp([n/2])` 의 제곱에 2를 곱해 반환하고
        - n이 짝수면 `two_exp([n/2])` 을 반환하면 어떨까?
3. 문제를 더 이상 쪼갤 수 없는 시점은 어디인가?
    - 2의 1제곱은 2임이 자명하니까, `n`이 1일 때는 더이상 못 쪼개고 2를 반환해줘야 한다

---


**Recursion** 

* 이 내용을 함수로 바꾸면?
```python3
def two_exp(n):
    if n == 1:         # 문제를 더  이상 쪼갤 수 없는 시점에서
        return 2       # base case 값을 반환한다
    return (two_exp(n // 2) ** 2) * 2 if n % 2 == 1 else two_exp(n // 2) ** 2 
    # 짝수일 경우, 홀수일 경우 분리해서 작은 문제로 쪼개기
```
    
* 걸리는 시간: `O(logn)`
    * n이 각 단계를 지날 때마다 절반씩 줄어들기 때문
* 훨씬 효율적으로 변한 재귀 설계

---

**Sort**

* 왜 sorting이 중요한가?
  * list의 원소들을 특정한 규칙에 따라 나열하는 알고리즘
  * sorting을 위한 다양한 알고리즘이 개발됨 
      * bubble sort, insertion sort, selection sort, mergesort, quicksort...
      * heap sort, bucket sort, counting sort, shell sort, Stalin sort...
  * Computer Science에서 가장 기본이 되는 알고리즘 중 하나
  * Time complexity와 같은 기본 개념을 익히기에 적절
---

**Bubble sort**

* sometimes referred to as sinking sort


1. repeatedly steps through the list, 
2. compares adjacent elements and swaps them if they are in the wrong order. 
3. The pass through the list is repeated until the list is sorted.

<img src="https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif"/>

https://en.wikipedia.org/wiki/Bubble_sort

---

**Merge sort**

* a divide and conquer algorithm that was invented by .green[John von Neumann] in 1945

1. Divide the unsorted list into `n` sublists, each containing one element (a list of one element is considered sorted).
2. Repeatedly merge sublists to produce new .red[sorted] sublists until there is only one sublist remaining. 

.center[<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif"/>]

---

template: base
layout: true

.mb-3[
## 오늘의 실습
]

---

#### Problem 1 - Bubble Sort

* 오름차순 bubble sort를 실습 ppt를 참고해 작성하시면 됩니다
* 코드가 여기저기에 공개되어 있지만, 자신의 힘으로 작성하시길 권장합니다
* Problem 2와 같은 코드를 쓰지 마세요!!
* 첫번째 줄에 sorting해야 할 데이터 수가 들어오고, 그 수만큼 data를 받아 sorting하는 프로그램을 작성하세요
* input / output format은 다음과 같습니다

.row[
.col-6[
**Input Example 1**
```c
5
5
4
3
2
1
```
]
.col-6[
**Output Example 1**
```c
1
2
3
4
5
```
]
]

---

#### Problem 2

.row[
.col-6[
**Input Example 2**
```c
4
10
40
20
30
```
]
.col-6[
**Output Example 2**
```c
10
20
30
40
```
]
]

.row[
.col-6[
**Input Example 3**
```c
6
123
421
23
222
9
5
```
]
.col-6[
**Output Example 3**
```c
5
9
23
123
222
421
```
]
]

---

#### Problem 2 - Merge Sort

* merge sort를 실습 ppt를 참고해 작성하시면 됩니다
* 코드가 여기저기에 공개되어 있지만, 자신의 힘으로 작성하시길 권장합니다
* Problem 1와 같은 코드를 쓰지 마세요!!
* Problem 1과 비교해 더 긴 input이 들어와, 
* bubble sort, insertion sort 또는 selection sort로 통과가 불가능합니다
* 첫번째 줄에 sorting해야 할 데이터 수가 들어오고, 그 수만큼 data를 받아 sorting하는 프로그램을 작성하세요
* input / output format은 Problem 1과 같습니다
* **Tip**
    * 재귀를 잘 활용해 보세요!!
    
---

#### Problem 3 - Fibonacci revisited

* 이전에 우리는 이미 피보나치 수열을 계산하는 코드를 작성했습니다
* 이번에는 `O(logn)` 시간에 피보나치 수열을 계산하는 코드를 작성하셔야 통과할 수 있습니다
* `O(n)` 짜리 코드로는 시간 제한에 걸립니다
* 어떻게 가능할까요??

---

#### Problem 3 - Fibonacci revisited
피보나치 수열의 `i+1`번째, `i`번째 항은 다음과 같이 구할 수 있습니다. 

<img src="https://user-images.githubusercontent.com/38465539/99405001-967e6680-292f-11eb-9c27-8bdfb74b0d33.png" width="200"/>

이는 다음과 같은 행렬 곱으로 확장할 수 있습니다. 어디서 많이 본 듯한 꼴 아닌가요?
<img src="https://user-images.githubusercontent.com/38465539/99405013-9a11ed80-292f-11eb-8127-91b60f4c2166.png" width="700"/>

앞쪽에서 언급했던 `two_exp` 의 두번째 접근법을 활용하면, `i+1`번째 피보나치 수를 `logn`번의 행렬 계산으로 구할 수 있습니다. 
이 접근법을 이용해 `n`을 input으로 받아 `n`번째 피보나치를 수를 구하는 프로그램을 작성하세요.
이전과 같은 `O(n)`짜리 방법을 이용한다면, 시간 제한에 걸려 통과할 수 없습니다.

---

#### Problem 3 - Fibonacci revisited

**참고자료**

* [행렬의 곱셈](https://j1w2k3.tistory.com/575)
