# 2. 변수

<br>

- 타입을 지정하지 않는다.
- string, integer, real number 등 다양한 타입을 store할 수 있다.
- 변수를 선언한 뒤, 변수를 사용하고자할 때에는 변수 이름 앞에 `$`를 붙인다.
- 변수에 값이 할당되기 전에 사용되면 blank로 취급된다.

``` shell
MY_MESSAGE="Hello World"
echo $MY_MESSAGE
```

<br><br><br>


## expr

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


## read

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



<br><br><br>


## 출처
- [https://www.shellscript.sh/variables1.html](https://www.shellscript.sh/variables1.html)
