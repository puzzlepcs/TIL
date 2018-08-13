# Collection API
java.util 패키지에 정의되어 있으며, 자료구조와 관련된 클래스들를 지원한다.  
객체들을 저장, 검색, 삭제하는 기능 등을 제공하는 클래스들의 집합이다.
- Collection: 모든 클래스들의 Object를 요소(element)로 저장하는 객체의 최상위 Interface

## 1. Set

## 2. List

## 3. Map
객체를 key와 value로 구분한다.

## 5. Calendar
날짜와 시간에 관한 정보를 표현할 때 사용한다.
* Calendar 클래스는 추상 클래스이므로 객체를 생성할 수 없다. getInstance() 메소드를 사용하여 시스템의 날짜와 시간정보를 표현할 수 있다.
* month는 0~11까지의 숫자를 지정해주기 때문에 달을 사용하고자 하면 1을 더해주어야 한다.

### 5.1 참고-객체의 수를 제한하기
생성자를 static 함수로 지정해주면 객체가 단 한개 생성된 것과 같은 기능을 한다. 메인 함수에서 새롭게 객체를 생성하는 대신, 메소드를 사용해 생성된 단 한개의 객체를 반환하여 사용한다. 다음은 Java에서 `Calendar` 클래스와 같은 방식을 사용한 예제이다.
```
class Cal {
	private static Cal c = new Cal();
	public static Cal getInstance() {
		return c;
	}
	private Cal() {
	}
}
```

## 4. Iterator
Collection 계열의 클래스들은 iterator()메소드를 사용하여 객체들을 조회할 수 있다.
* 인터페이스로, Iterator.class라는 파일에 구현되어 있다.
  * `public interface iterator<E> {...}`
* `hasnext()`, `next()` 메소드로 다음 객체를 알아낼 수 있다.

### for each
iterator를 생성한 뒤 다시 조회하고 싶으면 다시 iterator를 생성해야 하는 번거로움이 있다. for each문을 활용하면 이러한 번거로움을 피할 수 있다.

## 5. Generic: 한가지 타입만을 저장하기
```
  HashSet<String> set = new HashSet();
  // set에는 String 타입만 저장할 수 있다.

  // iterator또한 한가지 타입으로 지정해 줄 수 있다.
  Iterator<String> iterator = set.iterator();
  while(iterator.hasNext()) {
    /* ... */
  }
```
이렇게 생성된 Collection 객체의 경우 한가지 자료형만을 저장하는 객체가 생성된다.
