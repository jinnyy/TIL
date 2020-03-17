# 2. 변수

- 타입을 지정하지 않는다.
- string, integer, real number 등 다양한 타입을 store할 수 있다.
- 변수를 선언한 뒤, 변수를 사용하고자할 때에는 변수 이름 앞에 `$`를 붙인다.
- 변수에 값이 할당되기 전에 사용되면 blank로 취급된다.

``` shell
MY_MESSAGE="Hello World"
echo $MY_MESSAGE
```

<br>


## (1) expr

- `expr`로 숫자 타입 값들을 연산할 수 있다. (string 안 됨)

#### code
``` shell
X = 1
expr $X + 1
```
#### result
``` terminal
2
```

<br>


## (2) read

- `read`로 키보드 input을 받아올 수 있다.
- `read {변수명}` 형식으로 사용한다.
- Python의 input()과 비슷한 기능을 한다.

#### code
``` shell
echo What is your name?
read MY_NAME
echo  "Hello $MY_NAME - hope you're well."
```
#### result
``` terminal
What is your name?
(keyboard input)
Hello (keyboard input) - hope you're well.
```

<br>


## (3) Scope
- Bourne shell의 변수는 선언(declare)될 필요가 없다. (C와 같은 언어와는 달리)
- 선언되지 않은 변수에 접근하려고 하면 empty string("")을 반환받는다. (에러 x)
	- :warning 버그 조심!

<br>


## (4) source
- 작성한 스크립트로부터 환경 변화를 만들어내고 싶다면, 스크립트(코드)를 `source`해야 한다.
		- `.`(dot) command로 스크립트를 source할 수 있다.

<br>


## (5) {}

- 문자열 안에서 `{}`(curly bracket)을 이용하면 변수에 저장된 문자열과 다른 문자열을 이어붙여서 새로운 문자열을 만들 수 있다.

``` shell
#!/bin/sh  
echo  "What is your name?"  
read USER_NAMEecho  "Hello $USER_NAME"  
echo  "I will create you a file called ${USER_NAME}_file"  
touch  "${USER_NAME}_file"
```

> #### 참고
> - **touch**: 리눅스에서 파일을 생성하거나 갱신하는 명령어





<br><br><br><br><br>



## 출처
- [https://www.shellscript.sh/variables1.html](https://www.shellscript.sh/variables1.html)
