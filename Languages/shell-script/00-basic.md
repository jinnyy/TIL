# 0. Basic

## 실행방법
* bash에서 다음과 같은 방법으로 실행한다.
``` bash
$ ./filename.sh
```

## 확장자명
* filename&#46;sh
* `.sh`를 붙인다.


## 주석

``` shell
# comment
```


## 변수

### 예 1 - 선언 방법
``` shell
variable ="Hello"
echo $variable
```

### 예 2 - 활용 방법
* 코드
``` shell
#!/bin/sh
echo "what is your name?"
read name
echo "How do you do, $name?"
read remark
echo "I am $remark too!"
```
* 결과

  <img src="https://www.guru99.com/images/program.jpg" />




## 출처
- [https://www.shellscript.sh](https://www.shellscript.sh/)
- [https://www.guru99.com/introduction-to-shell-scripting.html](https://www.guru99.com/introduction-to-shell-scripting.html)
- [https://www.edx.org/](https://www.edx.org/school/linuxfoundationx?g_acctid=926-195-8061&g_campaign=gs-nonbrand-partner-linux&g_campaignid=896086444&g_adgroupid=44419224123&g_adid=263002189865&g_keyword=linux%20tutorials%20for%20beginners&g_keywordid=kwd-332449570444&g_network=g?utm_source=adwords&utm_campaign=896086444&utm_medium=44419224123&utm_term=linux%20tutorials%20for%20beginners&gclid=EAIaIQobChMIlMfs9MSe6AIVDKyWCh2PNwKoEAAYASAAEgK0yvD_BwE)
