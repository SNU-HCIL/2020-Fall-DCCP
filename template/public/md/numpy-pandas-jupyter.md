layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# NumPy, Pandas, and Jupyter

---

template: base
layout: true

.mb-3[
## Contents
]

---

- NumPy 개요
- Pandas 개요
- Jupyter 개요
- Jupyter를 활용한 NumPy, Pandas 사용 데모

---



template: base
layout: true

.mb-3[
## <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/NumPy_logo_2020.svg/2560px-NumPy_logo_2020.svg.png" width=175>
]

---


- **Num**erical **Py**thon
- Python에서 array, vector, matrix 등의 연산을 편리하게 해주는 library.
- 고성능 multi-dimensional array와 다양한 수치 연산 메소드 제공하여 Matlab, R 과 같이 사용할 수 있도록 함.
- List와 비슷한 자체 데이터 구조 Array를 제공한다.
    - 다양한 메소드( `mean()`, `std()`, `log()`... )를 통해 계산을 편리하게 할 수 있다.
    - 같은 종류의 데이터로만 구성할 수 있다.


- https://numpy.org

---

- 설치
    - `$ pip install numpy`
    - `$ pip3 install numpy`
    
        혹은 conda 사용 시
    - `$ conda install numpy`
    

- import

    ```Python3
    import numpy as np
    ```

---

template: base
layout: true

.mb-3[
## <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/2560px-Pandas_logo.svg.png" width=175>
]


---

- Data analysis and manipulation tool
- NumPy 기반으로 개발된 자료구조
- 1차원 데이터 타입인 Series와, 테이블 형태의 DataFrame 이라는 자료 구조 제공


---

- 설치
    - `$ pip install pandas`
    - `$ pip3 install pandas`
    
        혹은 conda 사용 시
    - `$ conda install pandas`
    

- import

    ```Python3
    import pandas as pd
    ```
    
---

#### Series

- object를 담을 수 있는 1D array

```Python3
>>> import pandas as pd
>>> import numpy as np
>>> s = pd.Series([1, 3, 5, np.nan, 6, 8])
>>> s
0    1.0
1    3.0
2    5.0
3    NaN
4    6.0
5    8.0
dtype: float64
>>> s.values
array([ 1.,  3.,  5., nan,  6.,  8.])
>>> s.index
RangeIndex(start=0, stop=6, step=1)
```


---

#### DataFrame

- Row, Column 으로 이루어진 테이블 형테의 자료 구조
- 각 Column은 다른 형태의 데이터를 담을 수 있음.

```Python3
>>> d = {'col1': [1, 2], 'col2': ['a', 'b']}
>>> df = pd.DataFrame(data=d)
>>> df
   col1  col2
0     1     a
1     2     b
```

---

#### 10 minutes to pandas

<img src="https://user-images.githubusercontent.com/37106672/101300351-a5926d80-3878-11eb-8514-c02da5a32026.png" width='60%'>

- https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html


---

template: base
layout: true

.mb-3[
## <img src="https://jupyter.org/assets/nav_logo.svg" width=175>
]

---

지금까지 배운 Python code 실행법
- script mode
```C
$ python file.py
```
- interactive mode
```C
$ python
>>> print('hello, world!')
hello, world!
```

---


Jupyter는 IPython을 기반으로 만들어졌습니다.

- IPython
    - Interactive Python
    - 하나의 cell 단위로 코드 및 markdown 작성 가능
    - notebook 형태로 실행할 수 있음
        - notebook은 .ipynb 확장자를 가지는 파일로 저장됨
    - shell command 사용 가능


- Markdown Cell
    * 노트 등을 markdown 형식으로 입력할 수 있는 cell
    * Markdown에 대해서는 https://www.markdownguide.org/getting-started/ 참조

- Code cell
    * 코드를 입력할 수 있는 cell
    

- Shift + Return (Enter)로 각 cell 실행 가능

---

#### JupyterLab 설치 및 실행

- 설치
    - `$ pip install jupyterlab`
    - 혹은 `$ conda install -c conda-forge jupyterlab`


- 실행
    - `$ jupyter-lab`
    

- https://jupyter.org/install 참고
    
---
<img src="https://user-images.githubusercontent.com/37106672/101300360-aa572180-3878-11eb-983e-e36d475f6f75.png" width='75%'/>

---

template: base
layout: true

.mb-3[
## <img src="https://colab.research.google.com/img/colab_favicon_256px.png" width=100/>
]


---
#### Google Colab (Colaboratory)

- Google에서 제공하는 온라인 notebook 환경
- Google 계정만 있으면 무료로 사용할 수 있음 (Google Drive 연동 가능)
- https://colab.research.google.com/notebooks/welcome.ipynb
- GPU 환경 설정 할 수 있음

---

template: base
layout: true

.mb-3[
## Demo
]

---
#### 따라해보기
- eTL에 게시된 파일을 다운로드 받습니다.
- 해당 파일이 위치한 폴더에서 `jupyter-lab` (혹은 `jupyter notebook`) 명령을 실행하여 jupyter 실행 환경을 구성합니다.
- Notebook 파일 명시에 따라 하나씩 실행하며 확인해 봅니다.
