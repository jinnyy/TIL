> #### 코드 작성(할 때 스스로를 위한 간단한) 팁
> latest_update = 19-09-15

<br><br><br>


# 팁
* 자주 쓸 값은 static final 변수로 지정
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

<br><br><br>



# 자주 하는 실수

* 시간 초과, 메모리 초과
  * 매 loop에서 새롭게 변수를 선언했을 때
    - 예)
    ``` java
    for(int i=0; i<N; i++) {
      funcExample(new boolean[N][N]);
    }
    ```

  * 같은 작업을 여러 번 수행할 때
    - 예) brute-force 대신 dynamic programming

