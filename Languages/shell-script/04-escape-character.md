# Escape 문자

- `\`를 활용해서 기능이 있는 문자 `"`를 글자 그대로 사용할 수 있다.
- `""` 안에 `"`를 제외한 다른 기능이 있는 문자 (`*`, `'`,  등) 를 넣으면 글자 그대로 사용할 수 있다.

<br><br>


### 공백 문자
- 공백 문자는 `""` 안에 넣어야 취급된다.
```sh
$ echo Hello       World
Hello World
$ echo "Hello       World"
Hello     World
```

<br>


### /
- `Hello "World"`라고 출력하고 싶다면:
``` sh
echo "Hello   \"World\""
```

<br>


### ""

- `""` 안에 	`*`와 `'`를 넣으면 글자 그대로 사용된다:
``` sh
$ echo *
case.shtml escape.shtml first.shtml 
functions.shtml hints.shtml index.shtml 
ip-primer.txt raid1+0.txt
$ echo *txt
ip-primer.txt raid1+0.txt
$ echo "*"
*
$ echo "*txt"
*txt
```

<br><br><br><br><br>



## 출처
- [https://www.shellscript.sh/escape.html](https://www.shellscript.sh/escape.html)
