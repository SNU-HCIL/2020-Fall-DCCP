layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #5

---
template: base
layout: true

.mb-3[
# Announcement
]

---

### Assignment 2

* Assignment 2가 지난주 금요일 출제되었습니다.
* 마감기한(10월 23일 금요일 23:59:59)에 유념하여 주시기 바랍니다.

---

### Office Hour

* 앞으로 **금요일 오후 7-8**시에 Zoom 으로 Office hour가 진행됩니다.
* 해당시간에 자유롭게 참석하셔서 과제, 실습 질문을 하실 수 있습니다.
* Zoom Link는 기존과 동일하게 eTL에 업로드 될 예정입니다.

---

### 질문 방법

1. 질문의 유형을 말머리로 달아주세요 (메일 / 실습 모두)
    * `[과제]`, `[실습]`, `[기타]` 세 가지 중 하나로 달아주시면 되겠습니다.
    * 효율적인 질의응답을 위한 것이고, 말머리가 없으면 답변이 달리지 않을 수 있습니다. 
2. 문제 상황 / 문제와 관련된 코드 블럭 등 .red[**상황 설명**]을 해주세요
    * 설명 없이 코드만 있거나, 오류 메세지만 있는 경우 답변이 달리지 않을 수 있습니다. 
    * 오류 메세지에 대한 설명은 다음과 같으니 참고해 주세요
        * https://dmoj.ca/about/codes/
    * 답변하기 어려운 질문 유형
        * 제 코드는 다음과 같습니다. 문제가 어디 있나요?
        * 온라인 저지에서 ~~error을 냅니다. 문제가 뭔가요?
3. `[실습]` 유형의 경우 원활한 문제 확인을 위해 .red[**본인의 온라인 저지 아이디**]를 적어주세요.


---

### Bonus Problem

* 이번주 실습부터 보너스 문제가 출제됩니다.
* 보너스 문제는 평균적인 실습 문제보다 더 어렵게 출제되며, 학생들의 자발적 심층 학습을 돕기 위한 문제입니다.
* 보너스 문제를 풀면 다른 실습 문제에서 받은 감점을 일부 면제받을 수 있습니다.
* 따라서 평소에 실습을 성실히 수행했다면 보너스 문제를 풀지 않아도 불이익은 없습니다.
* 실습 시간에는 보너스 문제에 대한 질문을 받지 않습니다.


---


template: base
layout: true

.mb-3[
# Debugging
]

---
### `print()`를 이용해보기

* 수업시간에 배운 cloning이 필요한 예제
* `for`문의 index는 그대로이나, L1이 변경되면서 생기는 문제
* 원하는 결과가 나오지 않을때 어떻게 해볼 수 있을까?

```Python
def removeDups(L1, L2):
   """
      Assumes that L1 and L2 are lists.
      Removes any element from L1 that also occurs in L2
   """
   for e1 in L1: # should be `for e1 in L1[:]`
       if e1 in L2:
          L1.remove(e1)
          
L1 = [1, 2, 3, 4]
L2 = [1, 2, 5, 6]
removeDups(L1, L2)
print('L1 = ', L1) # prints L1 = [2, 3, 4]
```

---
### `print()`를 이용해보기

```Python
def removeDups(L1, L2):
   """
      Assumes that L1 and L2 are lists.
      Removes any element from L1 that also occurs in L2
   """
   for e1 in L1:
       if e1 in L2:
          L1.remove(e1)
       print('e1:',e1, 'L1:', L1, 'L2:', L2)
```
* 이처럼 print문을 삽입하여 상태를 출력하게 할 수 있음.
* 매우 빈번하게 사용되는 방법
* 어떤 부분에 오류가 있는지 확인해볼 수 있음.
* 오류를 찾을 수 없다면 중간 중간 `print()`해보기

---
### `print()`를 이용해보기

