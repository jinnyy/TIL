# 코틀린 객체지향 프로그래밍
객체지향 프로그래밍 자체에 대한 설명은 생략하고, 코틀린 언어의 문법과 방식에 관해서만 다루도록 하겠다.

<br><br>


## 1. class와 object
문법은 다른 언어들(Java, Python, javascript 등)과 비슷하다.

* 클래스 안에 객체의 속성(attribute)과 행위(behavior)를 변수와 메소드(함수)로 정의할 수 있다.
* 아래 예시의 경우 `private`라는 키워드를 이용해서 속성의 접근 범위를 설정하고 있다.

```kotlin
class Lamp {
    // property (data member)
    private var isOn: Boolean = false
    // member function
    fun turnOn() {
        isOn = true
    }
    // member function
    fun turnOff() {
        isOn = false
    }
    fun displayLightStatus() {
        if (isOn == true)
            println("lamp is on.")
        else
            println("lamp is off.")
    }
}
fun main(args: Array<String>) {
    val lamp = Lamp()
    lamp.displayLightStatus()
}
```




<br><br><br><br>

## References
* https://www.programiz.com/kotlin-programming/class-objects
