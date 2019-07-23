# 알고리즘 문제 분석
<br><br>

알고리즘 **문제**는 P, NP, NP-Complete, NP-Hard 등으로 구분된다.
(알고리즘이 아니라 문제에 대한 분류이다)

<br>

<div align="center">
  <img src="https://cdncontribute.geeksforgeeks.org/wp-content/uploads/NP-Completeness-1.png" width=700 />
  <h6>출처  Geeks For Geeks</h6>
</div>
<br>

## P와 NP

* `P`와 `NP` 모두 `결정 문제`이다.
  - 결정 문제는 답이 YES 혹은 NO로 반환되는 문제를 말한다.
* `P`는 문제를 해결하는 (Pseudo) Polynomial Time (다항 시간) 안에 실행되는 알고리즘이 있다는 것이 증명된 결정 문제이다.
  - P 문제는 다항식 시간 동안 '**답(해답 알고리즘)을 찾을 수 있는**' 문제
* `NP`는 Non-deterministic Polynomial의 약자로, Polynomial Time (다항 시간) 안에 실행되는 Non-deterministic 알고리즘이 있는 문제이다.
  - NP 문제는 다항식 시간 동안 '**주어진 답(케이스)이 맞는지 확인할 수 있는**' 문제
  - 어떤 케이스를 input으로 해서 YES 혹은 NO를 **다항 시간** 안에 확인할 수 있다면 NP 문제이다.
* `P`⊂`NP` (`P`는 `NP`의 부분집합이다.)
  - `P` 문제는 어떤 certificate가 주어졌을 때 YES 혹은 NO를 다항 시간 안에 확인할 수 있기 때문이다.

<br>

## NP-Hard와 NP-Complete

* `NP-Hard`: 임의의 문제를 다항식 시간 내에 'A' 문제로 환원(reduction 또는 transformation)할 수 있는 경우, 이 'A'문제를 'NP-난해(NP-hard) 문제'라고 부른다.
  - `NP-Hard` 문제는 `NP` 문제보다 어렵거나 같다.
  - 환원: 쉬운 문제에서 어려운 문제로 바꾼다. (쉬운 문제 B를 위해서 어려운 문제 A라는 문제 해결의 바탕이 되는 개념을 사용한다)
  - [예] 곱셈(쉬운 문제)과 덧셈(어려운 문제)
    - 쉬운 문제(곱셈)을 해결하기 위해 어려운 문제(덧셈)으로 환원해서 답을 구한다.
* `NP-Hard`이면서 `NP`이면 `NP-Complete`이다.


<br><br>

## 참고
* `Polynomial Time Algorithm`: n^k형태로 Worst time Complexity가 정의되는 알고리즘 (k는 상수.)
* `Pseudo Polynomial time algorithm`: worst case의 time complexity가 n^k형태(k는 상수, n은 input의 numeric value (개수가 아님))로 표현되는 알고리즘
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
  - https://wkdtjsgur100.github.io/P-NP/
