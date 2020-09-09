layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #1

---

template: base
layout: true

.mb-3[

# 실습 Q&A 시스템 안내

]

---

### eTL

* 간단한 질문이나 공개적인 질문은 이전처럼 Zoom 내 채팅으로 문의할 수 있습니다.
* 조교의 도움이 필요하거나 비공개 질문은 .red[**eTL 게시글 내 댓글**]로 작성합니다.
    * 질문 내용이나 도움이 필요하다고 하시면 확인 후 순차적으로 도움을 드립니다.
* 오늘 .red[9월 9일 실습 Q&A] 게시글에 질문을 댓글로 달면, 조교가 답변을 답글로 달아드립니다.
* Zoom 채팅으로 질문이 몰릴 경우 처리하기 힘들 수도 있습니다. 이런 경우 eTL을 이용해 주세요.

<br>

### 실습 시간 이후 추가 질문

* eTL에 새로운 게시물로 작성하시거나,
* 조교 메일 <a href='mailto:dccp@hcil.snu.ac.kr'>dccp@hcil.snu.ac.kr</a>로 문의하십시오.

---

template: base
layout: true

.mb-3[

# Shell Commands

]

---
* 사용 예시는 후술합니다.
<br>
<br>
* `ls` (Linux, macOS, Windows Powershell 등) or `dir` (Windows 명령 프롬프트)
    * 파일 및 디렉토리 목록 출력
* `cd {directory}`
    * `{directory}`로 이동
* `mkdir {dirname}`
    * `{dirname}` 디렉토리 생성
* `rmdir {dirname}`
    * `{dirname}` 디렉토리 삭제
* `rm {filename}`
    * `{filename}` 파일 삭제
* `python {filename}` or `python3 {filename}`
    * Python 파일 `{filename}` 실행
    * 경우에 따라 `python`은 python 2가 실행될 수 있으므로 주의
    * `python --version` 혹은 `python3 --version`으로 버전 확인 후 사용
---
* `mv {file1} {file2}`
    * 파일 이동 혹은 이름 변경
* `cp {src} {dest}`
    * 파일 복사
* `man {command}`
    * 특정 명령어에 대한 매뉴얼을 출력
<br>
<br>
* `./`
    * 현재 디렉토리를 나타냄
* `../`
    * 상위 디렉토리를 나타냄
* `~/`
    * 홈 디렉토리를 나타냄
<br>
<br>
* `{}`은 입력하지 마세요!

---
* 일반적으로 shell command임을 나타내기 위해 $을 붙여 나타냅니다.
    * `$ pwd` : 터미널에 `pwd` 한 줄 입력
        * 현재 작업중인 디렉토리를 출력하는 명령어
    * `>>> print('hello, world!')`: python **한 줄** 입력
        * hello, world! 출력하는 코드
<br>
<br>
        
* 명령어와 Python code를 혼동하지 않도록 주의해 주세요.
* `$` 혹은 `>>>`는 사용자가 직접 입력하는 것이 아닙니다.
---
### Example

현재 Desktop 폴더에 있고, Desktop 폴더에 있는 test.py를 새로 만든 DCCP 폴더에 넣고 실행시키고자 합니다.
<br>
* `DCCP` 디렉토리 만들기
    * `mkdir DCCP`
* `test.py`를 `DCCP` 폴더로 이동시키기
    * `mv test.py ./DCCP/test.py`
* `Desktop`에서 바로 `test.py` 실행시키기
    * `python3 ./DCCP/test.py` 혹은
    * `python3 DCCP/test.py`
* `DCCP` 디렉토리로 이동 후 실행시키기
    * `cd DCCP`
    * `python3 test.py`
* 다시 `Desktop`으로 나가기
    * `cd ../`
---

template: base
layout: true

.mb-3[
# Tips
]

---
Python 파일 실행시 Visual Studio Code에서
<br>
`Run Python File in Terminal` 버튼 하나만 누르면 자동으로 명령어를 입력, 실행시켜 준다.

<img width='70%' src="https://user-images.githubusercontent.com/37106672/92508110-05aa5100-f243-11ea-81b0-7943ae5807e7.png">

좌측 하단에 선택된 Interpreter에 맞게 자동으로 실행



---


template: base
layout: true

.mb-3[
# Online Judge 소개
]

---

### Online Judge

* <a href='http://dccp.hcil.snu.ac.kr:2222/'>dccp.hcil.snu.ac.kr:2222</a>
* 위 온라인 채점 사이트에서 실습 과제 및 정기 과제 제출이 이루어집니다.
* ID와 Password는 eTL에 업로드되어 있으며, 로그인 후 Password를 변경해주세요!
<br>
<br>
* `2222` 포트가 Online Judge, `8888` 포트가 Interactive Keynote 입니다.

---

### 과제의 프로세스

1. 온라인 저지 사이트에서 과제 설명을 읽는다.
2. 자신의 로컬 환경에서 코드를 작성한다.
3. 입/출력 예시를 직접 실행해 보면서 코드를 확인한다.
4. 온라인 저지 사이트에 코드를 제출하고 채점결과를 확인한다.
5. 채점 결과 AC(Accepted) 되지 않은 경우 코드를 수정하고 재제출한다.

---

### 튜토리얼

<img width='70%' src="https://user-images.githubusercontent.com/37106672/92504638-e78e2200-f23d-11ea-8ca3-676456c5eb59.png">

