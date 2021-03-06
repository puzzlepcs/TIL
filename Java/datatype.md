# 자료형 Datatype
Java에서 자료형은 Primitive Type과 Reference Type, 크게 두가지로 나눌 수있다.

## 1. Primitive DT
컴파일러가 미리 만들어놓은 자료형. 크기와 종류가 정해져 있는 타입.
### 1.1 종류
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

### 1.2 형변환 (Type Casting)
형변환은 크게 두가지가 있다. (큰 타입에서 작은 타입으로, 작은 타입에서 큰 타입으로 변환)
다음 순서와 같이 크기를 생각하면 된다.  

> *(작음)* <- **byte - char,short - int - long - float - double** -> *(큼)*  

* Implicit Type Casting
  * 작은 자료형에서 큰 자료형으로 캐스팅 하는 것은 생략이 가능함.
  * 자료의 변형이 일어나지 않음.  
* Explicit Type Casting (명시적 캐스팅)
  * 큰 자료형에서 작은 자료형으로 변환하고자 할 때에는 명시적으로 캐스팅을 해주어야 한다.
  * 큰 자료형에서 작은 자료형으로 변환할 때에는 그 값이 변형될 수 있으므로 주의해야 한다.
  * 형변환 기호 생략 불가.  

#### 1.2.1 Java에서 정수형과 실수형 타입
실수를 정수로 변환할 때에 꼭 명시적 형변환을 해주어야 한다.  
long타입은 8바이트이고, float타입은 4바이트 이므로 실질적으로 long타입이 더 크다고 할 수 있지만, Java에서 정수형이 실수형보다 작기 때문에 이 부분에서 주의를 기울여야 한다.  
#### 1.2.2 참고
String타입뒤에 '+'로 연결해주면 어느 타입이던 String 타입으로 변환된다.
```
  String s = "Hello";
  System.out.println(s + 4 + 5);  //(1) Hello45
  System.out.println(4 + 5 + s);  //(2) 9Hello
  // 연산이 왼쪽에서 오른쪽으로 진행되기 때문에,
  // (1)의 경우 4와 5가 String으로 변환되고,
  // (2)의 경우 9로 계산된 결과가 형변환된다.

  String st4 = 'a'+10+"seoul";
	System.out.println(st4);       //(3) 107seoul
	String st5 = "seoul"+'a'+10;
	System.out.println(st5);       //(4) seoula10
  // (3)의 경우 'a'가 97값을 갖기 때문에 97+10이 연산된후 형변환된다.
  // (4)의 경우 모두 String으로 형변환되어 join된다.

```

## 2. Reference DT
참조형 데이터타입이라는 뜻이다. 유저가 정의하는 데이터 타입(User define DT)으로 array, class, interface가 있다.
참조형 데이터 타입은 선언되면 heap영역에 객체가 생성되며 stack영역에는 heap영역의 주소값이 저장된다.  
메소드에서 참조타입을 인자로 넘기거나 리턴값을 받을 때 값이 복사되는 Primitive 타입과 달리, 참조타입에서는 주소값이 넘어가기 때문에 이에 유의해야 한다.
### 2.1 Class
class는 객체의 설계도라고 생각하면 된다. class는 프로그램 내에서 직접 사용되는 것이 아니다. 반면 class를 이용해 생성된 object는 메모리 상에 존재한다.
즉, object는 class의 dynamic instance이고, class는 object의 blueprint이다.
class를 구성하는 속성들과 메소드를 정의하고 설계하는 것을 클래스 모델링이라고 한다.  

