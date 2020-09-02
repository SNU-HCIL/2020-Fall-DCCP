layout: true
name: base

#### 035.001.007 컴퓨터의 개념 및 실습

---
class: center, middle


# 실습 진행 방식

---

template: base
layout: true

.mb-3[

# 실습 진행 방식

]

---

### 목표

* 월요일에 배운 이론적인 내용을 습득하는 시간
* 조교가 발표하는 시간보다 **학생이 직접 코딩하는 시간**이 훨씬 많아야 함
* **활발한 질문 답변**을 통해 낙오자 없이 완료하는 것이 목표

<br>

### 두 종류의 과제

* **실습과제:** 매 실습시간마다 부여되며 실습시간 전에 완료해야 함
* **정기과제:** 2주 간격으로 etl을 통해 공지되며 명시된 기한 전에 제출

---

### 질문 방법

* 수강생 120명, 조교 4명, 비대면 수업
* 질문 답변을 원활하게 진행하기 위해 질문 방법을 잘 준수해주세요

<!-- <img src="https://user-images.githubusercontent.com/6987894/91629297-b1150380-ea02-11ea-8cc7-0ec9ccabe310.png" width="100%" /> -->

<br>

### 진행 조교와 질문 조교

* **진행 조교**: 해당 주차의 실습을 진행하는 사람
    * 4명의 조교가 매주 번갈아서 이 역할을 맡습니다
* **질문 조교**: 나머지 3명의 조교

* Zoom에서 진행 조교는 .gray[(호스트)], 질문 조교는 .gray[(공동 호스트)]의 권한을 가집니다

---

### 질문하는 방법

* 공개적인 질문
    * Zoom 채팅창에 그냥 올리면 됩니다
* 개인적인 질문
   * .red[**진행 조교**]에게 귓속말로 "질문 신청합니다"라고 보내주세요
   * 질문 조교 중 한 명이 배정되어 소회의실로 초대됩니다
* 주의
    * 진행 조교에게는 질문의 내용을 보내지 마세요
    * 질문이 들어온 순서대로 배정되니 기다려주세요

.mt-4[
### 질문이 가능한 시간
]
.row.pl-4.text-center[
.col-3.bg-secondary.text-light.pt-3[
개념 및 과제 설명
<br>
(개인 질문 불가)
]
.col-9.bg-info.text-light.pt-3[
학생 실습 시간
<br>
(모든 질문 가능)
]
]

---

### 기타 질문 창구

* etl 질의응답 게시판

  <img src="https://user-images.githubusercontent.com/6987894/91930248-54c02580-ed1b-11ea-8e3b-cd2046ddefd4.png" width="250px" />

* 조교 공식 메일: dccp@hcil.snu.ac.kr
    * 문의사항은 **반드시** 이 메일로만 보내야 답변을 받을 수 있습니다

---

### 온라인 채점 사이트

* 과제 채점을 원활하게 하기 위해 온라인 채점 사이트 운영
* 다음 실습시간에 자세히 설명합니다

<img src="https://user-images.githubusercontent.com/6987894/91629467-52e92000-ea04-11ea-814a-30fbed536ba8.png" width="80%" />

---

template: base
layout: true

.mb-3[
# 개발 환경 설정
]

---

### 프로그래밍 환경의 종류

