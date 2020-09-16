layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #2

---

template: base
layout: true

.mb-3[

# 실습 Q&A 시스템 업데이트

]

---

### Google docs

* 조교의 도움이 필요하거나 약간의 설명이 필요한 경우 *google docs* 설문지를 이용하시면 됩니다
* 여러분의 질문과 breakout room 신청 현황은 화면공유를 통해 모두에게 공유됩니다 
* assign 탭에서 본인에게 조교가 assign되어 있으면 breakout room에 들어가시면 됩니다
    * 본인의 assign 여부를 잘 확인해주시길 바랍니다 
* **zoom 채팅으로 온 질문은 받지 않습니다.** 효율적인 질문관리를 위해서니 양해 부탁드립니다.
    * 비공개 질문이 필요하시면 breakout room을 신청해주시길 바랍니다
---

### 실습 시간 진행

* 앞으로 실습은 `6시`까지만 진행합니다
* 6시까지 실습 문제를 풀지 못하신 분들은 그 다음 주 실습때까지 정답을 제출하셔야 합니다 

### 실습 시간 이후 추가 질문

* eTL에 질의응답 게시판, 혹은
* 조교 메일 <a href='mailto:dccp@hcil.snu.ac.kr'>dccp@hcil.snu.ac.kr</a>로 문의해주시길 바랍니다 

---

template: base
layout: true

.mb-3[

# 개발환경 관련 재공지

]

---

* VS Code를 **강력하게 권장**합니다
    * 앞으로의 실습, 과제, 프로젝트를 하기 위해 개발환경 구축은 필수적입니다
* 자신만의 개발환경이 있다면 사용하셔도 무방합니다
* 그러나 python3 IDLE나 Interactive Keynote 상에서 프로그래밍하는 것은 **매우 권장드리지 않습니다**
* 개발환경 관련 문의가 있으시다면 조교 메일([dccp@hcil.snu.ac.kr](mailto:dccp@hcil.snu.ac.kr))로 연락주시길 바랍니다


---

template: base
layout: true

.mb-3[

# Assignment

]

* 오늘부터 시작해 총 5개의 과제가 나갈 계획입니다
* 학기말에는 개인 프로젝트를 진행합니다
* 과제와 프로젝트를 위해서 꼭 `VS Code`를 설치하고 개발환경을 구축해주세요!!

---

template: base
layout: true

.mb-3[

# Turtle

]


---

* 앞으로 3번의 과제가 turtle이라는 Library를 통해 진행될 예정입니다
* Turtle??
    * 교육 용도로 제작된 Graphic Libaray
    * python에 기본 모듈로 포함 -> 설치할 필요가 없습니다!!
    * 귀여운 거북이를 조종해서 재미있는 그림을 그려볼 수 있습니다
    * 실행하면 자동으로 거북이가 그림을 그려주는 창이 생성됩니다

<img src="https://user-images.githubusercontent.com/38465539/93194407-02ebb680-f783-11ea-9af4-fa349b497f7f.png" width="50%" />

---




.row[
.col-6[

* 예시 1

```python3
'''Turtle을 t라는 이름으로 사용'''
import turtle as t

'''거북이 모양 변경'''
t.shape("turtle")
'''거북이 속도 변경'''
t.speed(5)

t.fd(100) # 앞으로 100만큼 가서
t.left(120) # 왼쪽으로 120도 돌고 
t.fd(100) # 다시 앞으로 100만큼 가기  
t.left(120)
t.fd(100)


```

]
.col-6[

* 실행 결과 (삼각형)

<img src="https://user-images.githubusercontent.com/38465539/93194861-84434900-f783-11ea-94cd-f9d51252a4bd.png" width="90%" />



]
]

---

.row[
.col-6[

* 예시 2

```python3
import turtle as t

t.shape("turtle")

t.fd(100)
t.left(144)
t.fd(100)
t.left(144)
t.fd(100)
t.left(144)
t.fd(100)
t.left(144)
t.fd(100)

t.exitonclick()  #클릭해야 꺼짐

```

]
.col-6[

* 실행 결과 (별)
<img src="https://user-images.githubusercontent.com/38465539/93198116-814a5780-f787-11ea-81b1-8ef81d0ff2e8.png" width="90%"/>


]

]

---

이외에도 다양한 기능이 있습니다

* 방금까지 그린 부분 안쪽을 채우기
* 특정 좌표로 이동하기
* 색깔 바꾸기
* 거북이가 이동하는 동안 그림 그리지 않도록 변경
* 선 굵기 바꾸기 등등...

---

* 다양한 기능(함수) 활용


```python3
def drawTwinkle(rad):  # radius값을 parameter로 받음 
    t.begin_fill()     # 채우기 시작
    t.circle(-rad, 90) # radius를 반지름으로 가지는 원을 90도만큼만 그림 (4분원)
    t.left(210)        # 왼쪽으로 210도 회전
    t.circle(-rad, 90) # 반지름 값이 음수면 시계방향 회전
    t.left(210)
    t.circle(-rad, 90)
    t.end_fill()       # 채우기 끝

t.fillcolor("#f1c805") # 채우기 색깔 설정
t.pencolor("#f49d0b")  # 외곽선 색깔 설정
'''#으로 시작하는 6자리 문자열은 hex color code로, rgb값을 컴퓨터에게 가르쳐줍니다.'''
t.width("4")           # 외곽선 굵기 설정
drawTwinkle(200)       # 함수 호출
```

