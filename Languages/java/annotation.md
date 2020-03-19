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

## 출처
- [https://elfinlas.github.io/2017/12/14/java-annotation/](https://elfinlas.github.io/2017/12/14/java-annotation/)
- [https://k39335.tistory.com/40](https://k39335.tistory.com/40)
- [https://elfinlas.github.io/2017/12/14/java-custom-anotation-01/](https://elfinlas.github.io/2017/12/14/java-custom-anotation-01/)
