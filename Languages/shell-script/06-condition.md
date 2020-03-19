# 조건
조건의 true / false를 표현한다.

- `[`는 `test`의 symbolic link이다.
	- `[`라고 쓰면 `test`로 interpret된다는 뜻이다.
- `[]`는 프로그램으로 취급되므로, 양 끝에 space(` `)로 둘러싸여 있어야 한다.

<br><br><br>


## if

- `if`, `then`, (`elif`, `else`), `fi`로 이루어져 있다.
- 끝낼 때 반드시 fi를 써야 한다.
``` sh
if [ ... ]
then
  # if-code
else
  # else-code
fi
```

`;`를 사이에 써서 `if`와 `then`을 같은 line에 쓸 수 있다.
``` sh
if [ ... ]; then
  # do something
fi
```

<br><br><br>

## 기타
- `&&`로 `{조건} AND {조건}`이라는 의미를 나타낸다.
- `||`로 `{조건} OR {조건}` 이라는 의미를 나타낸다.
- `\` = 한 줄에 써야 할 내용을 다음 줄에 **이어서** 쓸 때
	``` sh
	[ "$X" -nt "/etc/passwd" ] && \
      echo "X is a file which is newer than /etc/passwd"
	```
- `;` = 여러 줄에 써야 할 내용을 한 줄에 **끊어서** 쓸 때
	``` sh
	if [ "$X" -nt "/etc/passwd" ]; then
	  echo "X is a file which is newer than /etc/passwd"
	fi
	```


<br><br><br><br><br>



## 출처
- [https://www.shellscript.sh/test.html](https://www.shellscript.sh/test.html)
