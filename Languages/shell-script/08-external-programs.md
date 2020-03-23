
# External Programs

<br><br><br>

## Backtick (`)

- 외부 명령어(external commands)는 backtick (`)과 관련이 많다.
	- `` ` ` ``(backtick) 안에 있는 text는 command로 실행된다는 것을 나타낸다.

<br>

### 예 

#### 1. 명령어의 결과값

* 다음과 같은 명령어의 결과값을 변수에 넣고자한다면
	``` sh
	$ grep "^${USER}:" /etc/passwd | cut -d: -f5
	Steve Parker
	```
* 아래와 같이 `(backtick) 안에 해당 명령어를 넣는다.
	``` sh
	$ MYNAME=`grep "^${USER}:" /etc/passwd | cut -d: -f5`
	$ echo $MYNAME
	Steve Parker
	```

<br>


#### 2. 명령어의 재사용

* 다음과 같이 반복되는 command가 있을 때
	``` sh
	#!/bin/sh
	find / -name "*.html" -print | grep "/index.html$"
	find / -name "*.html" -print | grep "/contents.html$"
	```
* 아래와 같이 변수에 command를 넣어줌으로써 성능을 개선할 수 있다.
	``` sh
	#!/bin/sh
	HTML_FILES=`find / -name "*.html" -print`
	echo "$HTML_FILES" | grep "/index.html$"
	echo "$HTML_FILES" | grep "/contents.html$"
	```

<br><br><br>



## External Commands
- `tr`, `grep`, `expr`, `cut` 등


### tr
* tr은 translate의 약자이다.
* 번역하듯이 바꾸거나 삭제하는 command이다.

형식
``` sh
$ tr [OPTION] SET1 [SET2]
```

<details>
	<summary>옵션</summary>

* -c : 문자열을 덧붙임 (예: 주어진 set에 없는 문자들을 붙이는 연산)
* -d : `SET1`의 문자를 결과값에서 삭제
* -s : `SET1`에 나열된 반복 문자를 한 번만 등장한 것으로 대체
* -t : `SET1` 잘라내기
	
</details>

예
* 사용할 문서
	* code
	``` sh
	$cat greekfile
	```
	* output
	``` sh
	WELCOME TO 
	GeeksforGeeks
	```
* 예 1 - 소문자를 대문자로
	* code
	``` sh
	$ cat greekfile | tr “[a-z]” “[A-Z]”
	```
	``` sh
	$ cat geekfile | tr “[:lower:]” “[:upper:]”
	```
	* output
	``` sh
	WELCOME TO
	GEEKSFORGEEKS
	```
* 예 2 - 공백을 tab으로
	* code
	``` sh
	$ echo "Welcome To GeeksforGeeks" | tr [:space:] '\t'
	```
	* output
	``` sh
	Welcome    To    GeeksforGeeks
	```

<br>


### grep
* 입력으로 전달된 파일의 내용에서 특정 문자열을 찾고자할 때 사용하는 명령어
- **정규 표현식(Regular Expression)**에 의한 **패턴 매칭(Pattern Matching)** 방식 사용

형식
``` sh
$ grep [OPTION] [PATTERN] [FILE]
```

<details>
	<summary>옵션</summary>

* -E        : PATTERN을 확장 정규 표현식(Extended RegEx)으로 해석.
* -F        : PATTERN을 정규 표현식(RegEx)이 아닌 일반 문자열로 해석.
* -G        : PATTERN을 기본 정규 표현식(Basic RegEx)으로 해석.
* -P        : PATTERN을 Perl 정규 표현식(Perl RegEx)으로 해석.
* -e        : 매칭을 위한 PATTERN 전달.
* -f        : 파일에 기록된 내용을 PATTERN으로 사용.
* -i        : 대/소문자 무시.
* -v        : 매칭되는 PATTERN이 존재하지 않는 라인 선택.
* -w        : 단어(word) 단위로 매칭.
* -x        : 라인(line) 단위로 매칭.
* -z        : 라인을 newline(\n)이 아닌 NULL(\0)로 구분.
* -m        : 최대 검색 결과 갯수 제한.
* -b        : 패턴이 매치된 각 라인(-o 사용 시 문자열)의 바이트 옵셋 출력.
* -n        : 검색 결과 출력 라인 앞에 라인 번호 출력.
* -H        : 검색 결과 출력 라인 앞에 파일 이름 표시.
* -h        : 검색 결과 출력 시, 파일 이름 무시.
* -o        : 매치되는 문자열만 표시.
* -q        : 검색 결과 출력하지 않음.
* -a        : 바이너리 파일을 텍스트 파일처럼 처리.
* -I        : 바이너리 파일은 검사하지 않음.
* -d        : 디렉토리 처리 방식 지정. (read, recurse, skip)
* -D        : 장치 파일 처리 방식 지정. (read, skip)
* -r        : 하위 디렉토리 탐색.
* -R        : 심볼릭 링크를 따라가며 모든 하위 디렉토리 탐색.
* -L        : PATTERN이 존재하지 않는 파일 이름만 표시.
* -l        : 패턴이 존재하는 파일 이름만 표시.
* -c        : 파일 당 패턴이 일치하는 라인의 갯수 출력.

</details>

<br>

### expr

* 주어진 표현을 연산하고 결과값(만)을 보여준다.
* 사용되는 곳
	* 사칙연산, 정수에 대한 modular 연산등 기본적인 연산
	* 정규식, substring, 문자열 길이 등

형식
``` sh
$ expr [연산]
```

예
* 예 1 - basic arithmetic operations
	* 덧셈
		* code
		``` sh
		$ expr 12 + 8
		```
		* output
		``` sh
		20
		```
	* 곱셈
		* code
		``` sh
		$ expr 12 \* 2
		```
		* output
		``` sh
		24
		```
* 예 2
	* code
	``` sh
	echo "Enter two numbers"
	read x 
	read y
	sum=`expr $x + $y`
	echo "Sum = $sum"
	```
	* output
	``` sh
	Enter two numbers
	12 # 입력한 숫자
	28 # 입력한 숫자
	Sum = 40
	```


<br>

### cut
* 리눅스에서 파일 내용을 각 필드로 구분하고 필드별로 내용을 추출
* 각 필드들을 구분자로 구분

형식
``` sh
$ cut [옵션] [파일명]
```

<details>
	<summary>옵션</summary>
	
-   -b, --bytes=LIST : 바이트 단위로 선택
-   -c, --characters=LIST : 문자 단위로 선택
-   -d, --delimiter=DELIM : 필드를 구분짓는 기본 값은 TAB 대신에 DELIM을 사용
-   -f, --fields=LIST : 지정한 필드만을 출력
-   -s, --only-delimited : 필드 구분자를 포함하지 않는 줄은 미출력
-   --output-delimiter=STRING : 출력할때 구분자 대신에 STRING을 사용하며, STRING는 문자나 빈칸 등을 사용
-   --help : 도움말 출력
-   --version : 버전정보 출력
- -b, -c, -f 사용시 다음과 같이 특정 숫자 범위를 사용 가능

	| 형식 | 의미 |
	|:--:|:--:|
	| N | N 번째 바이트, 문자 또는 필드 |
	| N-M | N번째부터 M번째 까지의 바이트, 문자 또는 필드(M번째 포함) |
	| M | 처음부터 M번째 까지의 바이트, 문자 또는 필드 |

</details>

<br><br><br><br><br>




## 출처
- [https://www.shellscript.sh/external.html](https://www.shellscript.sh/external.html)
- [리눅스 기본명령어 - cut](http://www.incodom.kr/Linux/%EA%B8%B0%EB%B3%B8%EB%AA%85%EB%A0%B9%EC%96%B4/cut)
- [리눅스 grep 명령어 사용법. (Linux grep command) - 리눅스 문자열 검색](https://recipes4dev.tistory.com/157)
- [https://www.tecmint.com/tr-command-examples-in-linux/](https://www.tecmint.com/tr-command-examples-in-linux/)
- [geeks for geeks - tr](https://www.geeksforgeeks.org/tr-command-in-unix-linux-with-examples/)
- [geeks for geeks - expr](https://www.geeksforgeeks.org/expr-command-in-linux-with-examples/)
