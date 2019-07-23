# 알고리즘 문제 분석

<br><br>
# Intro

알고리즘 **문제**는 P, NP, NP-Complete, NP-Hard 등으로 구분된다.
(알고리즘이 아니라 문제에 대한 분류이다)

<br>
<div align="center">
  <img src="https://cdncontribute.geeksforgeeks.org/wp-content/uploads/NP-Completeness-1.png" width=700 />
  <h6>출처  Geeks For Geeks</h6>
</div>

* `P`와 `NP` 모두 `결정 문제`이다.
  - 결정 문제는 답이 YES 혹은 NO로 반환되는 문제를 말한다.
* `P`는 문제를 해결하는 Polynomial Time (다항 시간) 안에 실행되는 알고리즘이 있다는 것이 증명된 결정 문제이다.
* `NP`는 Non-deterministic Polynomial의 약자로, Polynomial Time (다항 시간) 안에 실행되는 Non-deterministic 알고리즘이 있는 문제이다.
  - 어떤 케이스를 input으로 해서 YES 혹은 NO를 **다항 시간** 안에 확인할 수 있다면 NP 문제이다.
* `P`⊂`NP` (`P`는 `NP`의 부분집합이다.)
  - `P` 문제는 어떤 certificate가 주어졌을 때 YES 혹은 NO를 다항 시간 안에 확인할 수 있기 때문이다.
* `NP-Hard`이면서 `NP`이면 `NP-Complete`이다.

<br>

#### 참고
* `Polynomial Time Algorithm`: n^k형태로 Worst time Complexity가 정의되는 알고리즘 (k는 상수.)
* `Deterministic Algorithm`: 계산의 각 단계에서 단 한가지의 가능성만을 고려할 수 있는 알고리즘
* `Non-deterministic Algorithm`(비결정적 알고리즘): 문제를 푸는 각 단계에서 여러가지의 가능성을 동시에 고려할 수 있는 알고리즘


<br><br><br>

# References
* (책) "알고리즘 문제 해결 전략", 구종만, 인사이트, 2012
* Geeks For Geeks
  - https://www.geeksforgeeks.org/pseudo-polynomial-in-algorithms/
  - https://www.geeksforgeeks.org/np-completeness-set-1/
* 위키
  - https://namu.wiki/w/P-NP%문제
* 블로그
  - https://zeddios.tistory.com/92