```python
def removeDups(L1, L2):
   """
      Assumes that L1 and L2 are lists.
      Removes any element from L1 that also occurs in L2
   """
   for e1 in L1:
       if e1 in L2:
          L1.remove(e1)
       print('e1:',e1, 'L1:', L1, 'L2:', L2)
          
L1 = [1, 2, 3, 4]
L2 = [1, 2, 5, 6]
removeDups(L1, L2)
print('L1 = ', L1) # prints L1 = [2, 3, 4]
```

---

### vscode debugger

* vscode에서는 다양한 언어를 debug 할 수 있으며, python 또한 당연히 지원됩니다.
* https://code.visualstudio.com/Docs/editor/debugging
* https://code.visualstudio.com/docs/python/debugging

<img src='https://code.visualstudio.com/assets/docs/editor/debugging/debugging_hero.png' width='40%'/>

---

### vscode debugger

<img src='https://code.visualstudio.com/assets/docs/editor/debugging/debugging_hero.png' width='50%'/>

* Step Over: 한 줄을 실행합니다.
* Step Into: 함수 내부로 들어갑니다.
* Step Out: 함수를 끝까지 실행시킨 다음 호출시킨 곳으로 되돌아 갑니다.

---

### vscode debugger


<img width='50%' alt="Screen Shot 2020-10-14 at 1 54 04 PM" src="https://user-images.githubusercontent.com/37106672/95945713-0a57bb80-0e26-11eb-95e9-a0969bb21224.png">
* 실행하고자 하는 코드를 연 타음 좌측 `Run` 패널을 선택후 `Run and Debug` 버튼을 누릅니다.



---

### vscode debugger


<img width='50%' alt="Screen Shot 2020-10-14 at 1 54 53 PM" src="https://user-images.githubusercontent.com/37106672/95945771-28252080-0e26-11eb-953c-002e681a53a9.png">
* `Debug Configiguration`은 `Python File`을 선택합니다.



---

### vscode debugger



<img width='50%' alt="Screen Shot 2020-10-14 at 1 54 09 PM" src="https://user-images.githubusercontent.com/37106672/95945750-1fcce580-0e26-11eb-8bd2-4eb4d60951b5.png">

* 좌측에는 생성된 variable, call stack 등을 볼 수 있습니다.
* `Exception`이 발생할 경우 위와 같이 발생지점 및 정보를 알 수 있습니다.
---

### vscode debugger
    
<img width='40%' alt="Screen Shot 2020-10-14 at 1 55 45 PM" src="https://user-images.githubusercontent.com/37106672/95945833-49860c80-0e26-11eb-8c8c-b91176fd644b.png">
* breakpoint
    * 코드 실행 중간에 멈춰서 확인해 보고 싶은 지점에 breakpoint를 설정할 수 있습니다.
    * Inline breakpoint를 멈추고 라인 넘버 왼쪽에 빨간 원을 눌러 생성할 수 있습니다.
    * breakpoint 지정 라인 실행 전에 멈추게 됩니다.

---


### vscode debugger - example

<img width='50%' alt="Screen Shot 2020-10-14 at 1 56 51 PM" src="https://user-images.githubusercontent.com/37106672/95945799-3a06c380-0e26-11eb-9a32-fb244f6935fe.png">

* 1 - 8번 줄 전에 멈춘 상태

---

### vscode debugger - example

<img width='50%' alt="Screen Shot 2020-10-14 at 1 56 57 PM" src="https://user-images.githubusercontent.com/37106672/95945806-3e32e100-0e26-11eb-8536-c272a60019b2.png">

* 2 - 8번 줄 실행 후, 9번 줄 앞에서 멈춘 상태. 좌측 variables 섹션에서 L1 변경 확인 가능.

---

### vscode debugger - example

<img width='50%' alt="Screen Shot 2020-10-14 at 1 57 06 PM" src="https://user-images.githubusercontent.com/37106672/95945817-425efe80-0e26-11eb-82a4-199072a043da.png">

* 3 - iteration 후 좌측 variables 섹션에서 L1 변경 확인 가능.



---


template: base
layout: true

.mb-3[
# 오늘의 실습
]

#### #1 - Lo Shu Magic Square
---

