# class와 object, Abstraction
## 1. Overview
참조 데이터 타입.
## 2. class구성과 object의 사용법
### 2.1 클래스 정의 (class design)
class는 다음과 같이 정의한다.
```
  [modifiers] class className {
    // 클래스의 속성인 attribute
    [modifiers] dataType attributeName;

    // 클래스 생성자
    [modifier] className([arguments]) {
      ...
    }

    // 클래스의 기능인 method
    [modifiers] returnType methodName([arguments]) // 선언부
    {  
      // 구현부
      ...
    }
  }
```
### 2.2 객체생성
정의된 class를 사용하여 객체를 만들기 위해서 new 키워드를 사용해야 한다. 만들어진 object는 메모리상에 존재하게 된다. (따라서 객체를 생성하기 위해서는 충분한 메모리가 있어야 한다. instance는 메모리가 허용하는 한 무수히 많이 생성할 수 있다.)
```
  className instanceName = new className();
```

## 3. 클래스와 메모리영역
### 3.1 JVM 메모리구조
JVM은 구현한 벤더마다, 버전마다 메모리 관리 기법이 다르고, GC의 관리 방법또한 다르다. 개략적으로 살펴보면 아래와 같이 클래스를 로딩하여 저장하는 공간(Class Area), 객체를 생성하는 공간(Heap), 프로그램 수행시 로컬변수가 중간 결과를 저장하는 공간(Stack)으로 구분할 수 있다.

* **Heap area** : instance가 저장되는 메모리 공간. 객체가 만들어지는 영역
  * 이 영역에서 객체를 생성하고 JVM이 객체의 고유의 Hashcode값을 사용하여 넘버링한다.
  * 위의 예제의 경우 `new Customer()`를 실행할 경우, 이 영역에 그 클래스의 정보가 저장된다.
  * GC가 사용이 종료된 객체의 메모리를 정리해 준다.
* **Stack area** : 프로그램이 실행되는 영역. 메소드가 수행되는 공간.
  * 메소드마다 하나의 프레임 이 생성됨. 프레임은 해당 메소드의 코드가 모두 실행되면 사라진다.
  * 메소드의 instance에서 heap에서 생성된 hashcode가 저장된다. 즉, Stack 영역에 그 인스턴스의 정보가 저장되어있는 것이 아니라, 저장되어 있는 곳을 의미하는 값이 저장되어 있는 것이다.
    * 이러한 이유로 클래스를 **레퍼런스 타입** 이라고도 부른다.
  * 스택구조를 사용한다.
* **Class area**
  * Class에 관련된 정보를 Class Loader가 이 영역에 로드한다.
  * Method area, Static area등 다양한 영역이 이 영역에 속한다.

### 3.2 클래스 생성 과정
JVM은 `Customer c = new Customer(); ` 라는 코드를 만나는 순간에 `Customer`라는 클래스 타입을 Class area에 **Dynamic Load** 한다. (캐싱되어 있는 경우 로드 되어 있는 정보를 사용한다.)
그 다음 'Customer.Class' 라는 바이트코드의 Customer라는 클래스가 유효한지 확인하는 **Verify** 과정을 거친다. (이미 로드되어 있는 경우에는 이 과정을 생략할 수 있다. 보안 문제 때문에 다시 검증하기도 한다.)
그리고 `Static` 키워드를 사용한 함수들과 변수들을 **Static 메모리 영역에** 올려준다. Static 키워드를 사용한 함수 중에 **Main()함수를** 찾는다. (Main함수가 없다면 세번째 단계, Static 키워드가 사용되지 않았다면 두번째 단계에서 종료)

정리하면 다음의 4단계를 거친다고 생각하면 된다.

> Dynamic Load -> Verify -> Static -> Main

### 3.3 Garbage Collector
Java는 메모리 관리를 개발자에게 위임하지 않고, GC(Garbage Collector)를 두어 Heap영역의 메모리를 관리하도록 한다. GC는 Heap영역의 객체 생성시 만들어지는 counter를 확인하여 객체 카운터가 0가 되는 순간 메모리를 정리한다. 자동적으로 실행되며, CPU가 한가하거나 메모리가 부족할 떄 JVM에 의해 실행된다.
`System.gc()`를 호출하여 실행을 유도할 수 있지만 바로 수행된다는 보장은 없다.
JVM에 따라 다양하게 구현, 실행되며 성능에 영향을 주기 때문에 Java version에 따라 더 좋은 성능의 GC 기법을 사용한다.

## 4. Constructor
### 4.1 개념
**객체의 초기화** 를 위한 호출부가 없는, 즉 객체가 만들어질 때 자동호출되는 특별한 메소드이다. 이 때문에 이 메소드의 이름은 반드시 클래스의 이름과 동일해야 하며, 아무것도 리턴하지 않는 void함수이여야 한다.
class내의 constructor가 하나도 정의되어 있지 않는 경우 컴파일 할 때 컴파일러가 **default constructor** 를 생성, 사용한다.
생성자가 정의되어 있는 경우 default constructor를 삽입하지 않기 때문에, 생성자를 정의할 때 기본 생성자도 같이 정의를 해주는 것이 바람직하다.
### 4.2 Constructor Overloading
Java에서 Polymorphism을 지원하는 방법으로 Method overloading을 제공한다. 오버로딩은 같은 이름의 메소드를 여러개 가지면서 Argument의 유형과 개수가 다르도록 하는 기술이다.

오버로딩은 컴파일시 컴파일러가 argument의 갯수와 타입에 따라 메소드의 이름을 다시 지정해주는 식으로 구현된다. 예를 들어 `Customer(int, int, int)`의 경우 `Customer_I_I_I`로 변환해주고, `Customer(float, int, int)`의 경우 `Customer_F_I_I`로 변환한다.

(참고: [Overloading](https://www.techopedia.com/definition/3236/overloading) )
생성자도 메소드의 하나이므로, 여러가지 경우의 생성자를 정의할 수 있다.

### 4.3 참고 - Java에서의 Destructor?
Java의 경우 자동으로 메모리가 정리되므로, Destructor가 없다.
finalize 함수로 메모리를 정리하는 기능이 있으나 기본적으로 GC가 사용하는 방법으로 메모리를 정리해 준다.
[GC와 memory leak](https://stackoverflow.com/questions/171952/is-there-a-destructor-for-java)
