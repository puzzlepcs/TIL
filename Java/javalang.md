# java.lang
Java언어의 가장 기본적인 클래스들을 모아놓은 패키지
## 1. Object
- java.lang.Object클래스는 최상위 클래스
- 모든 클래스가 기본적으로 상속받아야 하기 때문에 특별히 `extends Object`를 사용하지 않아도 컴파일러에 의해서 상속되어 진다.
- Object클래스에는 모든 클래스의 공통적인 기능을 정의하고, 자주 사용되는 메소드를 정의하여 필요시 Overriding해서 사용하도록 권장한다.
### 1.1 Object의 주요 메소드
- `toString()`
   - String 반환
   - 객체를 ㅐㄷ표하는 문자열을 return
- `hascode()`
  - int 반환
  - 객체를 구분하는 코드값을 리턴
- `eqauls()`
  - boolean 반환
  - 객체의 내용을 비교할 수 있도록 구현
- `finalize()`
  - GC에게 메모리 종료를 요청.
  - GC가 즉시 메모리를 정리하는 것은 보장하지 못함

### 1.2 예제
```
// Customer.java
public class Customer {
	String name;
	int age;
	Customer() {
		System.out.println("hello this is customer");
	}

	@Override
	protected void finalize() throws Throwable {
		super.finalize();
		System.out.println("Customer.finalize() called");
	}
}
```
```
// FinalizeTest.java
public class FinalizeTest {
	public static void main(String[] args) {
		System.out.println("Main Start.....");
		FinalizeTest f = new FinalizeTest();
		f.printCus();
		System.gc();
		System.out.println("Main End.....");
	}

	void printCus() {
		Customer c = new Customer();
	}
}
```
## 2. String
### 2.1 특징
문자열을 간단히 저장할 수 있는 클래스로 + 연산자가 오버로딩되어 있어 더하기 연산이 가능하다.  
- 유일하게 new를 사용하지 않고도 객체 생성 가능
  ```
    String s = new String("ABC");
    String s2 = "ABC";
  ```
- 어떤 type이던 String객체에 + 를하게 되면 문자열로 변환되어 결과값이 모두 String으로 변환됨
  ```
    String s1 = "aaa" + "b";
    String s2 = 32 + "a";
    String s3 = 3.4 + "232";
  ```
  - 유일하게 연산자 오버로딩이 허용된 클래스이다.
  - Java에서는 연산자 오버로딩이 불가능하다. 그러나 String은 +가 재정의 되어 있어 다양한 클래스를 이용한 연산이 가능하다.

### 2.2 주요 메소드
- `concat(String s)`, `replace(char old, char new)`, `charAt(int idx)`
- `substring()`
- `endsWith(String s)`, `startsWith(String s)`
- `indexOf(char a)`, `indexOf(String s)`, `indexOf(String s, int offset)`
- `equals(String a)`, `equlasIgnoreCase(String s)`, `compareTo(String s)`
- `length()`
  - String클래스의 경우 길이가 가변적이기 때문에 멤버변수가 아닌 메소드로 그 길이를 조회한다.

