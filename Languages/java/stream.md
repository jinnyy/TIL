# Stream

* Java 8 부터는 Stream이라는 기술이 추가되었다.
* 람다를 활용할 수 있는 기술 중 하나

<br>

#### 왜 사용할까?
* Array 또는 컬렉션 인스턴스에 함수 여러 개를 조합해서 원하는 결과를 필터링하고 가공한 결과를 얻음
* 람다를 이용해서 코드의 양을 줄이고 간결하게 표현
* 간단하게 병렬처리(multi-threading)가 가능

<br>

#### 사용 과정
1. [생성하기](https://oss.navercorp.com/yeonjin-kim0309/study-archive/blob/master/language/java/stream.md#1-생성하기) : 스트림 인스턴스 생성
2. [가공하기](https://oss.navercorp.com/yeonjin-kim0309/study-archive/blob/master/language/java/stream.md#2-가공하기) : 필터링(filtering) 및 맵핑(mapping) 등 원하는 결과를 만들어가는 중간 작업(intermediate operations)
3. [결과 만들기](https://oss.navercorp.com/yeonjin-kim0309/study-archive/blob/master/language/java/stream.md#3-결과-만들기) : 최종적으로 결과를 만들어내는 작업(terminal operations)

<br><br><br><br><br>




# 1. 생성하기

## 1-1) 배열 스트림
#### 생성
``` java
T[] arr = {};
Stream<T> streamAll = Arrays.stream(arr);		// 전체
Stream<T> streamPartial = Arrays.stream(arr, 0, 3);	// 0번째 ~ 2번째
```

<br>


## 1-2) 컬렉션 스트림

컬렉션 타입(_Collection, List, Set_)의 경우 인터페이스에 추가된 디폴트 메소드 `stream` 을 이용 가능

#### 컬렉션 타입 정의
``` java
public interface Collection<E> extends Iterable<E> {  
	default Stream<E> stream() {
		return StreamSupport.stream(spliterator(), false);
	}
 // ...  
}
```

#### 생성
``` java
List<String> list = Arrays.asList("a", "b", "c");
Stream<String> stream = list.stream();
Stream<String> parallelStream = list.parallelStream(); // 병렬 처리 스트림
```

<br>


## 1-3) 비어 있는 스트림

#### 생성
``` java
Stream<T> streamExample = Stream.empty();
```

#### 사용 예시
``` java
public Stream<String> streamOf(List<String> list) {  
 return list == null || list.isEmpty()   
 ? Stream.empty()   
 : list.stream();  
}
```

<br>

## 1-4) Stream.builder()
스트림에 직접적으로 원하는 값을 넣을 수 있음
* Stream.builder()로 빌더를 만들고
* 값을 add한 뒤 마지막에 build() 메소드로 생성

#### 생성

``` java
Stream<String> builderStream =   
 Stream.<String>builder()  
 .add("Eric").add("Elena").add("Java")  
 .build(); // [Eric, Elena, Java]
```

<br>

## 1-5) Stream.generate()

* `generate` 메소드를 이용하면 `Supplier<T>` 에 해당하는 람다로 값을 넣을 수 있음
* `Supplier<T>` 는 인자는 없고 리턴값만 있는 함수형 인터페이스
* 람다 함수에서 리턴하는 값이 들어감
* 특정 사이즈로 최대 크기를 제한해야 함
	* 크기가 정해져있지 않은 무한(_infinite_)한 스트림이 생성되기 때문에 

#### 생성
``` java
Stream<String> generatedStream =   
 Stream.generate(() -> "gen").limit(5); // [el, el, el, el, el]
```

<br>

## 1-6) Stream.iterate()
초기값과 해당 값을 다루는 람다를 이용해서 스트림에 들어갈 요소를 만듦

#### 생성
``` java
Stream<Integer> iteratedStream =  
	Stream.iterate(30, n -> n + 2).limit(5); // [30, 32, 34, 36, 38]
```

<br>

## 1-7) 기본 타입(primitive type)형 스트림
* 제네릭을 사용하지 않고 직접적으로 해당 타입의 스트림을 다룸
* `range` : 두 번째 인자인 종료지점이 포함 안 됨
* `rangeClosed` : 두 번째 인자인 종료지점이 포함됨

#### 생성
``` java
IntStream intStream = IntStream.range(1, 5); // [1, 2, 3, 4]  
LongStream longStream = LongStream.rangeClosed(1, 5); // [1, 2, 3, 4, 5]
```

* 제네릭을 사용하지 않기 때문에 불필요한 오토박싱(_auto-boxing_)이 일어나지 않음
* 필요한 경우 `boxed` 메소드를 이용해서 박싱(_boxing_)할 수 있음

``` java
Stream<Integer> boxedIntStream = IntStream.range(1, 5).boxed();
```


<br>


## 1-8) 문자열 스트림
* `IntStream`: String 타입 객체에 chars() 메소드로 스트림을 만들면 primitive type인 int들의 스트림이 생성된다.
* `Stream<String>`: String 객체들의 스트림

#### 생성
``` java
IntStream charsStream =   
	"Stream".chars(); // [83, 116, 114, 101, 97, 109]
```

``` java
Stream<String> stringStream =  
	Pattern.compile(", ").splitAsStream("Eric, Elena, Java");
```

<br>


## 1-9) 파일 스트림
* 자바 NIO 의 `Files` 클래스의 `lines` 메소드
* 해당 파일의 각 라인을 스트링 타입의 스트림으로 만들어줌

#### 생성
``` java
Stream<String> lineStream = Files.lines(
	Paths.get("file.txt"),
	Charset.forName("UTF-8")
	);
```

<br>

## 1-10) 병렬 스트림
* 스트림 생성 시 사용하는 `stream` 대신 `parallelStream` 메소드를 사용
* 내부적으로는 쓰레드를 처리하기 위해 자바 7부터 도입된 [Fork/Join framework](https://docs.oracle.com/javase/tutorial/essential/concurrency/forkjoin.html) 를 사용

#### 생성
``` java
// 병렬 스트림 생성  
Stream<Product> parallelStream = productList.parallelStream();  
  
// 병렬 여부 확인  
boolean isParallel = parallelStream.isParallel();
```

<br>

## 1-11) Stream.concat()
* `Stream.concat` 메소드를 이용해 두 개의 스트림을 연결해서 새로운 스트림을 생성

#### 생성
``` java
Stream<String> stream1 = Stream.of("Java", "Scala", "Groovy");  
Stream<String> stream2 = Stream.of("Python", "Go", "Swift");  
Stream<String> concat = Stream.concat(stream1, stream2);  
// [Java, Scala, Groovy, Python, Go, Swift]
```

<br><br><br>



# 2. 가공하기
* 작업은 스트림을 리턴하기 때문에 여러 작업을 이어 붙여서(_chaining_) 작성할 수 있다.
``` java
List<String> names = Arrays.asList("Eric", "Elena", "Java");
```
> 위 리스트를 바탕으로 아래 예시가 작성되었다.

## 2-1) Filtering

``` java
Stream<String> stream =   
	names.stream()  
	.filter(name -> name.contains("a"));  
// [Elena, Java]
```

<br>


## 2-2) Mapping

### map
``` java
Stream<String> stream =   
	names.stream()  
	.map(String::toUpperCase);  
// [ERIC, ELENA, JAVA]
```

### flatMap

``` java
students.stream()  
	.flatMapToInt(student ->   
	IntStream.of(student.getKor(),   
	student.getEng(),   
	student.getMath()))  
	.average().ifPresent(avg ->   
	System.out.println(Math.round(avg * 10)/10.0));
```

<br>


## 2-3) Sorting

``` java
IntStream.of(14, 11, 20, 39, 23)  
	.sorted()  
	.boxed()  
	.collect(Collectors.toList());
```

## 2-4) Iterating

``` java
int sum = IntStream.of(1, 3, 5, 7, 9)  
	.peek(System.out::println)  
	.sum();
```

<br><br><br>



# 3. 결과 만들기
* 최소, 최대, 합, 평균 등 기본형 타입으로 결과를 만들어낼 수 있음

## 3-1) Calculating

#### 예
``` java
long count = IntStream.of(1, 3, 5, 7, 9).count();  
long sum = LongStream.of(1, 3, 5, 7, 9).sum();

// 스트림이 비어있을 때 default로 값을 출력할 수 없는 경우 Optional을 이용
OptionalInt min = IntStream.of(1, 3, 5, 7, 9).min();  
OptionalInt max = IntStream.of(1, 3, 5, 7, 9).max();

// 스트림에서 Optional을 처리할 수도 있음
DoubleStream.of(1.1, 2.2, 3.3, 4.4, 5.5)
	.average()  
	.ifPresent(System.out::println);
```

<br>

## 3-2) Reduction
* 스트림은 `reduce`라는 메소드를 이용해서 결과를 만들어냄

#### parameters
-   accumulator : 각 요소를 처리하는 계산 로직. 각 요소가 올 때마다 중간 결과를 생성하는 로직
-   identity : 계산을 위한 초기값으로 스트림이 비어서 계산할 내용이 없더라도 이 값은 리턴
-  combiner : 병렬(_parallel_) 스트림에서 나눠 계산한 결과를 하나로 합치는 동작하는 로직

``` java
// 1개 (accumulator)  
Optional<T> reduce(BinaryOperator<T> accumulator);  
  
// 2개 (identity)  
T reduce(T identity, BinaryOperator<T> accumulator);  
  
// 3개 (combiner)  
<U> U reduce(U identity,  
 BiFunction<U, ? super T, U> accumulator,  
 BinaryOperator<U> combiner);
```

#### 예
``` java
// 인자 1개
OptionalInt reduced =   
	IntStream.range(1, 4) // [1, 2, 3]  
	.reduce((a, b) -> {
	return Integer.sum(a, b); 
	});

// 인자 2개
int reducedTwoParams = IntStream.range(1, 4) // [1, 2, 3]
	.reduce(10, Integer::sum); // method reference
```

* Combiner 는 병렬 처리 시 각자 다른 쓰레드에서 실행한 결과를 마지막에 합치는 단계
* 따라서 병렬 스트림에서만 동작함

``` java
// 인자 3개
Integer reducedParallel = Arrays.asList(1, 2, 3)  
	.parallelStream()  
	.reduce(
		10, Integer::sum,  
		(a, b) -> {  
			System.out.println("combiner was called");  
			return a + b;  
		});
```

<br>

## 3-3) Collecting

#### 예
``` java
List<Product> productList =  Arrays.asList(
	new Product(23, "potatoes"),  
	new Product(14, "orange"),  
	new Product(13, "lemon"),  
	new Product(23, "bread"),  
	new Product(13, "sugar")
	);
```

- **Collectors.toList()**
	- * 스트림에서 작업한 결과를 담은 리스트로 반환
	``` java
	List<String> collectorCollection =  
	 productList.stream()  
	 .map(Product::getName)  
	 .collect(Collectors.toList());  
	// [potatoes, orange, lemon, bread, sugar]
	```

- **Collectors.joining()**
	* 하나의 String으로 이어붙임
	* 인자
		-   delimiter : 각 요소 중간에 들어가 요소를 구분시켜주는 구분자
		-   prefix : 결과 맨 앞에 붙는 문자
		-   suffix : 결과 맨 뒤에 붙는 문자
	``` java
	String listToString = productList.stream()  
		.map(Product::getName)  
		.collect(Collectors.joining());  
	// potatoesorangelemonbreadsugar
	```

- **Collectors.averageingInt()**:  숫자 값(_Integer value_ )의 평균(_arithmetic mean_)
	``` java
	Double averageAmount = productList.stream()  
		.collect(Collectors.averagingInt(Product::getAmount));  
	// 17.2
	```

- **Collectors.summingInt()**: 숫자값의 합(_sum_)
	``` java
	Integer summingAmount =   productList.stream()
		.collect(Collectors.summingInt(Product::getAmount));  
	// 86
	```
	- `mapToInt` 메소드를 사용해서 좀 더 간단하게 표현 가능
	``` java
	Integer summingAmount =  productList.stream()  
		.mapToInt(Product::getAmount)  
		.sum(); // 86
	```
- **Collectors.summarizingInt()**: 합계와 평균 모두
	``` java
	IntSummaryStatistics statistics =  productList.stream()
		.collect(Collectors.summarizingInt(Product::getAmount));
	```
	-   개수  _getCount()_
	-   합계  _getSum()_
	-   평균  _getAverage()_
	-   최소  _getMin()_
	-   최대  _getMax()_

- **Collectors.groupingBy()**: 그룹핑
	- 결과는 Map타입
	``` java
	Map<Integer, List<Product>> collectorMapOfLists = productList.stream()  
		.collect(Collectors.groupingBy(Product::getAmount));
	```
	- 같은 수량이면 리스트로 묶어서 보여줌
	``` java
	{
		23=[Product{amount=23, name='potatoes'},   
		Product{amount=23, name='bread'}],   
		13=[Product{amount=13, name='lemon'},Product{amount=13, name='sugar'}],   
		14=[Product{amount=14, name='orange'}]
	}
	```
- **Collectors.partitioningBy()**
	``` java
	Map<Boolean, List<Product>> mapPartitioned =  productList
		.stream()  
		.collect(Collectors.partitioningBy(el -> el.getAmount() > 15));
	```
	- 결과
	``` java
	{
		false=[Product{amount=14, name='orange'},   
		Product{amount=13, name='lemon'},   
		Product{amount=13, name='sugar'}],   
		true=[Product{amount=23, name='potatoes'},   
		Product{amount=23, name='bread'}]
	}
	```
- **Collectors.collectingAndThen()**
	- 특정 타입으로 결과를 `collect` 한 이후에 추가 작업이 필요한 경우에 사용
	- `finisher` : collect 를 한 후에 실행할 작업을 의미
	``` java
	public static<T,A,R,RR> Collector<T,A,RR> collectingAndThen(
			Collector<T,A,R> downstream,
			Function<R,RR> finisher
		) { ... }
	```
	- 예
		- 결과를 Set 으로 collect 한 후 수정불가한 Set 으로 변환하는 작업을 추가로 실행
	``` java
	Set<Product> unmodifiableSet =  productList.stream()
		.collect(Collectors.collectingAndThen(
			Collectors.toSet(), 
			Collections::unmodifiableSet)
		);
	```
- **Collector.of()**
	- 직접 collector 를 만들 수도 있음
	- 예
	``` java
	Collector<Product, ?, LinkedList<Product>> toLinkedList =   Collector.of(
		LinkedList::new,  
		LinkedList::add,   
		(first, second) -> {  
			first.addAll(second);
			return first;
		});
	```
	- 결과가 담긴 `LinkedList` 가 반환됨




<br>

## 3-4) Matching
조건식 람다 Predicate 를 받아서 해당 조건을 만족하는 요소가 있는지 체크한 결과를 리턴

#### 메소드
-   하나라도 조건을 만족하는 요소가 있는지(_anyMatch_)
-   모두 조건을 만족하는지(_allMatch_)
-   모두 조건을 만족하지 않는지(_noneMatch_)

#### 예
``` java
List<String> names = Arrays.asList("Eric", "Elena", "Java");  
  
boolean anyMatch = names.stream()
	.anyMatch(name -> name.contains("a"));  
boolean allMatch = names.stream()  
	.allMatch(name -> name.length() > 3);  
boolean noneMatch = names.stream()  
	.noneMatch(name -> name.endsWith("s"));
```

<br>

## 3-5) Iterating
- `foreach` 는 요소를 돌면서 실행되는 최종 작업
- 보통 `System.out.println` 메소드를 넘겨서 결과를 출력할 때 사용
- `peek` 과의 차이: 중간 작업과 최종 작업의 차이

#### 예
``` java
names.stream().forEach(System.out::println);
```

<br><br><br><br>

### 참고
-  https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html
-  https://futurecreator.github.io/2018/08/26/java-8-streams/
-  [Introduction to Java 8 Streams](https://www.baeldung.com/java-8-streams-introduction)
-  [The Java 8 Stream API Tutorial](http://www.baeldung.com/java-streams)
-  [Java Null-Safe Streams from Collections](https://www.baeldung.com/java-null-safe-streams-from-collections)
-  [도서 <열혈 Java 프로그래밍>](http://www.kyobobook.co.kr/search/SearchCommonMain.jsp)