참고: [class.md](https://github.com/puzzlepcs/TIL/blob/master/Java/class.md)

### 2.2 Array
#### 2.2.1 Array Overview
대량의 데이터를 하나의 이름으로 저장하여 편리하게 사용하고 이동하기 위해 배열을 사용한다. 선행적인 데이터를 저장하기 위해 1차원 배열을 사용할 수 있다.  
*Java에서 배열은 Object이다.* 그러므로 Object를 생성하여 사용하듯이 배열도 객체 생성하여 사용하여야 한다.  

#### 2.2.2 정의
같은 데이터 타입의 순서적 나열
#### 2.2.3 특성
**선언과 동시에 크기가 결정 되고 그 크기는 변경될 수 없다.** 자료구조 중에 가장 접근이 빠르다. (인덱스로 데이터로 접근한다.)
#### 2.2.4 배열의 생성
배열은 다음과 같이 선언한다. 객체가 만들어지는 동시에 크기가 결정되어야 한다.
```
  DataType[] arrayName;
  arrayName = new DataType[arraySize];

  DataType arrayName[];     // 이렇게 선언하는 것도 허용한다.

```
Java는 C언어와의 호환성을 위해서 C언어의 문법과 비슷한 문법을 갖는다. 변수 선언과 생성, 값할당을 동시에 처리할 수 있다.
```
  int[] iarr1 = new int[] {1,3,5,7,9};
  int[] iarr2 = {1,3,5,7,9};
  Member[] cu = {new Member(),new Member(),new Member(),new Member()};  
```
마지막 경우와 같이 참조타입의 배열을 만드는 경우 배열의 원소인 객체를 만들 생성하기 전 그 객체에 접근하게 되면 NullPointerException 오류가 발생한다. 배열을 만들고 꼭 그 안의 객체를 생성하여야 한다. (맴버 객체의 개열의 객체화와 맴버 객체화 구분하기)

#### 2.2.5 주요 메소드, 속성
* **foreach** 문: 배열의 값 처리시에 기존의 for문보다 편리하고 빠르게 처리할 수 있다.
  ```
    for(int s: su) {
      System.out.println(s);
    }
  ```
* 배열의 길이를 나타내는 속성 length를 `arrayName.length`을 통해 조회 가능하다.
  * 배열의 길이를 메소드를 사용하지 않고 변수로 조회하는 이유
    * 메소드는 주로 가변적인 값을 조회하는데 사용. 배열의 경우 길이는 만들어질 때 생성되며 변하지 않는 값이다.
    * 변수로 값을 조회하는 것이 메소드를 사용하는 것 보다 빠르기 때문에 변하지 않는 속성값을 받고자 하면 변수를 이용하는 것이 좋다.

#### 2.2.6 배열의 복사 - 깊은 복사
```
public class ArrayTest5 {
	public static void main(String[] args) {
		int[] arr1 = {1,3,5,7,9};
		int[] arr2 = new int[5];

		arr2 = arr1;
		arr1[0] = 100;

		System.out.println("arr1");
		for (int i : arr1) {
			System.out.print(i+", ");
		}
		System.out.println();

		System.out.println("arr2");
		for (int i : arr2) {
			System.out.print(i+", ");
		}

/*
*    ****결과값****
*    arr1
*    100, 3, 5, 7, 9,
*    arr2
*    100, 3, 5, 7, 9,
*/
	}
}
```
배열은 참조타입이므로 `arr1 = arr2`처럼 복사시 그 값이 복사되는 것이 아니라, heap영역의 hashcode가 복사되어 같은 객체를 가리키게 된다. Primitive type의 경우 값이 복사(C에서의 얕은 복사)되지만 Reference Type의 경우 그 주소값이 복사되기 때문에 같은 객체를 가리킨다(C에서의 깊은 복사).

따라서 위의 코드에서 값을 복사하고자 한다면 for문을 사용하거나, `System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length)`메소드를 사용하면 된다.
```
for (int i = 0; i < arr2.length; i++) {
			arr1[i] = arr2[i];
		}
```
혹은
```
  System.arraycopy(arr1, 0 ,arr2, 0, arr1.length);
```

### 2.3 Interface
인터페이스는 상수와 구현되지 않은 메소드로만 구성된다. 상수 정의시에 특별히 상수라고 명시하지 않아도 컴파일러에 의해서 상수로 변경된다.(컴파일시 public static final 제한자가 자동으로 변수 앞에 붙는다.) 또한 메소드 정의시에 public하게 정의하지 않아도 인터페이스의 모든 메서드는 컴파일러가 public제한자를 삽입한다. (컴파일시 public abstract 제한자가 메소드 앞에 붙는다.)  
따라서 인터페이스는 객체화되지 않는 자료형이다.
* 특별히 정의하지 않아도 컴파일 시에 아래 제한자가 추가된다.
  - `public static final` 제한자가 상수 앞에 붙는다.
    - 따라서 변수의 사용이 불가능하다.
  - `public abstract` 제한자가 메소드 앞에 붙는다.  
    - 따라서 **메서드 오버라이딩 시 항상 public 제한자** 가 필요하다.  

#### 2.3.1 Interface의 특징
- 인터페이스는 객체 생성을 할 수 없다. 구현되지 않은 메소드를 포함하기 때문이다.
- super type으로 사용할 수 있다.
  - 설계의 지침으로 사용된다.
  - 다양한 클래스를 기능으로 묶어줄 수 있다.
  - 추상 클래스와 유사한 기능
- 상속되어져서 sub class가 모든 메소드를 구현(Overriding)해야한다.
- 상속한 sub class들의 *명세서 역할* 로 사용한다.
- polymorphism 효과

#### 2.3.2 `implement` 키워드, 다중상속과 Upcasting
* `extends`와는 다르므로 어떤 클래스를 상속받은 Sub class여도 interface를 사용할 수 있다.
* 다중상속이 가능하다.
  * 여러개의 interface를 implement한 경우 모든 interface의 method를 구현해주어야 한다.
  * 다중상속이 가능하기 때문에 polymorphism 효과가 나타난다.
  * 여러가지의 Upcasting이 가능하다. (Sub class가 Super class 혹은 Interface로 Upcasting이 가능하다.)
* 아무 기능도 구현하지 않는 Mark Interface
  * 쿠폰의 용도: 이 기능에서 사용할 수 있는가?
  * 다양한 종류의 클래스들을 묶어서 Mark Interface로 upcasting하여 사용한다.
  * 어떠한 기능을 수행해야 하는 클래스들을 묶어서 사용한다.


### 2.4 그밖에...
#### 2.4.1 class vs interface
* 계층적 구조 -> class와 상속로 구현
* 기능 위주 -> interface로 구현
#### 2.4.2 기타
- Java에서 문자열 String은 Primitive Type이 아니라, Reference Type이다.
- 리턴 타입 void는 아무것도 리턴하지 않는다는 의미. 구현부 내에 `return;`을 적어주어야 하나, 이는 의미없는 구문으로 간주되어 대게 생략된다.
