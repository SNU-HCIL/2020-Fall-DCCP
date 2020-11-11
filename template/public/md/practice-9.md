layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #9

---


template: base
layout: true

.mb-3[
## `isinstance()` 보충설명
]

---


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


template: base
layout: true

.mb-3[
## Recursion
]

---

* **Recursive function**: a function that calls itself



```python3
# 1! = 1          (base case)
# n! = n x (n-1)! (recursive case)

def factorial(n):
    if n == 1:    # base case
        return 1
    else:         # recursive case
        return n * factorial(n-1)
```

---

template: base
layout: true

.mb-3[
## 오늘의 실습

#### Problem #1: SuperSum
]

---

아래와 같이 정의되는 SuperSum 함수를 구현해 봅시다.

양의 정수 `k`, `n` 에 대하여

`SuperSum(0, n) = n`

`SuperSum(k, n) = SuperSum(k-1, 1) + SuperSum(k-1, 2) + ... + SuperSum(k-1, n)`

---

숫자 두 개(`k`, `n` | `k`, `n`은 10 이하 자연수)를 입력받아 `SuperSum(k, n)`을 출력합니다.

.row[
.col-6[
**Input Example 1**
```c
1 3
```
]
.col-6[
**Output Example 1**
```c
6
```
]
]

.row[
.col-6[
**Input Example 2**
```c
4 10
```
]
.col-6[
**Output Example 2**
```c
2002
```
]
]

.row[
.col-6[
**Input Example 3**
```c
10 10
```
]
.col-6[
**Output Example 3**
```c
167960
```
]
]
   
---

template: base
layout: true

.mb-3[
## 오늘의 실습

#### Problem #2: Binary Tree Traversal
]

---

### Binary Tree

A **binary tree** is made up of a finite set of nodes that is either **empty** or consists of a node called the **root** together with two binary trees, called the left and right **subtrees**, which are disjoint from each other and from the root.


<img src="http://www.tutorialspoint.com/data_structures_algorithms/images/binary_tree.jpg" width="60%" />


---

### Traversal

Any process for visiting the nodes in some order is called a **traversal**.

Traversal의 종류는 많지만 오늘은 그 중 대표적인 3가지를 구현해봅니다.

* Inorder Traversal
* Preorder Traversal
* Postorder Traversal

---

#### Inorder Traversal

<img src="http://www.tutorialspoint.com/data_structures_algorithms/images/inorder_traversal.jpg" width="30%" />

Inorder Traversal은
* Left subtree를 recursive하게 순회하고
* Root node를 방문한 다음
* Right subtree를 recursive하게 순회합니다.

`D` → `B` → `E` → `A` → `F` → `C` → `G` 순으로 방문합니다.

---

#### Preorder Traversal

<img src="http://www.tutorialspoint.com/data_structures_algorithms/images/preorder_traversal.jpg" width="30%" />

Preorder Traversal은
* Root node를 방문한 다음
* Left subtree를 recursive하게 순회하고
* Right subtree를 recursive하게 순회합니다.

`A` → `B` → `D` → `E` → `C` → `F` → `G` 순으로 방문합니다.

---

#### Postorder Traversal

<img src="http://www.tutorialspoint.com/data_structures_algorithms/images/postorder_traversal.jpg" width="30%" />

Postorder Traversal은
* Left subtree를 recursive하게 순회하고
* Right subtree를 recursive하게 순회한 다음
* Root node를 방문합니다.

`D` → `E` → `B` → `F` → `G` → `C` → `A` 순으로 방문합니다.

---

#### Input

첫번째 줄에는 binary tree의 node 개수 N(N은 자연수)이 주어집니다.

둘째 줄 부터 N개의 줄에 걸쳐 각 node와 left child node, right child node가 주어집니다.

node의 이름은 A부터 차례대로 영문자 대문자로 매겨지며, 항상 A가 root node가 됩니다. child node가 없는 경우 숫자 - 로 표현됩니다.

#### Output

첫째 줄에 Inorder Traversal 결과를,

둘째 줄에 Preorder Traversal 결과를,

셋째 줄에 Postorder Traversal 결과를 출력하면 됩니다.

각 줄에 N개의 알파벳을 공백없이 출력하시면 됩니다.

