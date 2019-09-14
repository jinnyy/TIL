# 흔한 실수들 모음
> latest update = 19-09-15

<br><br>

# 시간 초과
* 매 loop에서 새롭게 변수를 선언했을 때
  - 예)
  ``` java
  for(int i=0; i<N; i++) {
    funcExample(new boolean[N][N]);
  }
  ```

* 같은 작업을 여러 번 수행할 때
  - 예) brute-force 대신 dynamic programming

