# 변수 (2)

1. [`$n` 시리즈](#n-시리즈)
	- `$#`, `$0`, `$1`, ... `$9` 라는 형식의 변수를 사용가능하다.

2. [shift](#shift)
	- `shift`라는 명령어를 이용해 9개 이상의 parameter를 받을 수 있다.

3. [{}](#curly-bracket-)




<br><br><br>



## $n 시리즈

- `$#`: parameter의 개수
- `$0`: 실행되는 프로그램의 basename
- `$1`, ... `$9`: 첫 번째, ... 9번째 parameter
- `$?`: 마지막으로 실행한 command의 exit value
	- 예: 0 - 정상 종료
- `$!`: 마지막으로 실행한 background 프로세스의 pid
	- (마지막으로 실행한 background 프로세스가) 없으면 공백
- `IFS`: _Internal Field Separator_
	- default 값은 `SPACE TAB NEWLINE` (변경 가능)

<br>

#### 예시 - $#, $0, $1...9

* 코드
	var3<span>.sh</span>
	``` sh
	#!/bin/sh
	echo "I was called with $# parameters"
	echo "My name is $0"
	echo "My first parameter is $1"
	echo "My second parameter is $2"
	echo "All parameters are $@"
	```

* 결과
	``` sh
	$ ./var3.sh
	I was called with 0 parameters
	My name is /home/steve/var3.sh
	My first parameter is
	My second parameter is    
	All parameters are 
	$
	$ ./var3.sh hello world earth
	I was called with 3 parameters
	My name is ./var3.sh
	My first parameter is hello
	My second parameter is world
	All parameters are hello world earth
	```

#### 예시 - $?
* 코드
	``` sh
	#!/bin/sh
	/usr/local/bin/my-command
	if [ "$?" -ne "0" ]; then
	  echo "Sorry, we had a problem there!"
	fi
	```
* 결과
	- 프로그램이 0을 리턴하지 않았으면 -> "Sorry, we had a problem there!"를 출력


<br><br><br>


## shift
- `shift`라는 명령어를 이용해 9개 이상의 parameter를 받을 수 있다.

#### 예시 - shift
* 코드
	``` sh
	#!/bin/sh
	while [ "$#" -gt "0" ]
	do
	  echo "\$1 is $1"
	  shift
	done
	```	
* 결과
	* $#이 0이 될 때까지 shift를 반복한다.

<br><br><br>


## Curly Bracket `{}`
- 변수를 사용할 때 `{}`를 사용하면 코드를 더 분명하게 만들 수 있다.
	``` sh
	foo=sun
	echo $fooshine     # $fooshine is undefined
	echo ${foo}shine   # displays the word "sunshine"
	```
- 변수가 undefined or null일 때에 관한 이슈에 대응할 수 있다.
- `:-`로 default 값을 지정할 수 있다.
	``` sh
	echo -en "What is your name [ `whoami` ] "
	read myname
	echo "Your name is : ${myname:-`whoami`}"
	```
	> 참고
	> * `` `whoami` ``:  login name (UID)
	> * `-en`: echo에 옵션으로 부여 시 linebreak를 추가하지 말라는 뜻 (bash and csh)



<br><br><br><br><br>



## 출처
- [https://www.shellscript.sh/variables2.html](https://www.shellscript.sh/variables2.html)