---

* 결과

<img src="https://user-images.githubusercontent.com/38465539/93199638-90320980-f789-11ea-850d-af397ea561d6.png" width="55%">

---

### 대표적인 Turtle 내장 함수

* `t.fd(dist)` : dist만큼 앞으로 이동
* `t.bk(dist)` : dist만큼 뒤로 이동
* `t.goto(x, y)` : x, y좌표로 이동
* `t.speed(val)` : 속도를 val로 바꿈 (1: 느림, 10: 빠름 0: 초고속)
* `t.pos()` : 거북이의 현재 좌표 반환
* `t.penup()` : 거북이가 잉크가 묻은 꼬리를 들어서 더이상 칠하지 않음
* `t.pendown()` : 꼬리를 내려서 다시 그리기 시작
* `t.setheading(angle)` : 거북이가 angle에 해당하는 방향을 가리킴
* `t.color("colorStr")` : 펜 색깔을 colorStr로 바꿈

---

### 대표적인 Turtle 내장함수

* 색상 채우기
    * `t.fillcolor("colorStr")` : 채워지는 색상 변경
    * `t.begin_fill()` 함수 호출로 채우기 시작
    * `t.end_fill()` 함수 호출로 채우기 종료
    * `begin_fill`, `end_fill` 사이에 그려지는 도형 안에 정해진 색깔을 채운다
    
    
.row[
.col-6[



```python3
t.fillcolor("red")
t.begin_fill()
t.fd(100) 
t.left(120) 
t.fd(100) 
t.left(120)
t.fd(100)
t.end_fill()


```

]
.col-6[

<img src="https://user-images.githubusercontent.com/38465539/93200834-4d713100-f78b-11ea-835d-3a070ee28184.png" width="70%"/>



]
]
 



---

### 대표적인 Turtle 내장함수

### 중요!!

`t.exitonclick()`를 잊지 마세요!!
프로그램에서 이 함수를 호출하지 않을 시 거북이의 움직이 끝나자마자 프로그램이 꺼집니다

---

### Turtle 내장함수

