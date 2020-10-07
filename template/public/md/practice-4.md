layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #4

---

.mb-3[
# 공지
]

### 과제 1번
* 과제 1번의 기한이 하루 연장되었습니다
* 과제 1번 실행 방법과 파일 입출력에 관해서 오늘 질문하셔도 됩니다

---

template: base
layout: true

.mb-3[
# 과제 1번 관련 설명
]

---

### command line argument

* 프로그램을 실행할 때 유저가 프로그램에 입력을 주는 방법은 `input()` 이외에도 많습니다
* command line argument는 그 중 하나로, 터미널에서 실행할 때 명령어에 입력을 같이 주는 방식입니다.
* `sys` 모듈을 불러온 후 `sys.argv`를 통해 띄어쓰기로 split된 실행 명령을 볼 수 있습니다.

```python
# 터미널에서: python filename.py a b c와 같이 실행
import sys
print(sys.argv)  # ['filename.py', 'a', 'b', 'c']
```

---

### 파일 입출력

* `input()`과 `print()`를 통해 접근하는 터미널 상의 입출력을 standard input/output이라고 합니다.
* 파일로부터 내용을 읽거나 파일에 무언가를 쓰는 것을 file input/output이라고 합니다.
* Python에서는 `open(파일경로, 모드)`를 통해 file pointer를 얻을 수 있습니다.
    * 모드는 파일을 읽고 쓸 수 있는 권한을 지정합니다
        * 'r': 읽기 전용 (default)
        * 'w': 쓰기 전용, open하는 순간 파일이 초기화됨 (내용 지워짐)
        * 'a': 덧붙이기 전용, 파일의 끝에 내용을 추가함
   
---
   
### 파일 입출력
   
* 과제 1번에서는 파일로부터 아래와 같이 데이터를 읽어올 수 있습니다.

```python3
file_pointer = open('./hello.txt')
my_variable = file_pointer.read()
file_pointer.close()
```

* 파일 포인터는 파일의 내부를 가리키는 탐침같은 것으로, "현재 읽고 있는 위치"가 함께 저장되어 있습니다
* `file_pointer.read()`를 하면 탐침이 파일의 맨 끝으로 이동하므로, 다시 `read`하면 아무것도 읽히지 않습니다
* `file_pointer.seek(0)`을 통해 탐침을 맨 처음으로 다시 이동시킬 수 있지만, 과제 1번에서는 추천하지 않습니다.
* 자세한 건 나중에 수업때 배웁니다.

---

template: base
layout: true

.mb-3[
# 오늘의 실습
]

### function
---

* 여러개의 인자를 받고, keyword argument를 사용해 호출할 수 있습니다

```python
def f(x, y, z):
    return x + y + z
    
print(f(5, z=3, y=2))
```

---

* 함수의 각 인자에 default value를 지정할 수 있습니다

```python
def f(x, y=10, z=100):
    return x + y + z
    
print(f(5, z=3))
print(f(5, 3))
```
---

template: base
layout: true

.mb-3[
# 오늘의 실습
]

### string operations

---

* `strip`: 좌우에 오는 특정 문자를 제거함 (기본: 공백문자)
* `lstrip`: 왼쪽에 있는 특정 문자를 제거함 (기본: 공백문자)
* `rstrip`: 오른쪽에 있는 특정 문자를 제거함 (기본: 공백문자)

```python
s = "   hello  "
print('[' + s + ']')
print('[' + s.strip() + ']')
print('[' + s.lstrip() + ']')
print('[' + s.rstrip() + ']')
```

---

* `str.replace(a, b)`: 문자열 내에 등장하는 모든 `'a'`를 `'b'`로 바꿈

```python
s = "   hello  "
print('[' + s.replace(' ', '') + ']')
print('[' + s.replace('l', 'L') + ']')
print('[' + s.replace(' ', '').replace('l', 'L') + ']')
```

---

* replace는 string 자체를 바꾸지 않음

```python
s = "   hello  "
t = s.replace(' ', '')
print('[' + s + ']')
print('[' + t + ']')
```

