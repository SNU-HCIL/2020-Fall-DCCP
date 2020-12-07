layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Altair 실습

---


template: base
layout: true

.mb-3[
## Why Visualization
]

---

- 어떤 특정한 데이터를 이해하는 가장 좋은 방법 중 하나
- **시각화**해서 보는 것!!
- 옛날 옛적에는...




---

<img src="https://user-images.githubusercontent.com/38465539/101280765-48fa6880-380e-11eb-864b-c15395add615.png" width=670>

- charging systems on the canal

---

<img src="https://user-images.githubusercontent.com/38465539/101280769-50ba0d00-380e-11eb-874d-5e115544dc1d.png" width=570>

- Nightingale Diagram
- 사망자 / 부상자자의 수를 시간에 따라 나타냄
- 19세기 후반의 이 다이어그램은...



---

<img src="https://user-images.githubusercontent.com/38465539/101280839-ba3a1b80-380e-11eb-987a-2bec3d860172.png" width=470>

- 2020년 코로나19의 심각성을 강조하는 그래프에도 응용
- 무엇이 다를까??

---

.row[
.col-6[
<img src="https://user-images.githubusercontent.com/38465539/101280769-50ba0d00-380e-11eb-874d-5e115544dc1d.png" width=370>
]
.col-6[
<img src="https://user-images.githubusercontent.com/38465539/101280839-ba3a1b80-380e-11eb-987a-2bec3d860172.png" width=400>

]
]


- 무엇이 다를까?
    - 세기? 년도?
    - 색깔?

---

.row[
.col-6[
<img src="https://user-images.githubusercontent.com/38465539/101280769-50ba0d00-380e-11eb-874d-5e115544dc1d.png" width=370>
]
.col-6[
<img src="https://user-images.githubusercontent.com/38465539/101280839-ba3a1b80-380e-11eb-987a-2bec3d860172.png" width=400>

]
]

- 무엇이 다를까?
- 가장 중요한 차이: **표현하고 있는 데이터의 양**
    - 최초의 Nightingale diagram: 월별로 2년
    - 21세기의 Nightingale diagram: 주별로 5년
        - 당연히 일별로도, 심지어 시간별로도 할 수 있을 것

---

.row[
.col-6[
<img src="https://user-images.githubusercontent.com/38465539/101280769-50ba0d00-380e-11eb-874d-5e115544dc1d.png" width=370>
]
.col-6[
<img src="https://user-images.githubusercontent.com/38465539/101280839-ba3a1b80-380e-11eb-987a-2bec3d860172.png" width=400>

]
]

- 컴퓨터의 발전
    - Large-scale 데이터를 다룰 수 있게 됨
    - GPU의 발전 등으로 점점 더 큰 데이터를 다룰 수 있게 됨
- 복잡한 데이터를 쉽게 시각화 가능!!

---

- 왜 데이터를 시각화하는 것이 중요할까?

- Anything interseting??

<img src="https://user-images.githubusercontent.com/38465539/101282893-ef4c6b00-381a-11eb-9622-8224b10aacac.png" width=500>


---


- 왜 데이터를 시각화하는 것이 중요할까?

- 전기음성도와 이온화에너지의 관계가 드러남!!

<img src="https://user-images.githubusercontent.com/38465539/101282998-73065780-381b-11eb-8c01-0b197934f90b.png" width=500>
    

---

- 왜 데이터를 시각화하는 것이 중요할까?
- Outlier => 비활성기체 
- 원자가전자가 0개 (전자껍질이 가득 차있음) 
    - 화학적으로 (아주) 안정하기 때문에 이온화에너지가 상대적으로 높아진다

<img src="https://user-images.githubusercontent.com/38465539/101283003-7c8fbf80-381b-11eb-96ae-93abd1c30a25.png" width=500>


---


<img src="https://user-images.githubusercontent.com/38465539/101283003-7c8fbf80-381b-11eb-96ae-93abd1c30a25.png" width=300>
<img src="https://user-images.githubusercontent.com/38465539/101283278-aeedec80-381c-11eb-8403-efc6d1c340da.png" width=400>


---

- 아무튼 결론
    - 데이터에서 뭔가 insight를 뽑아내기 위해서는...
    - 그런데 그 data가 엄청 크고 복잡할 때는...
    - 그 data를 효과적인 방법으로 보여주는 것이 필요하다!!
- 오늘 배울 것
    - 내가 보고 싶은 data가 있는데...이를 빠르게 효과적으로 탐색하고 싶어
    - python으로 데이터 시각화??

---

template: base
layout: true

.mb-3[
## Altair
]


---


Python에서 데이터 시각화를 할 수 있는 다양한 라이브러리

- Matplotlib
- Seaborn
- **Altair**
    - 오늘 배울 것!!
    
---


<img src="https://user-images.githubusercontent.com/38465539/101283656-2a509d80-381f-11eb-8bef-940429521f95.png" width=300>



Altair를 (이 수업에서) 배우는 이유

1. 앞으로 컴퓨터를 계속 배운다면 Matplot과 seaborn은 수없이 많이 배우게 될 것!!
2. 복잡한 데이터를 간단하게 시각화해줌
    - 그 대신 자유도가 조금 떨어짐
3. 직관적인 사용법
4. 쉽게 interactive chart 구현 가능


---

오늘 할 것: Altair 맛보기!!

- jupyter notebook으로 ㄱㄱㅅ