* 공식 문서 참조!!
* [Turtle Documentation](https://docs.python.org/3/library/turtle.html)

* 프로그래밍 꿀팁
    * documentation과 친해지고 착한말만 해주길 바랍니다
    * doc은 답을 알고 있다
    
    
---


template: base
layout: true

.mb-3[
 
# Assignment #0

### Turtle로 라이언 그려보기

]

---

* turtle로 어려운 무언가를 그려보기 전에,
* 일단 귀여운 라이언부터 그려봅시다!!
* 라이언처럼 생기기만 하면 됩니다
* 필수요소
    * 귀
    * 눈
    * 코
    * 눈썹

---

* 예시 동영상

<iframe width="560" height="315" src="https://www.youtube.com/embed/-C5oJpHaReY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


---

* 선택과제 (추가점수)
    * 라이언이 아닌 다른 캐릭터 그려보기
    * 재미있는 캐릭터를 하나 선택해 그려봅시다!!

---

* 선택과제 예시
    * 잇님들~ 제가 찾던 터틀 정보 여기 다있네요~

<iframe width="560" height="315" src="https://www.youtube.com/embed/qdeBwgL1EUg" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


---

* turtle로 어려운 무언가를 그려보기 전에,
* 일단 귀여운 라이언부터 그려봅시다!!
* 라이언처럼 생기기만 하면 됩니다
* **기한: 다음주 수요일 (9/23) 자정**
    * etl로 제출
* 자세한 사항은 과제 pdf 참조

---

template: base
layout: true

.mb-3[
 
# 오늘의 실습

### 을 위한 사전지식

]

---

* bool 자료형
    * 수업시간에 짚고 넘어감
    * `True`, `False` 두 가지 상태를 가질 수 있음
    * 프로그래머는 python 코드에 어떤 상태가 **참**인지 **거짓**인지 물어볼 수 있고
    * python은 `True`, `False`로 대답한다
    * 물어볼 때 쓰는 연산자가 바로 **비교 연산자** (Relational Operator)
        * `<`, `>`, `<=`. `>=`, `==` 
        * 흔히 쓰는 부등식 형태
        
---

* 오늘 실습을 위해 알아야 할 Relational Operator:
    * `==`만 알면 된다
    * `a == b`와 같은 형태로 사용
    * `a`와 `b`가 같으면 `True`, 다르면 `False` 값을 뱉어냄
    * `=`와 구분하기 위해 두개를 붙여 쓴다
        * `=`은 assignment에 사용!!
    
---

* == 예시

```python3
>>> 3 == 2
False
>>> 3 == 3
True
>>> "3" == 3
False
>>> "Hello" == "Hello"
True
>>> 3 == 3.14
False
>>> 3 == int(3.14)
True


```

---

* `if` statement
    * 프로그램의 일부분을 특정한 **condition**이 만족될 때만 실행되도록 함
    
```python3
if condition:
    statement
    statement
```

* 위 코드에서 `condition`이 `True`면 `statement`들이 실행되고, `False`면 실행되지 않는다

```python
a = input()
if a == "hello":
    print("Nice to meet you!!")
```

---

* `if`, `else` statement

```python3
if condition:
    statement1
else:
    statement2
```

* `condition`이 `True`면 `statement1`, `False`면 `statement2`가 실행된다
* `condition`이 만족하지 않을 때 `else`문이 실행된다고 생각하면 됨 (맞거나 아니거나)

---

* `if`, `else` statement

```python
a = input()
if a == "hello":
    print("Nice to meet you!!")
else:
    print("What??")
```

* 만일 복잡한 condition을 다루고 싶다면???

---

* 중첩된 `if`, `else`문
```python3
a = input()
if a == "hello":
        print("Nice to meet you!!")
else:
        if a == "goodbye":
            print("See you again")
        else:
            print("What??")
```

* 복잡함
* indent가 많아져서 실수할 가능성
* solution??

---

* `if`, `else` statement + `elif`
    * `else if`의 약자
    * `if`문을 통과하지 못한 경우를 대상으로 다시 조건을 검사함 (연달아 사용 가능)
    
```python
a = input()
if a == "hello":
    print("Nice to meet you!!")
elif a == "goodbye":
    print("See you again")
elif a == "blablabla":
    print("??????")
else:
    print("What??")
```

---

template: base
layout: true

.mb-3[
 
# 오늘의 실습

### Problem #1: 계산기

]

---

지난주 실습 문제였던 수학연산 문제를 기억하시나요? 
지난주에는 두 개의 정수를 입력받아서 

* `+` 더하기
* `-` 빼기
* `*` 곱하기
* `/` 나누기
* `//` 몫
* `%` 나머지
* `**` 제곱

계산 결과를 모두 print했습니다. 
이번주에는 두 개의 정수와 연산 종류를 입력받아서 입력받은 계산만 수행하는 간이계산기를 만들어 봅시다

---

우리가 만들 계산기는 더하기, 뺴기, 곱하기, 몫, 나머지 연산을 수행할 수 있습니다.
각각의 연산은 add(`+`), sub(`-`), mul(`*`), quo(`//`), rem(`%`) 라는 문자열에 대응합니다. 
프로그램은 두 개의 정수를 입력받은 후 연산을 나타내는 문자열을 입력받고, 해당하는 연산을 수행해 그 결과를 print합니다. 

예를 들어 input으로 
```
5
4
mul
```
이 들어올 경우 output은 `20`이 됩니다.


* 꿀팁
    * `if`, `elif`, `else` statement를 적극적으로 활용하세요!!
    
   


---

template: base
layout: true

.mb-3[
 
# 오늘의 실습

### Problem #2: 근의 공식

]

---

중학교 때를 추억하며, 이차방정식의 근을 계산해 주는 프로그램을 만들어 봅시다.

프로그램은 input으로 3개의 정수를 입력받습니다. 각 숫자는 이차방정식의 계수가 됩니다.
예를 들어 3, 5, 1을 입력받는다면, 방정식은 다음과 같은 형태를 가지게 됩니다. 

`3x^2 + 5x + 1 = 0`

근의 공식을 활용해서 정답을 output으로 주는 프로그램을 작성하세요.

- **허수가 정답인 경우는 없습니다.** 어떠한 경우에도 `b^2 - 4ac`값은 0 이상입니다. 
- 중근의 경우에는 output이 한개, 그렇지 않은 경우에는 output이 두개입니다.
    - output이 두 개인 경우 큰 수부터 print해 주세요
- **모든 output은 소수 둘째 자리까지 나타내 주세요!!**
- 이미 당신은 제곱근을 계산할 모든 준비를 마쳤습니다. (`a ** 0.5`)

---

template: base
layout: true

.mb-3[
 
# 오늘의 실습

### 주의사항

]

* 프로그램은 온라인 저지 사이트에 나와있는 input/output 예시와 똑같이 동작해야 합니다.
* 점수가 200점이 아니어도 두 문제 모두 통과가 뜨면 됩니다
* 자주 나오는 실수
    * `input()`함수의 괄호 안에 string을 넣는 경우
        * 이 경우 괄호 안의 string도 출력되어서 output이 달라지게 됩니다 
    * 웹사이트의 input example만 수행 가능한 프로그램을 만드는 경우
    * 쉼표나 공백(스페이스)을 빼먹는 경우
        * 오늘 실습과는 상관없지만 언제나 output 형태에 신경써 주세요!!
        * 앞으로의 프로그래밍에 큰 도움이 됩니다
* 제출 후 abort 버튼을 누르지 마세요!! 새로고침만 고고

---
