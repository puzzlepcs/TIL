# 자료형 Datatype
## Primitive DT
크기와 종류가 정해져 있는 타입.
### 종류
* 숫자형
  * 정수
    * byte형 - 1byte(8bit)
    * short형 - 2byte(16bit)
    * int형 - 4byte(32bit), 기본 정수타입. 모든 연산의 결과는 int형이 된다.
    * long형 - 8byte(64bit), long형 데이터를 주기 위해 값 뒤에 l또는 L로 사용한다.
  * 실수
    * float형 - 4byte, float형 데이터를 주기 위해 값 뒤에 f또는 F를 사용한다.
    * double형 - 8byte
  * 문자형 - 숫자. '' 표시. (문자열 String과는 다름. ""로 표시)
    * char - 2byte, Java에서는 기본적으로 Unicode처리.
  * 논리형
    * boolean - 1byte
### 형변환
형변환은 크게 두가지가 있다. (큰 타입에서 작은 타입으로, 작은 타입에서 큰 타입으로 변환)
다음 순서와 같이 크기를 생각하면 된다.  

> (작음) <- byte - char,short - int -long -float - double -> (큼)  

* Atomatic promitions (Implicit Type Casting)
  * 작은 자료형에서 큰 자료형으로 캐스팅 하는 것은 생략이 가능함.  
* Explicit Type Casting (명시적 캐스팅)
  * 큰 자료형에서 작은 자료형으로 변환하고자 할 때에는 명시적으로 캐스팅을 해주어야 한다.
  * 큰 자료형에서 작은 자료형으로 변환할 때에는 그 값이 변형될 수 있으므로 주의해야 한다.
  * 형변환 기호 생략 불가.  

#### Java에서 정수형과 실수형 타입
실수를 정수로 변환할 때에 꼭 명시적 형변환을 해주어야 한다.  
long타입은 8바이트이고, float타입은 4바이트 이므로 실질적으로 long타입이 더 크다고 할 수 있지만, Java에서 정수형이 실수형보다 작기 때문에 이 부분에서 주의를 기울여야 한다.

#### 참고
String타입과 int형을 '+'로 연결해주면 String 타입으로 변환된다.
```
  String s = "Hello";
  System.out.println(s + 4 + 5);
  System.out.println(4 + 5 + s);
  // 각각 Hello45와 9Hello가 출력된다.
```

===

## Reference DT
유저가 정의하는 데이터 타입. (User define DT)
* Array
* Class
* Interface
