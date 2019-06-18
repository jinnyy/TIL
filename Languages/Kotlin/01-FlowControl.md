# Flow Control

<br><br>


# 1. if

if문은 기본적인 사용방법은 Java 문법과 같다.

```kotlin
if (testExpression) {
   // codes to run if testExpression is true
}
else {
  // codes to run if testExpression is false
}
```
<br>

statement가 한 개인 경우 curly brace(`{}`)를 생략 가능하다.

Java에서는 변수에 값을 assign할 때 if...else문(variable이 아닌 것)을 사용하는 것이 허용되지 않지만, Kotlin에서는 허용된다.

```kotlin
fun main(args: Array<String>) {
    val number = -10
    val result = if (number > 0) "Positive number" else "Negative number"
    println(result)
}
```

<br>

if문 안에 여러 expression이 있다면 마지막에 있는 expression이 해당 블록의 리턴된다.

```kotlin
fun main(args: Array<String>) {

    val a = -9
    val b = -11

    val max = if (a > b) {
        println("$a is larger than $b.")
        println("max variable holds value of a.")
        a
    } else {
        println("$b is larger than $a.")
        println("max variable holds value of b.")
        b
    }
    println("max = $max")
}
```

<br>

연속적으로 `if...else` 문을 사용하고 싶다면 `else if`로 표현하면 된다. (Java와 동일)

<br><br><br>



# 2. when

코틀린의 `when`은 Java의 `switch`문에 비교될 수 있다.


#### 기본적인 사용 방법

```kotlin
fun main(args: Array<String>) {

    val a = 12
    val b = 5

    println("Enter operator either +, -, * or /")
    val operator = readLine()

    val result = when (operator) {
        "+" -> a + b
        "-" -> a - b
        "*" -> a * b
        "/" -> a / b
        else -> "$operator operator is invalid operator."
    }

    println("result = $result")
}
```


#### 다른 방법

`->`의 왼쪽에 다수의 값을 `,`로 표현할 수 있다.

```kotlin
fun main(args: Array<String>) {

    val n = -1

    when (n) {
        1, 2, 3 -> println("n is a positive integer less than 4.")
        0 -> println("n is zero")
        -1, -2 -> println("n is a negative integer greater than 3.")
    }
}
```

range로도 표현할 수 있다.
```kotlin
fun main(args: Array<String>) {

    val a = 100

    when (a) {
        in 1..10 -> println("A positive number less than 11.")
        in 10..100 -> println("A positive number between 10 and 100 (inclusive)")
    }
}
```

타입을 검사할 수 있다.
```kotlin
when (x) {
    is Int -> print(x + 1)
    is String -> print(x.length + 1)
    is IntArray -> print(x.sum())
}
```

codition 부분에 expression을 사용하는 것도 가능하다. (값을 얻어내기만 하면 되는듯하다)
```kotlin
fun main(args: Array<String>) {

    val a = 11
    val n = "11"

    when (n) {
        "cat" -> println("Cat? Really?")
        12.toString() -> println("Close but not close enough.")
        a.toString() -> println("Bingo! It's eleven.")
    }
}
```

<br><br><br>


# 3. while loop

java의 사용방법과 다르지 않다.

<br><br><br>




# 4. for loop


```kotlin

fun main(args: Array<String>) {


    // 기본적인 사용 방법

for (i in 1..5) {

println(i)

}



//for(int i=5; i>=1; i--)

for (i in 5 downTo 1) print(i)


// for(int i=1; i<=5; i+=2)

for (i in 1..5 step 2) print(i)


// for(int i=5; i>=1; i+=2)

for (i in 5 downTo 1 step 2) print(i)


}

```


숫자 사이에 `...`을 사용하거나, `downTo` 키워드를 사용해 큰 숫자에서 작은 숫자 순으로 for문을 실행할 수 있다. `step` 키워드를 사용하면 커지거나 작아지는 간격을 조절할 수 있다.

<br><br>

## Iterate through an Array


```kotlin

fun main(args: Array<String>) {


   var language = arrayOf("Ruby", "Koltin", "Python" "Java")


   for (item in language)

       println(item)

}

```


아래와 같이 `.indices` 를 이용해서 인덱스를 탐색하는 것도 가능하다.


```kotlin

fun main(args: Array<String>) {


   var language = arrayOf("Ruby", "Koltin", "Python", "Java")


   for (item in language.indices) {


       // printing array elements having even index only

       if (item%2 == 0)

           println(language[item])

   }

}

```


## Iterate through a String


```kotlin

fun main(args: Array<String>) {


   var text= "Kotlin"


   for (letter in text) {

       println(letter)

   }

}

```


<br><br><br>



# 5. Tail Recursion


`tailrec`이라는 키워드를 이용해서 tail recursion을 하도록 컴파일러에게 명령할 수 있다. 이 키워드로 recursion을 최적화할 수 있다.





<br><br><br><br>




# References

* https://www.programiz.com/kotlin-programming/if-expression
* https://www.programiz.com/kotlin-programming/when-expression
* https://www.programiz.com/kotlin-programming/while-loop
* https://www.programiz.com/kotlin-programming/for-loop
