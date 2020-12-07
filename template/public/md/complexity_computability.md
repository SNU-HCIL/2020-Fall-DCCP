layout: true
name: base

#### 035.001 (007) 컴퓨터의 개념 및 실습

---
class: center, middle


# Complexity and Computability

---

template: base
layout: true

.mb-3[
## Contents
]

---

- 문제풀이의 효율성: Sorting algorithms
- 오래 걸리는 문제: NP problems
- 계산할 수 없는 문제: Halting problem

---

template: base
layout: true

.mb-3[
## 문제풀이의 효율성
]

---

Sorting algorithm의 다양성을 실제로 느껴보기

<a href="https://www.youtube.com/watch?v=kPRA0W1kECg">
    <img src="https://user-images.githubusercontent.com/6987894/101306418-2efd6c00-3888-11eb-92f3-d2f9b35e2bad.png" height="450px"/>
</a>

---

Jupyter Notebook 참조

---

template: base
layout: true

.mb-3[
## 오래 걸리는 문제
]

---

#### Subset Sum

> 주어진 정수 리스트의 부분집합 중 합이 0인 것이 있는가?

* 원소가 n개인 집합의 모든 부분집합의 수 = 2^n
* 따라서, 모든 부분집합을 검사하는 알고리즘은 O(2^n)의 시간복잡도를 가진다.
* 지수시간(exponential time)은 너무 오래 걸린다, 다항시간(polynomial time) 내에 해결할 순 없을까?

---

#### P문제와 NP 문제

* P 문제
    * deterministic Turing machine이 다항시간 내에 풀 수 있는 문제


* NP 문제
    * nondeterministic Turing machine이 다항시간 내에 풀 수 있는 문제
    * (혹은, deterministic Turing machine이 다항시간 내에 주어진 답이 맞다고/틀리다고 검증할 수 있는 문제)
    
---

직관적으로 번역하면

* deterministic Turing machine
    * 우리가 지금까지 써온 컴퓨터


* nondeterministic Turing machine
    * if문을 만날 때마다 자기자신을 복제해서 모든 분기를 동시에 실험해볼 수 있는 컴퓨터
    * if문을 만날때마다 복제된 개체가 지수적으로 증가하므로 능력치도 deterministic보다 지수배로 높음

따라서 대충 이렇게 생각할 수 있다

* P 문제
    * 우리가 아는 컴퓨터로 다항시간 내에 풀 수 있는 문제


* NP 문제
    * 우리가 아는 컴퓨터로 지수시간 내에 풀 수 있는 문제
    * subset sum problem도 NP문제임

---

#### P vs. NP

P문제의 집합과 NP문제의 집합은 같을까 다를까?

* P = NP
    * 우리가 아직 방법을 모를 뿐이지, 사실 subset sum problem을 다항시간 내에 푸는 방법이 있지 않을까?


* P != NP
    * 저걸 어떻게 다항시간 내에 풀어? 절대 아닐거야. 근데 그런 방법이 존재하지 않는다는 걸 어떻게 증명하지?


* 둘 중에 하나라도 성공하면 역사에 이름을 남길 수 있다

---

#### NP문제를 대하는 방법

* 역대 수많은 수학 천재들이 아무도 subset sum problem을 다항시간 내에 푸는 방법을 찾지 못했다
    * "아마 그런 방법이 없지 않을까?"
    * "있어도 내 인생과는 무관하지 않을까?"


* NP 문제를 풀려면 지수시간이 필요하다고 생각해도 사실상 무방

---

#### NP-hard

이거 하나만 풀면 "모든" NP 문제를 풀 수 있는 그런 문제가 있다

* 따라서, 적어도 NP보단 어렵기 때문에 "NP-hard"라고 부른다
* 어떻게 문제 하나로 "모든" NP문제를 풀 수 있단 말인가?

자세한 것은 알고리즘 수업 시간에 배우는 것으로 하고...  

NP-hard 문제 중에 *지나치게* 어려운 문제 하나를 소개하겠습니다.

---

template: base
layout: true

.mb-3[
## 계산할 수 없는 문제
]

---

#### Halting Problem

프로그램과 초기 입력값이 주어졌을 때 해당 프로그램을 실행하면 언젠간 멈출지 아니면 영원히 계속될지를 판단하기

* 즉, Python 코드랑 입력파일을 눈으로만 보고 무한루프를 돌지 말지 알아내면 됨

---

#### Halting Problem은 NP-hard다

```python3
def subset_sum(l):
    for r in range(1, len(l)+1):
        for combination in combinations(l, r):
            if sum(combination) == 0:
                return combination
    return None

l = list(map(int, input().split())

if subset_sum(l) is None:
    while True:
        pass
```

* 이런 식으로 치트키를 쓰면 임의의 NP 문제를 다항시간 내에 halting problem으로 환원시킬 수 있다

---

#### Halting Problem의 계산 가능성


* Halting Problem은 헛소리인가?
    * 임의의 주어진 문제(프로그램+초기입력)에 대해 뭘 판단해야 하는지 명확히 정의되어 있다
    * 모든 가능한 문제에 대해 정답이 존재한다 (프로그램은 반드시 멈추거나 멈추지 않는다)
    * 따라서, halting problem은 잘 정의된 문제이다.


* Halting Problem은 풀 수 있는가?
    * **Turing machine은 이 문제를 풀 수 없다.**

---

#### Turing machine은 halting problem을 풀 수 없다.

"Turing machine은"

* Halting problem을 푸는 게 아예 불가능하다고 말할 순 없다
* 다만, turing machine을 사용해서 halting problem을 푸는 건 불가능하다
* 즉, 현존하는 모든 컴퓨터는 turing machine을 풀 수 없다
   

"풀 수 없다"

* 지수시간이든 그 이상의 시간이든, 유한한 시간 내에 가능한 모든 문제에 대해 정확한 답을 내릴 수 없다
* 꽤 많은 경우에 대해 정확한 답을 내릴지도 모른다.
* 하지만 "모든" 가능한 문제에 대해 정확한 답을 내리는 것은 불가능하다.
    
---

#### 왜 풀 수 없는가?

"자기 자신"을 처리할 수 없다

* Halting problem을 풀 수 있다고 주장하는 프로그램이 있다면, 그 프로그램한테 자기 자신에 관한 입력을 줘서 망가뜨릴 수 있다
* "스스로 수염을 깎을 수 없는 사람들의 수염만 깎아주는 이발사가 있다면, 그는 스스로 면도를 할 수 있는가?"

이런 종류의 얘기를 좋아한다면 「괴델, 에셔, 바흐」라는 저서를 추천 (주의: 난독서적임)

---

template: base
layout: true

.mb-3[
## 결론
]

---

Take-Home Message: 컴개실 시간에는 대체로 "어떻게든 동작하게 만드는 것"에 초점을 두었지만, "어떻게 더 빠르게 풀 것인가?", "근본적인 느림을 해결할 수 있는가?", "푸는게 가능한 문제이긴 한가?" 등의 다양한 층위에서 고민할 지점이 많다

* 오늘 다룬 내용은 알고리즘, 오토마타이론 등의 과목에서 더 자세히 배울 수 있음

(참고) 그 밖의 다른 관점들

* 하나의 컴퓨터로만 계산해야 하는가? → 멀티코어 프로그래밍
* 항상 매우 정확한 값이 필요한가? → 근사적 알고리즘
* 모든걸 결정론적으로 계산해야 하는가? → 뉴럴 네트워크
* 회로 설계를 바꾸면 어떨까? → 컴퓨터 구조
* 양자 컴퓨팅?