---

### 튜토리얼

<img width='70%' src="https://user-images.githubusercontent.com/37106672/92504640-e826b880-f23d-11ea-963a-bea6426973e2.png">

문제 목록을 확인할 수 있습니다.

---

### 튜토리얼

<img width='70%' src="https://user-images.githubusercontent.com/37106672/92504649-e957e580-f23d-11ea-8aaf-a6a9fc7f3748.png">

문제에 대한 설명을 볼 수 있습니다.<br>
.blue[**Submit Solution**] 버튼을 눌러 코드를 제출할 수 있습니다.

---

### 튜토리얼

<img width='70%' src="https://user-images.githubusercontent.com/37106672/92504653-e9f07c00-f23d-11ea-8131-71022a7c547d.png">

작성한 코드를 입력한 후 .blue[Submit] 버튼을 눌러 채점합니다.

---

### 튜토리얼

<img width='70%' src="https://user-images.githubusercontent.com/37106672/92504621-e1984100-f23d-11ea-9b9b-d7645a6a657b.png">

채점 결과를 확인합니다.

---

### 튜토리얼

<img width='70%' src="https://user-images.githubusercontent.com/37106672/92504634-e65cf500-f23d-11ea-818d-eead7222196e.png">

본인의 제출 및 채점 결과를 확인할 수 있습니다.

---

### 튜토리얼

채점 결과는 다음과 같이 나타납니다.

* AC - Accepted
    * 테스트를 성공적으로 통과
* WA - Wrong Answer
    * Output이 테스트 통과 못함
* MLE - Memory Limit Exceeded
    * 프로그램 메모리 한도 초과
* TLE - Time Limit Exceeded
    * 프로그램 실행 시간 초과
* RTE - Runtime Exception
    * Runtime Exception 발생 (Segmentation fault 등)

---

### 튜토리얼

채점 결과는 다음과 같이 나타납니다.

* IR - Invalid Return
    * nonzero exit code (Error)
* OLE - Output Limit Exceeded
    * Output의 길이가 너무 길어 발생
* IE - Internal Error
    * 조교한테 문의

---


template: base
layout: true

.mb-3[
# 오늘의 실습
]

---
### `input()`과 `print()` 사용해보기

* `input()`을 이용해 사용자가 입력 한 값을 받을 수 있습니다.

```Python
>>> var = input()
hello
>>> var
hello
```

* `var = input()`은 input()을 통해 입력 받은 값을 var라는 변수(variable)에 assign 합니다.

---
### `input()`과 `print()` 사용해보기

* `print()`를 통해 문자를 출력할 수 있습니다.

```python
print(1)
print('hello')
```
* `input()`을 통해 입력 받은 값을 `print()`를 통해 출력할 수 있습니다.

```python
name = input('what is your name?')
print(name)
```

---
#### 실습1 설명

수업시간에 보았던  `input()` 과 `print()`를 이용하여 수업에서 사용했던 코드를 직접 작성해 봅시다.

```
My name is Python.
What is your name? (type in your name here and hit 'enter'): {name}
Your name is {name}.
How old are you? (type in your age here and hit 'enter'): {age}
You are {age} years old.
```

 `{}`은 입력할 값입니다. 괄호 자체를 입력하지 않도록 주의해 주세요. 
 
 Visual Studio Code나 다른 에디터를 통해 코드를 작성해보고, Submit Solution 버튼을 누르고 코드를 제출하세요.
 
---
 
  #### Input Example
 
```
gildong
20
```

 
 #### Output Example (코드 직접 실행 시)
 
 ```
My name is Python.
What is your name? (type in your name here and hit 'enter'): gildong
Your name is gildong.
How old are you? (type in your age here and hit 'enter'): 20
You are 20 years old.
 ```
 
 #### Caution

*  **띄어쓰기와 괄호, 온점 등에 유의하세요.**
*  `python filename.py < input.in` 과 같이 I/O Redirection을 이용한 Output은 위 예시와 다를 수 있습니다.
---
#### 실습2 설명

Python에서 Operator(연산자)를 이용해 간단한 수학연산을 해봅시다!

Python에서 수학연산에 사용되는 대표적인 연산자들은 다음과 같습니다.

* `+` 더하기
* `-` 빼기
* `*` 곱하기
* `/` 나누기
* `//` 몫
* `%` 나머지
* `**` 제곱

---

#### Operator Example
```Python
a = 3
b = 5
```
```Python
>>> a + b
8
>>> a - b
-2
>>> a * b
15
>>> a / b
0.6
>>> a // b
0
>>> a % b
3
>>> a ** b
243
```

---
실습 문제는 숫자 2개를 입력 받아 덧셈, 뺄셈, 곱셈, 나눗셈, 몫, 나머지, 제곱을 차례대로 출력하는 것입니다.

 #### Input Example
 
```
24
9
```

 
 #### Output Example
 
 ```
33
15
216
2.6666666666666665
2
6
2641807540224
 ```
---
 #### Caution

*  단순히 `input()`으로 받으면 '24'와 '9'는 string(문자열)이라 `+` operation을 하게 되면 '249'가 됩니다.
*  숫자로 바꿔주기 위해 받은 문자를 `int(input())`으로 받거나 variable을 `var = int(var)`로 type casting 해주세요.
