# Modifier와 Encapsulation(은닉화)
## 1. Modifier Overview
Modifier는 크게 use modifier와 Access modifier로 나눌 수 있다.
- use modifier
  - static: member variable, member method, member nested class
  - final: class, varaible, method
  - abstract: class, method
- Access modifier
  - public
  - protected
  - private

## 2. static
모든 것을 객체지향으로 구현하는 Java에서 편의성을 위해서 객체 생성 없이도 메소드, 변수, 클래스에 접근 할 수 있게끔 해주는 키워드이다.  
static 제한자는 member variable, member method, member nested class에 사용할 수 있다. 전체를 구성하는 외부 클래스(outer class)에는 static을 사용할 수 없다.   
static 키워드를 붙인 멤버변수, 멤버메소드, 멤버 클래스는 컴파일시 메모리의 static 영역에 로드된다. 따라서 힙 영역에 인스턴스를 생성하지 않아도 접근가능하다.  
static영역은 클래스 영역(constance memory)영역의 일종으로, 힙 영역과는 달리 메모리의 크기가 한정적이고 가변적이지 않다. 스태틱 영역에 로드된 클래스의 정보들은 프로그램 종료 때까지 계속 존재한다. 이 때문에 static을 과도하게 사용하게 되면 오류가 발생 할 수 있다.  

Java에서 기본적으로 제공하는 클래스 중 Math는 static class이다.
```
  // Math m = new Math();             // Static class이므로 인스턴스를 생성하지 않고도 사용할 수 있다.
  System.out.println(Math.sin(1.34));
  System.out.println(Math.PI);
```
### 2.1 member variable에서의 static
static변수는 객체간 공유되는 값이다. 인스턴스를 생성하지 않고도 접근할 수 있어서 클래스변수라고도 한다.
객체 생성을 하지 않고도 클래스 이름을 사용해 `className.staticVarName`로 직접 접근이 가능하다.

#### 2.1.1 예제
```
class StaticVarTest {
  static int count = 0;     // static member variable
  int b;                    // member variable (instance variable)
  void run() {
    int num;                // local variable (메소드가 끝나면 사라짐)
    num++;
    b++;
    count++
  }
  public static void main(String[] args) {
    System.out.println("StaticVarTest.count="+StaticVarTest.count);
    StaticVarTest a1 = new StaticVarTest();
    StaticVarTest a2 = new StaticVarTest();
    a1.run();
    a2.run();
    a1.b +=100;
    a1.count += 100;
    System.out.println("a1.count="+a1.count+" b="+a1.b);
    System.out.println("a2.count="+a2.count+" b="+a2.b);
    System.out.println("StaticVarTest.count="+StaticVarTest.count);
  }
}
/** 출력화면
*    StaticVarTest.count=0
*    count=1	b=1	num=1
*    count=2	b=1	num=1
*    a1.count=102 b=101
*    a2.count=102 b=1
*    StaticVarTest.count=102
*/
```

### 2.2 member method에서의 static
객체생성을 하지 않고도 `className.staticMethodName()`로 메소드를 사용할 수 있다.

#### 2.2.1 static 메소드 사용시 주의점
static 변수 안에서는 일반 클래스 변수와 클래스 메소드를 사용하면 안된다. 일반 변수와 메소드는 객체 생성 후에 사용가능하기 때문에 static method 내에서는 static variable과 static method만 사용해야 한다.
```
class StaticTest {
  int a;
  static int count
  static void set(int k){
    // a = k;       // static method내에서 일반 인스턴스 변수를 사용하면 안된다.
    count = k;        
  }
}
```

### 2.3 member nested class에서의 static
member nested class는 클래스 내부에서 사용하는 클래스로, 클래스 내부에서 인스턴스를 생성하여 그 기능을 사용한다. 클래스 내부에서만 사용할 수 있다. 이때, 외부에서 nested class의 인스턴스를 생성하거나 그 메소드를 사용하고 싶으면 static키워드를 사용하면 된다.

