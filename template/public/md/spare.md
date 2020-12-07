layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Practice Session #6

---


template: base
layout: true

.mb-3[
# 오늘의 실습
]

---

#### 실습문제 #1.  My Rational Numbers


* **유리수 (有理數)**
    * 두 정수의 비율 또는 분수의 형식으로 나타낼 수 있는 수
    * `q = m/n` : 분자 (numerator) `m` 과 분모 (denomiator) `n`
    * <img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/8e6cec2aa6fba3b8882c147d811f5710823fec8b" title="Q" />
     
    
* 정수 `m` 과 `n` 주어졌을 때 **기약분수 형태** (irreducible fraction)와 **소수점 형태**로 출력
    * `n = 0` 일 경우 `#DIV/0!` 출력
    * `n = 1` 일 경우 분자만 출력
    * 기약분수: 더 이상 약분되지 않는 분수
        * <img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/915f0894b772e0a9b5841d0360dc6f418f045d8f" title="irreducible" />
        * 최대 공약수 (Greatest Common Divisor, GCD)가 1
        

* **Rational Number Class**를 만들고, Initializer method (`__init__`)와 <br>
String representation method (`__str__`)를 적극적으로 활용해 보세요!
* **Do not use `Fraction` library! Build your own class!**


---

#### 실습문제 #1. My Rational Numbers


* How to find Greatest Common Divisor (GCD)?
    * 소인수 분해?
    * **유클리드 호제법 (Euclidean algorithm)**
        * 자연수 `a`, `b` 에 대해서 `a` 를 `b` 로 나눈 나머지를 `r` 이라 하면, <br>
        `a` 와 `b` 의 최대공약수는 `b` 와 `r` 의 최대공약수와 같다.
        * `gcd(a, b) == gcd(b, r)`
            * `gcd(a, b)`: `a` 와 `b` 의 최대공약수
        * Example for `gcd(1071, 1029)`
            * <img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/28a78ff05151f0e27020eab4713cbe6878d8ed65" title="gcd" />
* Reference
    * https://en.wikipedia.org/wiki/Euclidean_algorithm

---

#### 실습문제 #1. My Rational Numbers 


* 입력 방식: 분자와 분모를 가리키는 정수 `m` 과 `n` 이 `/` 로 구분되어 입력됩니다.
* 출력 방식
    * 첫 번째 줄에 기약분수 형태, 두 번째 줄에는 소수점 이하 12자리 형태 출력
    * 단, 분모가 0인 경우 한 줄에 걸쳐 `#DIV/0!` 을 출력합니다.
* **입출력 예시**
.row[
.col-4[
 ##### Input Example #1
 
```python3
1/2
```
 
 ##### Output Example #1
 
```python3
1/2
0.500000000000
```
]
.col-4[
 ##### Input Example #2
 
```python3
-186/1812
```
 
 ##### Output Example #2
 
 ```python3
-31/302
0.102649006622
```
]
.col-4[
 ##### Input Example #3
 
 ```python3
999999/0
```
 
 ##### Output Example #3
 
 ```python3
#DIV/0!
```
]
]
   
---

#### 실습문제 #all.  My Chemical Romance


* **Chemical Elements**: 118개의 화학원소

```txt
H He Li Be B C N O F Ne Na Mg Al Si P S Cl Ar K Ca Sc Ti V Cr Mn Fe Co Ni Cu Zn 
Ga Ge As Se Br Kr Rb Sr Y Zr Nb Mo Tc Ru Rh Pd Ag Cd In Sn Sb Te I Xe Cs Ba La 
Ce Pr Nd Pm Sm Eu Gd Tb Dy Ho Er Tm Yb Lu Hf Ta W Re Os Ir Pt Au Hg Tl Pb Bi Po 
At Rn Fr Ra Ac Th Pa U Np Pu Am Cm Bk Cf Es Fm Md No Lr Rf Db Sg Bh Hs Mt Ds Rg 
Cn Nh Fl Mc Lv Ts Og
```
    