---

* `str.count(s)`: 개수
* `str.split(s)`: s를 기준으로 쪼갬
* `str.find(s)`: 처음으로 등장하는 위치(index)

```python
s = 'lorem ipsum dolor sit amet'
print(s.count('l'))
print(s.split())
print(s.split('l'))
print(s.find('l'))
```

---

* slicing

```python
s = 'lorem ipsum dolor sit amet'
print(s[0])
print(s[1])
print(s[0:5])
print(s[3:8])
print(s[6:])
print(s[:6])
```

---

* 음수로 indexing할 경우 오른쪽 끝에서부터 접근 가능

```python
s = 'lorem ipsum dolor sit amet'
print(s[-1])
print(s[-2])
print(s[:-1])
print(s[:-2])
```

---

* every 2 characters, every 3 characters
* reverse

```python
s = 'lorem ipsum dolor sit amet'
print(s[2:13])
print(s[2:13:2])
print(s[2:13:3])
print(s[::2])
print(s[::3])
print(s[::2])
print(s[::-1])
```

---

template: base
layout: true

.mb-3[
# 오늘의 실습
]

### list

---

* 스트링과 마찬가지로 slicing 가능

```python
l = ['a', 'b', 'c', 'd', 'e']
print(l[0])
print(l[-1])
print(l[2:4])
```

---

```python
l = ['a', 'b', 'c', 'c', 'd', 'e']
print(l.count('c'))
print(l.index('a'))
print(l.index('b'))
print(l.index('c'))
print(l.index('d'))
```

---

* split으로 쪼개면 list가 됨
* `s.join(list)`를 사용하면 리스트 안의 각 string의 사이사이에 `s`를 끼워넣어서 하나의 스트링으로 합칠 수 있음
    * `list`에는 스트링만 있어야 함

```python
s = 'lorem ipsum dolor sit amet'
a = s.split()
print(a)
print(' '.join(a))
print('---'.join(a))
```

---

* nested list

```python
l = [0, [1, 2], 3]
print(l[0])
print(l[1])
print(l[1][1])
print(l[0][1])  # error
```

---

* 이렇게 하면 l과 t가 동일한 list를 가리키게 됨

```python
l = [1, 2, 3]
t = l
l.append(4)
print(l)
print(t)
```

---

* `[:]`과 같이 slicing하여 clone할 수 있음

```python
l = [1, 2, 3]
t = l[:]
l.append(4)
print(l)
print(t)
```

---

* List comprehension

```python
a = []
for i in range(10):
    a.append(2 * i + 1)
print(a)
 
b = [2 * i + 1 for i in range(10)]
print(b)
```

---

* List comprehension with filtering

```python
a = []
for i in range(10):
    if i % 2 == 0:
        a.append(2 * i + 1)
print(a)
 
b = [2 * i + 1 for i in range(10) if i % 2 == 0]
print(b)
```

---

* 2중 이상의 list comprehension은 직관적이지 않으므로 그냥 for문을 사용하는 게 더 나음

```python
a = [10 * i + j for i in range(5) for j in range(5)]
b = [10 * i + j for j in range(5) for i in range(5)]
print(a)
print(b)

c = []
for i in range(5):
    for j in range(5):
        c.append(10 * i + j)
print(c)
```

---

* `sort`를 사용해 오름차순으로 정렬할 수 있음

```python
a = [5, 3, 2, 4, 1]
a.sort()
print(a)
```
---

* `key` function을 제공하면, 각 원소에 대해 `key`함수를 적용한 결과가 오름차순이 되도록 정렬함

```python
def my_sort_key(x):
    if x % 2 == 0:
        return 0
    else:
        return 1
        
a = [5, 3, 2, 4, 1]
a.sort(key=my_sort_key)
print(a)
```

---

* `lambda`를 사용해서 코드를 압축할 수 있음

```python
a = [5, 3, 2, 4, 1]
a.sort(key=lambda x: x % 2)
print(a)
```