### 2.3 String 객체 생성과 문자열 literal
String에서 == 와 eqaul() 는 왜 다르게 작용할까? String 객체와 문자열 literal이 메모리상에 어떻게 존재하는지 알면 이를 이해할 수 있다.
[string.md](https://github.com/puzzlepcs/TIL/blob/master/Java/string.md)

### 2.4 String의 단점을 보완한 StringBuilder
String 클래스는 편집시에 처리가 느리다는 단점이 있다. 이런 단점을 보완한 클래스가 StringBuilder, StringBuffer이다.
- StringBuilder와 StringBuffer의 기능은 비슷하나, StringBuilder가 성능이 더 좋다.  
```
public class StringTest {
  public static void main(String[] args) {
    double start = System.currentTimeMillis();
    String s = new String();
    for(int i = 0; i < 100000; i++) {
      s += "a";
    }
    double end = System.currentTimeMillis();
    System.out.println("Execute Time: " + (end-start));

    start = System.currentTimeMillis();
    StringBuilder sb = new StringBuilder();
    for(int i = 0; i < 100000; i++) {
      sb.append("a");
    }
    end = System.currentTimeMillis();
    System.out.println("Execute Time: " + (end-start));
  }
}
/*
* ****출력화면*****
* Execute Time: 812508.0
* Execute Time: 10.0
*/
```

## 3. Math class
Math 클래스는 흔히 계산을 하는데 도움이 되는 많은 수의 기본적 수학 함수들과 상수들을 제공한다.  
Math 클래스의 모든 메소드들은 정적 메소드(static method)로 **클래스의 객체를 생성하지 않고 그 메소드가 정의된 클래스 이름을 통해서 호출될 수 있다.**  

### 3.1 Math 클래스 필드
Math.E와 Math.PI는 Math 클래스에 정의되어 있는 클래스 필드로, 각각 오일러 수, 원주율 값이다.

### 3.2 Math 클래스 주요 메소드
- random() : 난수 발생
- abs() : 절댓값
- floor(), ceil(), round() : 올림, 내림, 반올림
- max(), min(): 전달 된 두 값중 큰 값, 작은값을 반환
- pow(), sqrt(): 제곱연산, 제곱근 반환
- sin(), cos(), tan()
- toDegrees(), toRadians()

## 4. Wrapper class
Java의 자료형은 기본형(primitive type), 참조형(reference type)으로 나뉜다. Wrapper 클래스는 참조형 타입으로, Java의 Primitive type을 객체화 시키는 클래스들이다.  

### 4.1 Wapper 클래스 종류
기본형 | Wrapper class | 생성자
-----|-----|------
boolean|Boolean|Boolean(boolean value), Boolean(String s)
char|Character|Character(char value)
byte|Byte|Byte(byte value), Byte(String s)
short|Short|Short(short vlaue), Short(String s)
int|Integer|Integer(int value), Integer(String s)
long|Long|Long(long value), Long(String s)
float|Float|Float(double value), Float(float value), Float(String s)
double|Double|Double(double value), Double(String)  


Boolean, Character, Number 모두 Object의 자손이며 모든 숫자와 관련된 Wrapper 클래스는 Number의 자손이다.

### 4.2 Wrapper 클래스의 용도
Wrapper 클래스는 주로 다음과 같은 상황에서 사용된다.
1. 매개변수로 객체가 요구될 때
2. 기본형 값이 아닌 객체로 저장해야 할 때
3. 객체간의 비교가 필요할 때  

### 4.3 Wrapper 클래스 구조
Wrapper 클래스는 기본형 변수를 객체로 감싸서 사용할 수 있게끔 작성되어 있다. 실제로 Integer 클래스의 코드는 다음과 같다.
```
public final class Integer extends Number implements Comparable {
  ...
  private int value;
  ...
}
```  


또한 Wrapper 클래스들은 모두 `equals()` 메소드가 오버라이딩 되어 있어 주소 값이 아닌 객체의 값을 가지고 비교한다.  
그밖에도 MAX_VALUE, MIN_VALUE, SIZE, TYPE등의 static 멤버를 공통적으로 가지고 있다.

### 4.4 Integer.parseInt("100") vs Integer.valueOf("100")
parse 메소드는 기본형을 반환하지만, valueOf는 Wrapper 클래스를 반환한다.

정리하자면  
String -> primitive type | String -> Wrapper class  
------|------
byte b = Byte.parseByte("100");|Byte b = Byte.valueOf("100");
short s = Short.parseShort("100");|Short s = Short.valueOf("100");
int i = Integer.parseInt("100");|Integer i = Integer.valueOf("100");
long l = Long.parseLong("100");|Long l = Long.valueOf("100");
float f = Float.parseFloat("100");|Float f = Float.valueOf("100");
double d = Double.parseDouble("100");|Double d = Double.valueOf("100");  


JDK 1.5 부터 도입되어 지원되는 autoboxing과 unboxing 때문에 반환값이 기본형일 때와 Wrapper 클래스일 때의 차이가 사라졌다. 현재 valueOf() 메소드를 사용해도 아무 문제가 없지만, 성능을 비교하자면 valueOf() 메소드가 조금 더 느리다.  
