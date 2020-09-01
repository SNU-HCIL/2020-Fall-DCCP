layout: true

#### 035.001 컴퓨터의 개념 및 실습

---

class: center, middle

# -1. 인터랙티브 키노트 사용법

---

# 프로그램 구조

<img src="https://user-images.githubusercontent.com/6987894/91038686-24ef8e80-e646-11ea-9c3b-1f9507a22dac.png" height="250px" />

* 직접 개발한 웹 페이지이며 Svelte를 사용했습니다.
* 따로 서버가 없고 Github Pages 등의 서비스를 이용해 호스팅할 예정입니다.
* 교수님께서 강의노트를 마크다운(.md) 파일로 작성해주시면 호스팅은 저희가 알아서 하겠습니다.

---

# 프로그램 구조

* 지금 이 페이지도 인터랙티브 키노트 프로그램으로 작성되어 있습니다.
* <a href="http://147.46.242.161:8011/edit/prac-1.md?token=3d229c9f0bedea9333030aa32b64751767ab12c7e2f60cbf" target="_blank">이 링크</a>에서 마크다운 파일을 확인하실 수 있습니다
* 위 링크는 저희 연구실 GPU 서버에서 돌아가고 있는 <a href="http://147.46.242.161:8011/tree?token=3d229c9f0bedea9333030aa32b64751767ab12c7e2f60cbf" target="_blank">Jupyter Notebook 서버</a>에 있는 파일 중 하나입니다
* 두 링크 모두 저희 연구실 GPU 서버에 직통되는 토큰을 포함하고 있으므로 유출되지 않게 조심해주세요

---

# 앞으로의 작업 방식

.row[
.col-8[

* 교수님께서 <a href="http://147.46.242.161:8011/tree?token=3d229c9f0bedea9333030aa32b64751767ab12c7e2f60cbf" target="_blank">Jupyter Notebook 서버</a>에서 `.md` 확장자 파일을 만드시면 저희가 수합하겠습니다.
* `파일이름.md` 파일을 만들면, `http://147.46.242.161:8010/파일이름`에서 확인하실 수 있습니다.
* 지금 주소가 `http://147.46.242.161:8010/prac-1`이므로 `prac-1.md`의 내용이 보이는 것입니다
* 새로 만들 때는 Text File 메뉴 선택하시면 됩니다.

]
.col-4[

<img src="https://user-images.githubusercontent.com/6987894/91039423-7f3d1f00-e647-11ea-998e-ecdcd7cd0d73.png" height="300px" />

]
]

---

# 앞으로의 작업 방식

* 이후로는 기능을 보여드리기 위한 슬라이드가 이어집니다.
* 이 슬라이드에 작성된 기능 만으로 대부분 작업하실 수 있을 것 같습니다.
* 더 많은 상세 기능들은 현이가 곧 정리해주기로 했으니 완료되면 문서 보내드리겠습니다.

---

# incremental slide

* 대쉬(-)를 3개 쓰면 슬라이드 구분자가 되고

--

* 대쉬(-)를 2개 쓰면 이전까지의 내용과 이어져서 incremental slide를 만들기 좋습니다

--

* 짠

---

# 코드

```python
print(5000 / 3)
print(5000 // 3)  # 몫
print(5000 % 3)  # 나머지
```

* python 코드 블록을 만들면 자동으로 Run 및 Visualize 버튼이 생성됩니다
* Run은 대체로 잘 돌아가는데 몇 가지 이슈가 있어 차차 수정하겠습니다.
    * Syntax highlighting이 안 됩니다
    * 다른 error는 괜찮은데 syntax error를 내면 콘솔이 죽어서 새로고침해야합니다 (고치겠습니다 ㅠㅠ)

---

# 이미지

* 이미지는 따로 어딘가 업로드해서 주소를 불러와야 합니다

![alt text](https://wikidocs.net/images/page/51/REPL.png)

---

# 이미지

<img src="https://wikidocs.net/images/page/51/REPL.png" width="100%" />

* 가로/세로 조절을 하려면 img 태그를 직접 쓰는게 더 좋습니다
* width: 100%

---

# 이미지

<img src="https://wikidocs.net/images/page/51/REPL.png" width="750px" />

* 슬라이드는 자동 스케일링 되어 100% 기준 width=750px, height=500px 정도 됩니다
* width: 750px

---

# 이미지 (height=500px)

<img src="https://wikidocs.net/images/page/88691/leap_year.png" height="500px" />

---

# 이미지


<img src="https://wikidocs.net/images/page/88691/leap_year.png" height="400px" />

* height를 400px(약 80%)로 설정하고
* 남은 약 20%의 공간에 다른 내용을 넣기

---

# 좌우 레이아웃

.row[
.col-6[

```
.row[
.col-6[

왼쪽에 들어갈 내용

]
.col-6[

오른쪽에 들어갈 내용

]
]

```
]
.col-6[

* 왼쪽에 보이는 것과 같이 `.className[\n내용\n]`의 형식으로 class가 있는 div 요소를 만들 수 있습니다
* Bootstrap에서 제공하는 기본 class인 `row`, `col` 등을 사용할 수 있습니다
* 하나의 `row` 안에 `col-숫자`가 여러개 들어가며, 숫자의 합은 12가 되어야 합니다

]
]

---

# 좌우 레이아웃

.row[
.col-6[

```
.row[
    .col-6[

        왼쪽에 들어갈 내용

    ]
    .col-6[

        오른쪽에 들어갈 내용

    ]
]

```
]
.col-6[

* 이렇게 들여쓰기를 하면 markdown parser가 제대로 인식하지 못하니 꼭 아까와 같이 써야 합니다

]
]

---

# 좌우 레이아웃 활용 (예시)


.row[
.col-6[

<img src="https://wikidocs.net/images/page/88691/leap_year.png" width="100%" />

]
.col-6[

예시 답안:

```python
year = int(input('연도 입력: '))
if year % 4 != 0:
    print('평년')
elif year % 100 != 0:
    print('윤년')
elif year % 400 != 0:
    print('평년')
else:
    print('윤년')
```

]
]

---

# 좌우 레이아웃 (예시)

.row[
.col-4[
```python
year = int(input())
if year % 4 != 0:
    print('평년')
```
]
.col-4[
```python
year = int(input())
if year % 4 != 0:
    print('평년')
elif year % 100 != 0:
    print('윤년')
```
]
.col-4[
```python
year = int(input())
if year % 4 != 0:
    print('평년')
elif year % 100 != 0:
    print('윤년')
elif year % 400 != 0:
    print('평년')
else:
    print('윤년')
```
]
]