---

* 내림차순 정렬의 예시

```python
a = [5, 3, 2, 4, 1]
a.sort(key=lambda x: -x)
print(a)
```

---

* 튜플이 담긴 리스트를 정렬

```python
a = [(5, 'apple'), (3, 'banana'), (2, 'android'), (4, 'chocolate'), (1, 'cookies')]
a.sort(key=lambda x: x[0])
print(a)
a.sort(key=lambda x: x[1])
print(a)
```

---

template: base
layout: true

.mb-3[
# 오늘의 실습
]

### 실습 문제 1. Sorting Students' GPAs
---

학생들의 수강 내역을 받아서 평점 평균(GPA)가 높은 순서대로 출력해봅시다. 

* 첫 줄에는 학생의 수가 주어집니다
* 두 번째 줄 이후부터 각 학생의 성적 정보가 주어집니다
    * 각 줄의 처음 단어는 학생의 이름입니다
    * 이후로 1개 이상의 성적이 나열되어 있습니다
* 평점 평균이 동일한 경우는 없습니다.

.row[
.col-6[

**입력**

```python3
5
Amy 4.3 3.7 2.0 4.3 1.0
Bob 3.0 0.0 0.0 1.7 3.3
Chris 4.3 4.3 4.3 4.3 4.3 4.3 4.3
Donald 3.3 3.7 1.3 0.7
Eliot 3.3
```

]
.col-6[

**출력**

- 이름과 성적을 띄어쓰기 한 칸으로 구분
- 소수 둘째 자리까지 출력(format 함수)

```python3
Chris 4.30
Eliot 3.30
Amy 3.06
Donald 2.25
Bob 1.60
```

]
]

---

template: base
layout: true

.mb-3[
# 오늘의 실습
]

### 실습 문제 2. Copy & Pasting Spreadsheet

---

엑셀 시트를 복사해서 메모장에 붙여넣기한 결과를 Python으로 처리해봅시다.

<img src="https://user-images.githubusercontent.com/6987894/95291424-79736400-08aa-11eb-9aec-3628848455ed.png" />

* **첫 번째 셀은 이름**을 담고 있습니다.
* **두 번째 셀은 전화번호**를 담고 있습니다.
    * 전화번호는 숫자, 하이픈(-), 공백문자(' ')로 이루어져 있습니다
    * 전화번호는 11개의 숫자를 반드시 포함합니다.
* **세 번째 셀은 메세지**를 담고 있습니다.
    * 4종류의 특수문자(!, ^, @, ~)가 있을 수 있습니다.
* 모든 셀은 좌우 공백문자를 포함할 수 있습니다
---

**입력**

* 입력의 첫 줄에 줄 수가 주어집니다
* 각 줄마다 탭(\t)으로 총 3개의 셀에 대한 정보가 있습니다
* 모든 셀은 좌우 공백문자를 포함할 수 있습니다.

```python3
4
최길웅  	010-1234-5678	꼭 당첨되고 싶습니다 ^^
  박석현	   010 1234 5679	안녕하세요~ 
 전현 	01012345670   	방해할 거야@@@@@@@@@@@@@@@@@
손상준	01012345675	이것은 테스트입니다
```

---

**출력**

* `이름(전화번호): 메세지`의 형식으로 바꾸어 출력합니다
    * 모든 셀에서 좌우 공백문자는 제거하고 시작합니다
    * 전화번호는 000-0000-0000의 형식으로 바꿉니다
    * 메세지에서 모든 특수문자(!, ^, @, ~)는 제거해야 합니다
    * 메세지에 특수문자가 5개 이상 있는 경우 메세지 전체를 `'[차단됨]'`으로 바꿔야 합니다
    * 메세지에 `'테스트'`가 포함되어 있는 경우 해당 줄(row)을 모두 무시합니다

```python3
최길웅(010-1234-5678): 꼭 당첨되고 싶습니다
박석현(010-1234-5679): 안녕하세요
전현(010-1234-5670): [차단됨]
```