* **Representations of Molecules**
    <img src="https://wps.prenhall.com/wps/media/objects/3313/3393159/imag2503/TB25_001.GIF" title="formula" />

---

#### 실습문제 #all.  My Chemical Romance


.row[
.col-6[

* **Condensed Structural Formula**
    * 분자가 가지고 있는 특징적인 구조를 따로 빼서 쓰는 식 
    
```txt
CH3COOH
CH3(CH2)4CH3
Co(NH3)6Cl3
HOH
```

]
.col-6[
    
* **Molecular Formula**
    * 분자를 구성하는 원자의 종류와 수를 전부 적어주는 식
    
```txt
C2H4O2
C6H14
Cl3CoH18N6
H2O
```

]
]


* **표현식이 주어졌을 때,** <br>
.red[**실습문제 #1**]: 해당 표현식이 올바른 **Condensed Structural Formula** 인지 판단하고 <br>
.red[**실습문제 #2**]: 가능한 경우 **Molecular Formula** 으로 바꾸어 봅시다.
* 화학적으로 말도 안되는 구조지만 형식 규칙 상으로 올바른 표현식이 가능
    * `CaFeBeNe`, `FAlSe`, `BINArY`, `OgOgOOOOOOOgOgOg`

---

#### 실습문제 #1.  My Chemical Romance: Condensed

* Definition for **Condensed Structural Formula**

.row[
.col-6[

**`<num>`**: Natural number from 2 <br>
```txt
2 3 4 5 6 7 8 9 10 11 12 ...
```
**`<single-term>`**: Molecule/Compound single-term unit <br>
```txt
<atom>
<atom><num>
(<multiple-term>)<num>
```
**`<formula>`**: Condensed structural formula <br>
```txt
<single-term>
<multiple-term>
```

]
.col-6[

**`<atom>`**: 118 chemical elements
```txt
H He Li Be B C N O F Ne Na Mg Al Si P S Cl Ar K Ca Sc Ti V Cr Mn Fe Co Ni Cu Zn Ga Ge As Se Br Kr Rb Sr Y Zr Nb Mo Tc Ru Rh Pd Ag Cd In Sn Sb Te I Xe Cs Ba La Ce Pr Nd Pm Sm Eu Gd Tb Dy Ho Er Tm Yb Lu Hf Ta W Re Os Ir Pt Au Hg Tl Pb Bi Po At Rn Fr Ra Ac Th Pa U Np Pu Am Cm Bk Cf Es Fm Md No Lr Rf Db Sg Bh Hs Mt Ds Rg Cn Nh Fl Mc Lv Ts Og
```
**`<multiple-term>`**: Compound multiple-term unit <br>
```txt
<single-term1><single-term2>
<single-term><multiple-term>
```

]
]


---

#### 실습문제 #1.  My Chemical Romance: Condensed

.row[
.col-5[

* **`<single-term>`** examples
    * `<atom>`
    ```txt
    Au
    ```
    * `<atom><num>`
    ```txt
    H2
    ```
    * `(<multiple-term>)<num>`
    ```txt
    (CO3)2
    ```

]
.col-7[

* **`<multiple-term>`** examples
    * `<single-term1><single-term2>`
    ```txt
    H2O
    ```
    * `<single-term><multiple-term>`
    ```txt
    CH3(CH2)4CH3
    ```
* **`<formula>`** example
    * 
    ```txt
    (Co(H2NCH2CH2NH2)3)2(SO4)3
    ```
    
]
]


* **표현식**이 주어졌을 때 올바른 정의의 **Condensed Structural Formula** 인지 판단
    * `True` or `False`
    * Recursive Function, Exception Handling 활용


---

#### 실습문제 #1.  My Chemical Romance: Condensed

* **입력 방식**: 한 줄에 걸쳐 표현식을 나타내는 문자열이 주어집니다. 
    * (특수문자, 공백이 포함될 수 있음)
* **출력 방식**: Condensed Structural Formula 여부를 `True` 또는 `False` 로 출력합니다.

.row[
.col-3[
 ###### **Input Example #1**
 
```python3
CH3(CH2)4CH3
```
 
 ###### **Output Example #1**
 
```python3
True
```
]
.col-3[
 ###### **Input Example #2**
 
```python3
H1F
```
 
 ###### **Output Example #2**
 
 ```python3
False
```
]
.col-3[
 ###### **Input Example #3**
 
 ```python3
Au
```
 
 ###### **Output Example #3**
 
 ```python3
True
```
]
.col-3[
 ###### **Input Example #4**
 
 ```python3
HUH
```
 
 ###### **Output Example #4**
 
 ```python3
True
```
]
.col-3[
 ###### **Input Example #5**
 
 ```python3
CaFeBeNe
```
 
 ###### **Output Example #5**
 
 ```python3
True
```
]
.col-3[
 ###### **Input Example #6**
 
 ```python3
K4(Fe(CN)6)
```
 
 ###### **Output Example #6**
 
 ```python3
False
```
]
.col-3[
 ###### **Input Example #7**
 
 ```python3
H2 O
```
 
 ###### **Output Example #7**
 
 ```python3
False
```
]
.col-3[
 ###### **Input Example #8**
 
 ```python3
O123456789
```
 
 ###### **Output Example #8**
 
 ```python3
True
```
]
]


---

#### 실습문제 #2.  My Chemical Romance: Molecular

* **Condensed Structural Formula**를 **Molecular Formula** 으로 바꾸어 봅시다.
    * 원소 별로 분자를 구성하는 원소의 개수를 dictionary에 저장
    * Hill System 규칙에 따라 원소/개수 순서로 출력 (1은 개수 생략)
* **Hill System**
    * **원소 `C` 가 포함된 화합물**
        * 탄소 `C` 를 쓰고 수소 `H` 를 쓰고 나머지 원자는 알파벳 순서로 씁니다. <br>
        ```txt
        CCl4, CH3I, C2H5Br
        ```
    * **원소 `C` 가 포함되지 않는 화합물**
        * 모든 원자를 알파벳 순서로 씁니다. <br>
        ```txt
        BrI, H2O4S
        ```
    * 예외 무시: ~~ionic compounds, oxides, acids, hydroxides~~
    * https://en.wikipedia.org/wiki/Chemical_formula#Hill_system
    
    
---

#### 실습문제 #2.  My Chemical Romance: Molecular

.row[
.col-6[

* **원소 `C` 가 포함된 화합물**
    * Condensed Structural Formula
    ```txt
    BrCH2COOH
    ```
    * Frequency Dictionary
    ```txt
    H:3, C:2, O:2, Br:1
    ```
    * Molecular Formula
    ```txt
    C2H3BrO2
    ```

]
.col-6[

* **원소 `C` 가 포함되지 않는 화합물**
    * Condensed Structural Formula
    ```txt
    NH3
    ```
    * Frequency Dictionary
    ```txt
    H:3, N:1
    ```
    * Molecular Formula
    ```txt
    H3N
    ```
]
]
    
* 실습문제 #1과 Dictionary, Sort 활용

---

#### 실습문제 #2.  My Chemical Romance: Molecular

* **입력 방식**: 한 줄에 걸쳐 Condensed Structural Formula 표현식 문자열이 주어집니다. 
    * 앞선 예제의 `True` 인 표현식
* **출력 방식**
    * Condensed Structural Formula에서 Molecular Formula 형태로 바꾼 <br>
    표현식 문자열을 출력합니다.

.row[
.col-3[
 ###### **Input Example #1**
 
```python3
CH3(CH2)4CH3
```
 
 ###### **Output Example #1**
 
```python3
C6H14
```
]
.col-3[
 ###### **Input Example #2**
 
 ```python3
HOH
```
 
 ###### **Output Example #2**
 
 ```python3
H2O
```
]
.col-5[
 ###### **Input Example #3**
 
 ```python3
(Co(H2NCH2CH2NH2)3)2(SO4)3
```
 
 ###### **Output Example #3**
 
 ```python3
C12H48Co2N12O12S3
```
]
]


