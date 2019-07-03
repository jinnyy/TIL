# Function

<br><br><br><br>


## 0. 함수의 종류
* 코틀린 표준 함수 (Kotlin Standard Library Function)
* 유저가 정의한 함수 (User-defined functions)

<br><br><br>


## 1. 코틀린 표준 라이브러리 함수
> 참고 https://kotlinlang.org/api/latest/jvm/stdlib/

(당연하게도) 패키지와 클래스로 이루어져 있다. 기본적인 연산(예: `print()`)들을 간단하게 실행할 수 있도록 미리 구현된 것들이다.

<br><br><br>



## 2. 유저가 정의한 함수 (User-defined functions)

### 정의

`fun`이라는 키워드를 이용해서 새로운 함수를 정의할 수 있다.

```kotlin
fun hello() {
}
```

이렇게 정의한 함수를 main 함수에서 call하면 그 때 실행된다.

#### 예시

```kotlin
fun callMe() {
    println("Printing from callMe() function.")
    println("This is cool (still printing from inside).")
}
fun main(args: Array<String>) {
    callMe()
    println("Printing outside from callMe() function.")
}
```
결과는 다음과 같이 나타난다:
```
Printing from callMe() function.
This is cool (still printing from inside).
Printing outside from callMe() function.
```

<br>

### 리턴 타입

리턴 타입을 지정하고 싶을 때에는 함수의 body가 시작되는 curly brace 앞에 `: 타입` 형식으로 사용한다.
하지만 리턴 타입이 존재할 때 타입을 명시하지 않더라도, 컴파일러가 알아낼(infer) 수 있다면 에러가 발생하지 않는다.

```kotlin
fun addNumbers(n1: Double, n2: Double): Int {
    ... .. ...
}
```
<br>

#### 예시

약간 혼란스럽지만, 코틀린에서는 다음과 같은 문법이 허용된다.

```kotlin
fun main(args: Array<String>) {
    println(getName("John", "Doe"))
}
fun getName(firstName: String, lastName: String): String = "$firstName $lastName"
```

위의 코드는 아래와 같은 의미이다.
* `main` 함수에서 `getName()`에 "John"과 "Doe"를 parameter로 보내 함수를 실행한 뒤 리턴값을 `프린트`한다.
* getName() 함수는 두 개의 argument를 받는다. 각각 String 타입이며 함수 내부적으로 firstName과 lastName이라는 변수명으로 사용된다.
* getName() 함수는 `=` 뒤의 내용인 "$firstName $lastName"을 리턴한다. 즉 첫 번째 argument와 두 번째 argument 사이에 공백 하나를 붙인 한 개의 String을 리턴한다..

결과는 다음과 같다:
```
John Doe
```

<br><br><br>



## 3. Infix Notation

함수에서 Infix Notation은 다음과 같은 표현을 의미한다.

```kotlin
a or b  // a.or(b)
a and b // a.and(b)
```

이런 표현을 유저가 정의한 함수에서도 사용할 수 있다.
`infix`라는 키워드를 함수를 정의할 때 앞에 붙여주면 infix notation으로 사용할 수 있는 함수로 정의된다.
예시로 확인하는 것이 이해가 더 빠르다.

```kotlin
class Structure() {
    infix fun createPyramid(rows: Int) {
        var k = 0
        for (i in 1..rows) {
            k = 0
            for (space in 1..rows-i) {
                print("  ")
            }
            while (k != 2*i-1) {
                print("* ")
                ++k
            }
            println()
        }
    }
}
fun main(args: Array<String>) {
    val p = Structure()
    p createPyramid 4       // p.createPyramid(4)
}
```

위와 같이 createPyramid라는 함수를 infix notation으로 사용할 수 있다.


<br><br><br><br>



## References
* https://www.programiz.com/kotlin-programming/functions
* https://kotlinlang.org/api/latest/jvm/stdlib/
