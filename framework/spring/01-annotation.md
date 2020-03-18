# Annotations
자주 사용되는 annotation 정리

<br><br><br>


# 1. 의존성 주입

### @Required
``` java
public class TestBean {
	@Required
	private TestDao testDao;

	public void setTestDao(TestDao testDao) {
		this.testDao = testDao;
	}
}
```
- optional 하지 않은, 꼭 필요한 속성들을 정의
- 설정하지 않을 경우 빈 생성시 예외를 발생시킴

### @Autowired
``` java
// required : 필수인지 여부
@Autowired(required=false)
Test test = new TestTwo();

// 같은 타입의 빈이 2개 이상 존재하게 되면 예외가 발생함
// 이럴 때는 @Qualifier를 사용하여 특정 빈을 사용하도록 지정
@Autowired
@Qualifier("test")
private Test test;
```
- 속성(field), setter method, constructor(생성자)에서 사용
- 스프링이 자동적으로 값을 할당
	-  (new와 생성자를 이용해서 생성하지 않음)
	- **타입**을 이용하여 의존하는 객체를 삽입
- Controller 클래스에서 DAO나 Service에 관한 객체들을 주입 시킬 때 많이 사용
- 스프링 프레임워크에 종속적


### @Inject
- Autowired 어노테이션과 비슷한 역할
- Java 에서 지원하는 어노테이션
- 필드 , 생성자 , 메소드에서 사용

<br><br><br>


# 2. 컨트롤러

### @Controller
- 스프링의 Controller라는 것을 명시
- Spring MVC에서 **Controller 클래스**에 사용됨

### @RestController
- @Controller나 @RestController 중 하나를 **Controller 클래스**에 명시
- Spring에서 Controller 중 View로 응답하지 않는, 컨트롤러를 의미
- 이 어노테이션이 적혀있는 컨트롤러의 메서드는 HttpResponse로 바로 응답이 가능
	- @ResponseBody 역할을 자동적으로 해줌

### @RequestMapping
``` java
@RequestMapping(value = "/path/name", method = RequestMethod.GET)
```
- Spring의 컨트롤러 혹은 그 메서드의 URI를 정의
- GET, POST, PATCH, PUT, DELETE 등 요청 받는 형식도 정의
- @GetMapping, @PostMapping 등 메소드에 따른 annotation도 사용가능하다.

### @PathVariable
``` java
@RequestMapping(value = "/some/path/{id}", method = RequestMethod.GET)  
public ResponseEntity<?> someMethod(@PathVariable int id) {
	// some logic here
}
```
- URI에서 `/` 다음에 넘어오는 값들을 파싱


### @RequestBody
``` java
@RequestMapping(value = "/book", method = RequestMethod.POST)  
public ResponseEntity<?> someMethod(@RequestBody Book book) {
	// Book model type인 book이라는 변수를 사용 가능
}
```
- POST나 PUT, PATCH (body가 있는 메소드) 로 요청을 받을 때, 요청에서 넘어온 body 값들을 자바 타입으로 파싱


### @RequestParam
- ?name=hello 와 같은 쿼리 파라미터를 파싱
``` java
@RequestMapping(value = "/search/movie")
public ResponseEntity<?> someMethod(@RequestParam String name) {
}
```

### @ResponseBody
- HttpMessageConverter 를 이용하여 JSON 혹은 xml 로 요청에 응답할수 있게 해주는 어노테이션
- 이미 RestController 어노테이션이 붙어 있다면, 쓸 필요가 없다

<br><br><br>


# 데이터 접근

### @Service
- Service Class 에서 쓰인다
- 비즈니스 로직을 수행하는 클래스라는 것을 나타냄

### @Repository
- DAO class 에서 쓰인다
	- 데이터베이스에 접근하는 메소드가 있는 클래스에서 쓰임

### @Transactional
- 메소드가 transactional하게 동작하도록 한다.
- class에 적용하면 해당 클래스 내부의 모든 메소드가 transactional하게 동작한다.

<br><br><br>


# 성능 개선 및 기타

### @Async
- method가 비동기방식으로 처리됨
- public 메소드에만 적용해야한다
- 같은 객체 내의 method끼리 호출시에는 @Async가 설정되어있어도 비동기처리가 되지 않음
- 사용방법
	- Application 클래스에 @EnableAsync를 설정하고  
	- 메소드 위에 @Async annotation만 추가

### @Scheduled
1. @EnableScheduling Annotation을 적어서 스케줄링을 사용한다는 것을 알린다.  
``` java
@EnableScheduling
@SpringBootApplication
public  class  SchedulerApplication {
	public  static  void  main(String[] args) {
		SpringApplication.run(SchedulerApplication.class, args);
	}
}  
```
2. 하위 패키지의 클래스에서 주기적으로 수행해야할 메서드 위에 @Scheduled Annotation을 붙인다.  
``` java
@Scheduled(fixedRateString = "5", initialDelay = 3000)
private  void  scheduleTest() {
	logger.error("hello jeong-pro"); 
}
```

- 주기적인 작업이 있을 때 사용
- 예시의 경우 3초의 대기시간(initialDelay) 후에 5ms(fixedRate)마다 "hello jeong-pro"라는 로그를 찍는 작업을 스케줄러가 수행해줌


<br><br><br>


## 출처

- [https://www.baeldung.com/spring-data-annotations](https://www.baeldung.com/spring-data-annotations)
- [medium.com/@aaaalpooo](https://medium.com/@aaaalpooo/많이-쓰는-spring-framework-annotation-정리-summary-of-annotations-frequently-used-in-spring-framework-935e1c1a4877)
- [https://itjava.tistory.com/54](https://itjava.tistory.com/54)
- [https://cornswrold.tistory.com/8](https://cornswrold.tistory.com/8)
- [https://springboot.tistory.com/38](https://springboot.tistory.com/38)
- [http://dveamer.github.io/java/SpringAsync.html](http://dveamer.github.io/java/SpringAsync.html)
- [https://jeong-pro.tistory.com/186](https://jeong-pro.tistory.com/186)