1. 로컬: 각자의 컴퓨터에서 프로그래밍
2. 리모트: 원격 서버에 접속해서 프로그래밍
3. 외부 서비스: 가상 프로그래밍 환경을 제공하는 외부 웹 서비스 사용
    * (참고) [Google Colab](https://colab.research.google.com/notebooks/intro.ipynb#recent=true) / [Repl.it](https://repl.it/@enaard/Python-3)

<br>

### 실습 방침

* 본 실습에서는 **로컬 프로그래밍 환경**을 기준으로 합니다
* 즉, 본인의 컴퓨터에 Python과 코드 에디터를 설치하고 실행합니다

---

template: base
layout: true

.mb-3[
# 개발 환경 설정
]

<h3>
    <div class="d-flex">
        <img class="mr-2" src="https://user-images.githubusercontent.com/6987894/91920627-a14c3680-ed04-11ea-91d0-3ebfe6ac61bb.png" height="38px" />
        <span>VS Code 설치하기</span>
    </div>
    
</h3>

---

* Microsoft에서 만든 코드 에디터로 가볍고 편의 기능이 많음

<img src="https://user-images.githubusercontent.com/6987894/91920591-84176800-ed04-11ea-85ae-9e96d8e1f7b3.png" width="70%" />

---

* 오픈소스 프로젝트 중 가장 기여자가 많은 프로젝트이기도 합니다

<img src="https://user-images.githubusercontent.com/6987894/91920444-06535c80-ed04-11ea-8826-90185b6698ad.png" width="80%" />

---


* https://code.visualstudio.com/ 에서 설치합니다

<img src="https://user-images.githubusercontent.com/6987894/91920951-4b2bc300-ed05-11ea-95ea-4701a120c612.png" width="70%" />

---

* 설치 옵션은 크게 상관 없습니다

  <img src="https://user-images.githubusercontent.com/6987894/91921076-9b0a8a00-ed05-11ea-8fed-06e6836bd334.png" height="400px"/>

---

* VS 코드를 실행하고, 새 파일을 만듭니다

  ![](https://user-images.githubusercontent.com/6987894/91921302-23892a80-ed06-11ea-8046-95025a2b3f45.png)
  
---

* 아래 사진과 같이 입력합니다. 이는 Python 문법에 따라 작성된 프로그램입니다

  ![image](https://user-images.githubusercontent.com/6987894/91921389-60edb800-ed06-11ea-8e89-42972bf601e5.png)
  
---

* Python 프로그램이라는 것을 명시하기 위해 `.py` 확장자를 붙여 원하는 위치에 저장합니다
* 컴개실 전용 폴더(디렉토리)를 하나 만드는 것을 권장합니다

.row[
.col-sm-auto[
<img src="https://user-images.githubusercontent.com/6987894/91921507-a5795380-ed06-11ea-9a71-e5a07bc91bf2.png" height="250px" />
]
.col[
<img src="https://user-images.githubusercontent.com/6987894/91924201-13287e00-ed0d-11ea-9001-c4f25329211d.png" width="100%" />
]
]

---

* VS Code가 확장자로부터 Python 프로그램임을 인식해 문법을 색상으로 강조해줍니다

  ![image](https://user-images.githubusercontent.com/6987894/91922198-50d6d800-ed08-11ea-8f28-9e9f5a9698f0.png)

---

template: base
layout: true

.mb-3[
# 개발 환경 설정
]

<h3>
    <div class="d-flex">
        <img class="mr-2" src="https://user-images.githubusercontent.com/6987894/91921561-be820480-ed06-11ea-858e-e91597375dbf.png" height="38px" />
        <span>Python3 설치하기 (Windows)</span>
    </div>
    
</h3>

---

* https://www.python.org/downloads/ 에 접속합니다
    * Google에 "download python"이라고 검색하면 바로 나옵니다
* 강조되어 있는 3.8.5 버전 다운로드 버튼을 누릅니다

<img src="https://user-images.githubusercontent.com/6987894/91921672-06089080-ed07-11ea-9dc6-ff559089f457.png" width="60%" />

---

* **Add Python 3.8 to PATH 옵션을 꼭 체크**해주세요
   * cmd 등 윈도우 내 여러 환경에서 `python`이라는 이름으로 Python3를 사용할 수 있게 됩니다
* Install Now 버튼을 클릭합니다

  <img src="https://user-images.githubusercontent.com/6987894/91921829-6c8dae80-ed07-11ea-9eb7-ff85e23db146.png" height="320px" />
  
---

* 실행(window + R)창에서 `cmd`를 입력하거나, 윈도우 메뉴에서 `cmd`를 검색해서 명령 프롬프트를 실행합니다

  ![image](https://user-images.githubusercontent.com/6987894/91922591-4701a480-ed09-11ea-8ba1-b439974dec32.png)
  
---

* `python`이라고 입력하고 엔터를 입력

  <img src="https://user-images.githubusercontent.com/6987894/91922684-7a443380-ed09-11ea-9b2c-7a61a5d563f2.png" width="80%" />
  
---

* 이렇게 뜨면 성공적으로 설치된 것입니다

  <img src="https://user-images.githubusercontent.com/6987894/91922727-91832100-ed09-11ea-9423-810d7125cf19.png" width="80%" />

---


template: base
layout: true

.mb-3[
# 개발 환경 설정
]

<h3>
    <div class="d-flex">
        <img class="mr-2" src="https://user-images.githubusercontent.com/6987894/91921561-be820480-ed06-11ea-858e-e91597375dbf.png" height="38px" />
        <span>Python3 설치하기 (macOS)</span>
    </div>
    
</h3>

---

* VS Code를 설치하는 것까지 동일
* Python 공식 홈페이지에서 받아도 되지만...
* 앞으로 mac을 더 잘 활용하기 위해 brew를 이용하겠습니다

---

* 맥 terminal을 실행합니다
    * spotlight search에 *terminal*이라고 검색하면 나옵니다
    
<img src="https://user-images.githubusercontent.com/38465539/91925561-386abb80-ed10-11ea-9962-d9baa3cd486b.jpeg" width="50%"/>

---

#### HomeBrew

* macOS를 위한 패키지 매니저 
* Linux의 apt-get과 거의 똑같은 역할 (언젠가부터 Linux에서도 사용 가능)
* homebrew [공식 홈페이지](https://brew.sh/) 접속 후 
    * 명령어를 복사해서 
    * 맥 terminal 에 붙여넣고 실행!
    
<img src="https://user-images.githubusercontent.com/38465539/91925713-8ed7fa00-ed10-11ea-983d-4cf68d6aec3b.png" width="100%"/>


---

#### HomeBrew

* `brew -v` 명령어로 homebrew가 잘 깔렸는지 확인합니다

  <img src="https://user-images.githubusercontent.com/38465539/91925807-c5157980-ed10-11ea-8d50-43443c4a064b.png" width="80%"/>

* 앞으로 계속 프로그래밍을 한다면 brew를 쓸 일이 많을 겁니다
    
---

#### Python 설치

* `brew install python` 명령어로 python을 설치합니다
* `python3` 명령어를 실행해 잘 설치되었는지 확인

  <img src="https://user-images.githubusercontent.com/38465539/91926523-64873c00-ed12-11ea-930c-7f3d76e9d9b0.png" width="100%"/>

---

template: base
layout: true

.mb-3[
# 개발 환경 설정
]

### VS Code로 Python 프로그램 실행하기

---

* **VS Code를 껐다 켭니다**
* "폴더 열기" 메뉴를 사용해 아까 작성한 코드가 저장된 폴더를 엽니다
* 해당 폴더의 navigation menu가 생기는 것을 확인합니다

.row.mt-4[
.col-6[
  <img src="https://user-images.githubusercontent.com/6987894/91923213-c2178a80-ed0a-11ea-8109-ff0f02ecd4db.png" width="100%" />
]
.col-6[
  <img src="https://user-images.githubusercontent.com/6987894/91923269-e4a9a380-ed0a-11ea-9e61-5bff0cbf4d13.png" width="100%" />
]
]

---

* 새 터미널을 생성합니다

  <img src="https://user-images.githubusercontent.com/6987894/91923928-8087df00-ed0c-11ea-954e-cdfa7cf6b9b1.png" width="100%" />

* 아래에 생긴 터미널에 `python`을 입력해서 아까와 같이 잘 되는지 확인합니다
* VS Code를 껐다 켜지 않았다면 제대로 안될 수 있습니다

  <img src="https://user-images.githubusercontent.com/6987894/91923856-546c5e00-ed0c-11ea-9be4-d72bca657f9e.png" width="95%" />
  
  
---

* `exit()`를 입력해서 Python interactive mode를 빠져나옵니다
* `python [파일명].py`를 입력합니다
* 결과가 정상적으로 출력되는지 확인합니다

  <img src="https://user-images.githubusercontent.com/6987894/91924030-af9e5080-ed0c-11ea-96f9-d982e34cf3c8.png"/>

---

template: base
layout: true

.mb-3[
# 개발 환경 설정
]

### Python 익스텐션 설치하기

---

* 더 많은 편의기능을 이용하기 위해선 python 확장 프로그램을 설치해야 합니다
* 왼쪽의 확장(extension) 탭에서 python을 검색해서 설치합니다

  <img src="https://user-images.githubusercontent.com/6987894/91934178-a2419000-ed25-11ea-80eb-1802e31c74cc.png" height="300px" />

---

* `F1` 혹은 `Ctrl(Cmd)+Shift+P` 키를 눌러 커맨드 창을 띄우고, `Python: select interpreter` 옵션에서 설치된 Python 3.8을 선택합니다.

  <img src="https://user-images.githubusercontent.com/6987894/91934307-05332700-ed26-11ea-9830-30e2ff1ab1ee.png" width="100%" />

<br>

* 오늘은 설치만 하면 됩니다
* 이 확장 프로그램의 활용법이나 다른 편의기능들은 나중에 다시 보겠습니다
