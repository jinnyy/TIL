# 와일드카드

- `*`를 와일드카드로 사용할 수 있다.
- (정규식과는 달리) 글자 수와 관계 없이 모든 글자에 매칭된다.

<br><br>

### 복사
모든 파일을 복사하려면:

#### 예
/tmp/a/에 있는 모든 파일을 /tmp/b/로 복사

``` shell
# 모든 파일
$ cp  /tmp/a/*  /tmp/b/
# 모든 .txt 파일
$ cp  /tmp/a/*.txt /tmp/b/
# 모든 .html 파일
$ cp  /tmp/a/*.html /tmp/b/
```

<br>

### 이동

#### 예
모든 .txt 파일을 .bak으로 바꾸고 싶을 때

- `mv`를 이용해 다음과 같이 실행하면
	``` sh
	$ mv  *.txt *.bak
	```
	- 모든 .txt 파일의 이름이 *.bak으로 바뀐다.

- loop를 이용해야 한다.
- 참고
	``` sh
	# Rename all *.txt to *.text
	for f in *.txt; do 
	    mv -- "$f" "${f%.txt}.text"
	done
	```





<br><br><br><br><br>



## 출처
- [https://www.shellscript.sh/wildcards.html](https://www.shellscript.sh/wildcards.html)