* 오늘 구현해 볼 Lo Shu Magic Square는 아래 조건을 만족하는 3 by 3 matrix입니다.
    * **각 row별 수의 합**과
    * **각 column별 수의 합**과
    * **각 diagonal에 위치하는 수의 합**이 모두 일치하는 matrix

---

<img width="50%" alt="Screen Shot 2020-10-13 at 11 16 06 PM" src="https://user-images.githubusercontent.com/37106672/95932992-3e23e880-0e08-11eb-8a19-898a46107a66.png">

* 우측과 같이
    * **각 row별 수의 합**과
    * **각 column별 수의 합**과
    * **각 diagonal에 위치하는 수의 합**이 모두 일치하는 matrix를 **Lo Shu Magic Square**이라고 합니다.

---

* 숫자 9개를 받아서, 해당 matrix가 magic square 인지 판별하는 프로그램을 만듭니다.
* Input: 숫자 9개가 한 줄에 띄어쓰기로 구분되어 입력됩니다.
* Output: `True` or `False`
* Input Example 1
```Python
1 2 3 4 5 6 7 8 9
```
* Output Example 1
```Python
False
```
* Input Example 2
```Python
4 9 2 3 5 7 8 1 6
```
* Output Example 2
```Python
True
```

---

* 숫자 9개는 입력하는 순서대로 3개씩 한 row을 이룹니다.
    
    `4 9 2 3 5 7 8 1 6` 을 입력하면
    ```Python
    4 9 2
    3 5 7
    8 1 6
    ```
    위와 같은 matrix가 구성되어야 합니다.
    
* Hint
    * nested list를 이용하세요
    * 직접 계산하여도 되고, transposed matrix(전치행렬)을 구하여 계산하여도 됩니다.
        * transposed matrix는 `zip(row1, row2, row3)`을 이용하여 만들 수 있습니다.
<!--         * `zip`은 tuple을 가지는 list가 반환되므로, `list(map(list, zip(r1, r2, r3)))` 형식으로 netsted list로 만들 수 있습니다. -->


---

template: base
layout: true

.mb-3[
# 오늘의 실습
]

#### #2 - Encryption and Decryption

---

* 글자를 코드로 치환하여 암호를 만드는 방식을 활용하여 string을 암호화 및 복호화 하는 프로그램을 만들어 봅시다.
* 아래와 같은 코드북이 있다고 가정해봅시다.
    * `H`: `%`
    * `e`: `9`
    * `l`: `@`
    * `o`: `#`
* 암호화는 위처럼 코드북이 구성이 되면, 왼쪽에 해당하는 글자를 오른쪽으로 바꾸는 과정을 거칩니다.
    * `Hello!` → `%9@@#!`
* 복호화는 위처럼 코드북이 구성이 되면, 오른쪽에 해당하는 글자를 왼쪽으로 바꾸는 과정을 거칩니다.
    * `%9@@!` → `Hell!`
* 코드북에 없는 글자는 암호화/복호화 하지 않고 그대로 출력합니다.

---

* Input은 `command`, `original`, `code`, `sentence` 순으로 주어집니다.
    * `command`: `encrypt` or `decrypt`
        * `encrypt`가 들어오면 문장을 암호화하고,`decrpyt`가 들어오면 복호화합니다.
    * `original`: 바뀌기 전 글자 목록이 들어옵니다.
    * `code`: original을 바꿀 글자 목록이 들어옵니다.
    * `sentence`: 암호화/복호화 할 문장이 주어집니다.
* Output은 `sentence`를 `command`에 맞게 암호화/복호화 한 문장을 출력합니다.

---

* Input Example 1
    ```c
    encrypt
    Hdelkmw
    !@#$*-j
    Hello, 2orld! 
    ```
* Output Example 1
    ```c
    !#$$o, jor$@!
    ```
---

* Input Example 2
    ```c
    decrypt
    Apl
    #$%
    # $ $ % e
    ```
* Output Example 2
    ```c
    A p p l e
    ```
---

* Caution
    * 바꿀 문자와 바뀔 문자 각각 대소문자는 구분됩니다.
<br>
* Hint
    * `dict()`와 `zip()`을 활용하세요