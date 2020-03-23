# Annotation


## 어노테이션이란
- 주석처럼 코드에 달아 특별한 의미를 부여하거나 기능을 주입할 수 있다.
- 기본적으로 interface 형태
- interface 앞에 @을 붙인다
- java 5부터 지원

<br>

## 커스텀 어노테이션

어노테이션을 정의하는 인터페이스
- `@interface`로 annotation임을 나타냄
- `InsertIntData`는 annotation의 이름이 됨
``` java
@Target(ElementType.FIELD)  
@Retention(RetentionPolicy.RUNTIME)
public @interface InsertIntData {
	int data() default 0;  
}
```

어노테이션을 사용하는 클래스
- 변수 위에 `@어노테이션 이름` 형식으로 어노테이션을 사용
``` java
public class AnnotationExam01 {  
	@InsertIntData(data = 30)  
	private int myAge;  
  
	@InsertIntData  
	private int defaultAge;  
  
	public AnnotationExam01() {  
		this.myAge = -1;  
		this.defaultAge = -1;  
	}  
  
	public int getMyAge() {  
		return myAge;  
	}  
  
	public int getDefaultAge() {  
		return defaultAge;  
	}
} 
```

<br><br><br>

## Meta Annotations

### @Target
``` java
@Target(ElementType.이름)
```
* 어노테이션을 적용할 위치를 지정한다
* package java.lang.annotation 에 있는 ElementType의 내용을 인자로 넘겨준다.
* 예
	* @Target(ElementType.METHOD)
	* @Target({ElementType.CONSTRUCTOR, ElementType.METHOD, ElementType.PARAMETER, ElementType.FIELD, ElementType.ANNOTATION_TYPE})


### @Retension
``` java
@Retension(RetentionPolicy.이름)
```
* 어노테이션의 범위(?). 어떤 시점까지 어노테이션이 영향을 미치는지 결정  
* 인자 종류
	* `SOURCE`: 컴파일 시 버려짐. 클래스 파일에는 포함되지 않는다.
	* `CLASS`: class file에는 남지만 런타임시 (VM에 의해) 남지 않는다.
	* `RUNTIME`: (컴파일러에 의해) class file에 남고, (VM에 의해) 런타임 시에도 유지된다.


### @Documented
* 문서에도 어노테이션의 정보가 표현됨

<br><br><br>

## 출처
- [https://elfinlas.github.io/2017/12/14/java-annotation/](https://elfinlas.github.io/2017/12/14/java-annotation/)
- [https://k39335.tistory.com/40](https://k39335.tistory.com/40)
- [https://elfinlas.github.io/2017/12/14/java-custom-anotation-01/](https://elfinlas.github.io/2017/12/14/java-custom-anotation-01/)

Meta Annotations
- [https://codediver.tistory.com/71](https://codediver.tistory.com/71)
- [https://medium.com/@ggikko/java-%EC%BB%A4%EC%8A%A4%ED%85%80-annotation-436253f395ad](https://medium.com/@ggikko/java-%EC%BB%A4%EC%8A%A4%ED%85%80-annotation-436253f395ad)