```
public class StaticInnerClass {
	int a;
	void printStatic() {
		System.out.println("a -> "+a);
		Inner in = new Inner();
		in.innerA = 100;
		in.printInner();
  }
	static class Inner {
		int innerA;
		void printInner( ) {
			System.out.println("innerA -> "+innerA);
    }
  }

  public static void main(String[] args) {
    StaticInnerClass s = new StaticInnerClass();
    s.a = 10;
    s.printStatic();
    // Inner의 인스턴스가 StaticInnerClass의 인스턴스를 생성하지 않고 바로
    StaticInnerClass.Inner in = new StaticInnerClass.Inner();  
    in.printInner();
  }
}
```

##### 참고 - Nested Class의 사용목적
클래스 내부의 클래스는 기능을 묶기 위해서 흔히 사용된다.

### 2.4 static block과 instance block
instance block은 클래스 생성시 constructor보다 먼저 실행되는 블록이다. 보통 여러가지의 생성자가 있을 때 공통적으로 수행하고자 하는 코드가 있을때 이를 instance block를 통해 처리한다.
```
class StaticTest {
  // static block
  static {
    System.out.println("static initialize! count: " + count);
  }

  // instance block
	{ System.out.println("instance initialize...");}

	public StaticTest() {
		System.out.println("StaticTest constructor");
	}
	public StaticTest(int a) {
		System.out.println("StaticTest(int) constructor");
	}

	public static void main(String args[]) {
		System.out.println("Main Start!");
		StaticTest si=new StaticTest();
		System.out.println("Main...");
		StaticTest si2=new StaticTest();
	}
}

```
한 종류의 클래스당 한번만 실행하고 싶은 코드가 있다면 instance block에 static키워드를 사용하면 된다. instance block은 객체가 생성될 때 마다 호출되는 반면 static block은 단 한번만 호출된다.


## 3. final
마지막을 의미하며 클래스 앞에 정의하여 더이상 상속받을 수 없음을, 메소드 앞에 정의하여 Overriding할 수 없음을, 변수 앞에 정의하여 값을 변경할 수 없음을 나타내는 키워드이다. (변수에 사용하면 C에서의 `constant`와 같은 기능을 한다.)

- final class: 상속 받을 수 없음
- final method: Override 할 수 없음
- final variable: 상수로 정의

## 4. abstract
일부 구현되지 않은 메소드를 포함할 수 있는 *클래스* 정의 시에 사용하며, 구현되지 않은 *메소드* 정의 시에 사용한다.

```
abstract class Trans {
  abstract void start();
  abstract void stop();
}
```
### 4.1 추상 메소드
메소드 앞에 `abstract`키워드를 사용하여 추상 메소드를 선언할 수 있다. 구현되지 않은 메소드를 선언하는 기능을 한다. 추상메소드를 갖는 클래스는 반드시 추상클래스이여야 한다. (키워드 사용시 구현부가 없어야 한다.)

### 4.2 추상 클래스
#### 4.2.1 super class로 사용하기
추상 클래스는 객체화 수 없다. 다시 말하면 힙 영역에 올라갈 수 없다. 따라서 다음과 같은 코드는 사용할 수 없다.
```
class AbstractTest{
  public static void main(String[] args) {
    Trans t = new Trans();
  }
}
```
그렇다면 추상 클래스는 어떨 때 사용이 될까? 추상 클래스는 super class로써, 주로 틀을 만드는데 사용한다. 선언된 클래스 메소드들을 자식 클래스에서 오버라이드 하여 구현한다. 부모 클래스의 추상 메소드들을 전부 오버라이딩 해야 자식객체를 객체화할 수 있다.
```
  class Bus extends Trans{
    @Override
    void start() {}               //  Trans의 선언된 start()메소드를 오버라이딩 하여 구현
    @Override   
    void stop() {}                // Trnas의 선언된 stop()메소드를 오버라이딩 하여 구현
  }
  class AbstractTest {
    public static void main(String[] args) {
      Trans s = new Bus();        // Bus를 Trans로 upcasting
      s.start();                  // Bus의 start()함수 호출
      s.stop();                   // Bus의 stop()함수 호출
    }
  }
```
#### 4.1.2 추상 클래스는 일반 메소드를 가질 수 있다.
추상 클래스의 모든 메소드가 추상메소드일 필요는 없다.  
추상 메소드의 유무와 관계없이, 추상 클래스이면 객체화 될 수 없다. (모든 멤버 메소드가 일반 메소드 여도 추상 클래스이면 객체화가 불가능하다.)
