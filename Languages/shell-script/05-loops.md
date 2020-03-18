# Loops

- [`for` loops](#for-loops)
- [`while` loops](#while-loops)


<br><br><br>


## For Loops
list의 모든 값을 iterate한다.

### 형식
``` sh
for i in {리스트 값 나열}
do
  {수행할 작업}
done
```
- (당연히) wildcard 등 shell script의 다른 문법도 사용할 수 있다.

<br><br>


### 예시

#### [1]
코드
``` sh
for i in 1 2 3 4 5
do
  echo "Looping ... number $i"
done
```
결과
``` sh
Looping .... number 1
Looping .... number 2
Looping .... number 3
Looping .... number 4
Looping .... number 5
```

<br>


#### [2]
코드
``` sh
for i in hello 1 * 2 goodbye 
do
  echo "Looping ... i is set to $i"
done
```

결과
``` sh
Looping ... i is set to hello
Looping ... i is set to 1
Looping ... i is set to (name of first file in current directory)
    ... etc ...
Looping ... i is set to (name of last file in current directory)
Looping ... i is set to 2
Looping ... i is set to goodbye
```

<br><br><br>



## While Loops

### 형식
``` sh
while {조건}
do
  {수행할 작업}
done
```

<br><br>

### 예시

#### [1]
- keyboard input으로 `bye`를 받을 때까지 while문이 계속 실행된다.

``` sh
INPUT_STRING=hello
while [ "$INPUT_STRING" != "bye" ]
do
  echo "Please type something in (bye to quit)"
  read INPUT_STRING
  echo "You typed: $INPUT_STRING"
done
```

<br>

#### [2]
- `:`은 항상 `true`로 취급된다.

``` sh
while :
do
  echo "Please type something in (^C to quit)"
  read INPUT_STRING
  echo "You typed: $INPUT_STRING"
done
```



<br><br><br><br><br>



## 출처
- [https://www.shellscript.sh/loops.html](https://www.shellscript.sh/loops.html)
