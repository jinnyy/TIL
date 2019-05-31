# Introduction

<br><br>

## 0. Basics
### 0-1) 코틀린이란

코틀린은 JVM 위에서 실행되는 프로그래밍 언어이다.
오픈 소스이며, 다양한 언어(Java, Scala, Groovy, C#, JavaScript and Gosu)에 영향을 받았다.
따라서 이와 같은 언어를 알고 있는 학습자는 비교적 쉽게 학습할 수 있다.(라고 한다)

코틀린은 statically typed(컴파일 시 타입이 정해지는) 언어이지만 JavaScript와 같은 loosely typed 언어와도 호환 가능하다.

<br>



### 0-2) 설치

이클립스를 사용하는 경우 다음 링크를 참고해 설치 가능하다.

https://kotlinlang.org/docs/tutorials/getting-started-eclipse.html

<br><br>



## 1. 첫번째 코틀린 애플리케이션

#### helloWorld.kt
```kotlin
// main function
fun main(args: Array<String>) {
	println("Hello World!")
}
```

* `fun`이라는 키워드를 사용해 함수를 정의하고 있다.
* main function에서부터 컴파일이 시작된다.

위의 코틀린 코드는 아래의 자바 코드와 같다.

#### HelloWorld.java
```java
class HelloWorldKt {
    public static void main(String[] args) {
        System.out.println("Hello, World!"); 
    }
}
```

여기에서 알 수 있는 코틀린의 특징은 다음과 같다.

* 프로그램 안에 `class`가 없어도 된다.
* `println()`함수가 내부적으로 `System.out.println()`을 call한다.

<br><br>

## 2. 변수와 타입
코틀린에서는 변수(variable)를 선언하기 위해 `var`와 `val` 키워드가 사용된다.

* `val`: initialize된 후 수정 불가능하다. (Java의 `final` 변수와 유사) (Immutable Reference)
* `var`: 수정 가능하다. (Mutable Reference)


```kotlin
var language = "French"
val score = 95
```

타입을 명시적(explicitly)으로 선언하고 싶다면 다음과 같은 문법으로 선언 가능하다.
```kotlin
var language: String = "French"
val score: Int = 95
```

> #### 참고
> 타입이 명시적으로 표현되지 않은 경우, declare와 initialize를 서로 다른 위치에서 하는 것이 허용되지 않는다.
> ```kotlin
> var language           // Error 
> language = "French"
> ```








<br><br><br>

## References

https://www.programiz.com/kotlin-programming

