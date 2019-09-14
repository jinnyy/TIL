#### (스스로를 위한 간단한) 코드 작성 팁
latest_update = 19-09-15

<br>

> #### 참고
> * 각 항목은 java 언어를 기준으로 설명하고 있음
> * 예시도 전부 java 언어를 사용함

<br><br><br>


# 팁
* 자주 쓸 값은 `static final` 변수로 지정
  - 오탈자로 인해 연산 결과가 달라지는 것을 막아준다.
    - 예1
    ```java
    // modular 연산을 자주 해야 하는 경우
    static final int MOD = 1000000;
    ```
    - 예2
    ```java
    // 특정 string 값을 리턴하는 경우
    static final String YES = "yes";
    static final String NO = "no";
    ...
    return value==1 : YES : NO;
    ```
  - 값을 수정할 일이 생겼을 때 편리하다 (수정해야 할 텍스트가 적어지고, 실수할 가능성을 줄여준다.)
    - 예) UP과 DOWN을 서로 바꿔야 할 때 변수명을 사용
    ```java
    static final int UP=0, DOWN=1;
    ...
    val1 += arr[UP];
    val2 += arr[DOWN];
    ```
<br><br><br>




# 자주 하는 실수

### 시간 초과, 메모리 초과
* 매 loop에서 새롭게 변수를 선언했을 때
  - 예)
  ``` java
  for(int i=0; i<N; i++) {
    funcExample(new boolean[N][N]);
  }
  ```

* 같은 작업을 여러 번 수행할 때
  - 예) brute-force 대신 dynamic programming

<br>


### StackOverflowError

* 주로 recursive 함수/메소드를 사용할 때 발생
  - recursion에서 반복문으로 바꿔주면 해결 가능
  - 참고: (설정해놓은 스택의 크기와 각 재귀에서 사용하는 스택의 양에 따라 다르지만), 아주 기본적인 메소드의 경우, java에서 약 10470번 수행 가능했다. ([Ref.1] https://codeday.me/ko/qa/20190415/331927.html)


<br><br><br><br>




## References
* [1][StackOverflowError] https://codeday.me/ko/qa/20190415/331927.html