---
<img src='https://www.acmicpc.net/JudgeOnline/upload/201007/trtr.png' width='25%'/>

.row[
.col-6[
**Input Example**
```c
7
A B C
B D -
C E F
E - -
F - G
D - -
G - -
```
]
.col-6[
**Output Example**
```c
DBAECFG
ABDCEFG
DBEGFCA
```
]
]

---

#### Hint

Left child, Right child와 Node Item 정보를 가지는 node class를 만들어서 사용해보세요!

class 구현은 필수사항은 아닙니다.

---

template: base
layout: true

.mb-3[
## 오늘의 실습

#### Problem #3: Colored Paper
]

---

아래 <그림 1>과 같이 여러개의 정사각형칸들로 이루어진 정사각형 모양의 종이가 주어져 있고, 

각 정사각형들은 하얀색으로 칠해져 있거나 파란색으로 칠해져 있다. 

주어진 종이를 일정한 규칙에 따라 잘라서 다양한 크기를 가진 정사각형 모양의 하얀색 또는 파란색 색종이를 만들려고 한다. 

<img src='https://www.acmicpc.net/upload/images/bwxBxc7ghGOedQfiT3p94KYj1y9aLR.png' width='20%'/>

---

전체 종이의 크기가 `N`×`N`(N=2<sup>k</sup>, k는 자연수) 이라면 종이를 자르는 규칙은 다음과 같다.

.row[
.col-4[
<img src='https://www.acmicpc.net/upload/images/VHJpKWQDv.png' width='100%'/>
]
.col-8[

전체 종이가 모두 같은 색으로 칠해져 있지 않으면 가로와 세로로 중간 부분을 잘라서 <그림 2>의 I, II, III, IV와 같이 똑같은 크기의 네 개의 `N/2` × `N/2`색종이로 나눈다.

나누어진 종이 I ~ IV 각각에 대해서도 앞에서와 마찬가지로 모두 같은 색으로 칠해져 있지 않으면 같은 방법으로 똑같은 크기의 네 개의 색종이로 나눈다. 

이와 같은 과정을 잘라진 종이가 모두 하얀색 또는 모두 파란색으로 칠해져 있거나, 하나의 정사각형 칸이 되어 더 이상 자를 수 없을 때까지 반복한다.
]
]
 

---
.row[
.col-4[
<img src='https://www.acmicpc.net/upload/images/VHJpKWQDv.png' width='100%'/>
]
.col-8[

위와 같은 규칙에 따라 잘랐을 때 <그림 3>은 <그림 1>의 종이를 처음 나눈 후의 상태를,

<그림 4>는 두 번째 나눈 후의 상태를, 

<그림 5>는 최종적으로 만들어진 다양한 크기의 9장의 하얀색 색종이와 7장의 파란색 색종이를 보여주고 있다. 
]
]

---

입력으로 주어진 종이의 한 변의 길이 N과 각 정사각형칸의 색(하얀색 또는 파란색)이 주어질 때 잘라진 하얀색 색종이와 파란색 색종이의 개수를 구하는 프로그램을 작성하세요.

#### Input

첫째 줄에는 전체 종이의 한 변의 길이 N이 주어집니다.

N은 2, 4, 8, 16, 32, 64 중 하나입니다.

색종이의 각 가로줄의 정사각형칸들의 색이 윗줄부터 차례로 둘째 줄부터 마지막 줄까지 주어집니다.

하얀색으로 칠해진 칸은 0, 파란색으로 칠해진 칸은 1로 주어지며, 각 숫자 사이에는 빈칸이 하나씩 있습니다.

#### Output

첫째 줄에는 잘라진 햐얀색 색종이의 개수를 출력하고, 둘째 줄에는 파란색 색종이의 개수를 출력합니다.

---

.row[
.col-6[
**Input Example**
```c
8
1 1 0 0 0 0 1 1
1 1 0 0 0 0 1 1
0 0 0 0 1 1 0 0
0 0 0 0 1 1 0 0
1 0 0 0 1 1 1 1
0 1 0 0 1 1 1 1
0 0 1 1 1 1 1 1
0 0 1 1 1 1 1 1
```
]
.col-6[
**Output Example**
```c
9
7
```
]
]