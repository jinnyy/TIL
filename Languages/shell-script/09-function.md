
# Function

- `exit`
	- shell script를 종료함
	- 프로그램을 멈춤
- `return`
	- 함수를 종료하거나 종료하면서 값을 리턴
	- caller에게 control을 반환

형식
``` sh
함수이름()
{
	명령어
}
```

<br><br><br>

## Scope of variables
- 기본적으로는 scope가 없다.
- 매개 변수(1, $2, $@ 등)만 scope가 있음


#### 예
* code
	``` sh
	#!/bin/sh

	### function
	myfunc()
	{
	  echo "I was called as : $@"
	  x=2
	}

	### Main script
	echo "Script was called with $@"
	x=1
	echo "x is $x"
	myfunc 1 2 3
	echo "x is $x"
	```

* output
	``` sh
	Script was called with a b c
	x is 1
	I was called as : 1 2 3
	x is 2
	```

<br><br><br>

## Recursion
- 함수는 재귀 가능하다

#### 예
``` sh
#!/bin/sh

factorial()
{
  if [ "$1" -gt "1" ]; then
    i=`expr $1 - 1`
    j=`factorial $i`
    k=`expr $1 \* $j`
    echo $k
  else
    echo 1
  fi
}


while :
do
  echo "Enter a number:"
  read x
  factorial $x
done
```

<br><br><br>



## Return Codes
- caller에게 control을 반환한다.
- 이(반환할) 때 값도 함께 리턴할 수 있다.

``` sh
#!/bin/sh

### function
adduser()
{
  USER=$1
  PASSWORD=$2
  shift ; shift
  COMMENTS=$@
  useradd -c "${COMMENTS}" $USER
  if [ "$?" -ne "0" ]; then
    echo "Useradd failed"
    return 1
  fi
  passwd $USER $PASSWORD
  if [ "$?" -ne "0" ]; then
    echo "Setting password failed"
    return 2
  fi
  echo "Added user $USER ($COMMENTS) with pass $PASSWORD"
}

## Main script
adduser bob letmein Bob Holness from Blockbusters
ADDUSER_RETURN_CODE=$?
if [ "$ADDUSER_RETURN_CODE" -eq "1" ]; then
  echo "Something went wrong with useradd"
elif [ "$ADDUSER_RETURN_CODE" -eq "2" ]; then 
   echo "Something went wrong with passwd"
else
  echo "Bob Holness added to the system."
fi
```

<br><br><br><br><br>



## 출처
- [https://www.shellscript.sh/functions.html](https://www.shellscript.sh/functions.html)
