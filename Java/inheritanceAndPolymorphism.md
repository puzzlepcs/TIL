# Inheritance & Polymorphism
## 1. Inheritance(상속)
### 1.1 상속의 정의
![Inheritance image](https://github.com/puzzlepcs/TIL/blob/master/Java/img/inheritance.PNG)  
Sub(자식)가 Super(부모)의 **모든** 것을 물려받는 것. 즉 선택적 상속은 되지 않는다.  
설계적 관점에서 Generalization, Specialization을 위해 상속을 사용한다. 공통적인 특성을 모아 super class로 generalize하고, 새로운 specialized된 sub class를 만든다.
```
  class Sub extends Super {
      ...
  }
```
설계적 관점에서 Generalization, Specialization을 위해 상속을 사용한다.  

### 1.2 상속의 목적
1. **확장**: Super에 더 많은 기능을 확장한 Sub클래스를 만들어서 사용할 수 있다.
2. **재정의**: Overriding이라고도 하며, 메소드를 다시 정의하는 것이다.
3. **객체의 형변환**: 참조타입인 객체는 primitive와 달리 정해진 타입이 아니기 때문에 상속을 사용해 형변환 한다.

#### 1.2.1 재정의의 의미로서의 상속
##### Method Overriding
상속받은 super의 method중 특정 method의 내용을 수정, 추가하여 다시 정의하는 기법이다.
* 규칙: sub 클래스의 Overriding 되는 method는 상속받은 super 클래스의 아래 내용이 반드시 같아야 한다.
  * Name, Return type, Argument list, Access modifier
  * 만약 위의 내용 중 하나라도 같지 않다면 재정의가 아니라 확장의 의미를 갖는 메소드이다.
* `@Override`: 아래 정의된 method가 Overriding 문법에 맞는지를 컴파일러에게 확인 요청한다. 실행과 관계없다.
  * Java의 모든 클래스들은 단 하나의 클래스를 상속받고 있다. Java에서 모든 클래스의 부모 클래스는 `java.lang.Object`라는 클래스이다. (컴파일시 컴파일러가 자동으로 `extends Object`라는 코드를 삽입한다.)
    * `toString()` 메소드는 `Object`클래스의 메소드이다. 따라서 클래스에서 오버라이딩 하지 않는다면 부모 클래스인 Object의 `toString()`메소드가 호출되며, 그 변수의 hashcode를 String으로 반환해준다.

##### Overriding vs Overloading
Method Overriding과 Method Overloading을 혼동하지 않도록 주의하자.
* 공통점
  * 메소드 정의시 사용되는 기법이다.
  * 똑같은 메소드 이름을 정의할 때 사용한다.
  * Polymorphism(다형성) 효과
* 차이점
  * Overriding: super 로부터 상속받은 기능 중 특정 기능을 재정의하는 기법
    * 상속을 기반
    * 메소드 이름, arguement list는 항상 같아야 한다.
    * modifier는 같거나 보다 넓은 범위로 정의해야 한다.
  * Overloading
    * 하나의 클래스 내에서 이루어진다.
    * 같거나 비슷한 기능의 method의 이름을 같게 정의해서 편리성을 추구하는 것이다.
    * 메소드 이름은 같게, argument list는 다르게 정의한다.
    * 나머지 method 형식은 상관 없다.  

### 1.3 상속의 장단점
* 장점
  * 재사용성 증가
  * 일관성 증가
  * 유지보수성 증가
  * 명세서 역할
  * Polymorphism
* 단점
  * 지나친 상속은 프로그램의 구조의 복잡성을 증가시킨다
  * 지나친 상속은 JVM 관리에 부하를 줄 수 있다.
  * 지나친 상속은 성능 저하를 일으킨다.

## 2. Polymorphism(다형성)
* object polymorphism : 같은 타입의 변수가 다양한 형태의 객체를 참조하는 것.
  * super type의 변수가 다양한 sub type을 참조.
  * 객체 생성시 super도 같이 생성되어지기 떄문에 메모리에 존재하는 super type으로 변수를 선언할 수 있다.
  ```
    Member m = new Member();
    Member mc = new MainMember();
  ```
* method polymorphism
  * 같은 클래스 타입의 메소드 호출 시 그 기능이 다양하게 처리 되어지는 것.
  * Override와 Oveload가 있다.
  
## 3. 상속과 다형성
### 3.1 상속과 메모리
#### 3.1.1 상속과 객체 생성 순서
클래스 로더가 클래스 메모리 영역에 클래스 관련 정보를 로드한다. Sub 클래스를 객체화 하면, 클래스 영역의 Super 클래스의 인스턴스를 먼저 생성한 뒤, Sub 클래스의 인스턴스를 생성한다. 그 둘을 하나로 묶은 주소값을 Stack영역의 메모리에 저장하게 된다.  

```
// Member.java
  public class Member {
    Member() { System.out.println("Member Constructor!"); }
  }
```
```
// VipMember.java
  public class VipMember extends Member{
    VipMember() { System.out.println("VipMember Constructor!"); }
  }
```
```
// MemberMain.java
public class MemberMain{
  public static void main(String[] args) {
    VipMember v = new VipMember();

    /**
    *   ***실행시 출력화면***
    *   Member Constructor!
    *   VipMember Constructor!
    *
    */
  }
}
```
#### 3.1.2 상속과 생성자
 Sub 클래스의 생성자에는 super의 생성자가 컴파일시 자동으로 호출된다. 따라서 Super 클래스에서 생성자 오버로딩시에 default 생성자를 선언하지 않으면 존재하지 않는 메소드를 호출하는 것과 같기 때문에 에러가 발생한다.  

### 3.2 super키워드
객체 생성시 자동으로 생성되는 두가지 변수 중 하나로, super가 있다. super는 현재 수행중인 객체(this가 레퍼런스하고있는 객체)가 상속받은 상위 객체의 레퍼런스를 갖는 reference variable이다. super변수를 사용하면 상속받은 부모의 생성자, 속성들과 메소드들을 사용할 수 있다.

* super: 현재 수행중인 객체의 상위 객체의 reference를 가지고 있다. 독립적으로 사용하지는 못한다.
  * super() : 부모 클래스의 생성자 호출 가능
  * super(argument_list) : argument_list가 같은 super객체의 생성자를 호출한다. (단, 생성자 내의 첫번재 줄에서만 사용가능하다.)
  ```
    // this()또한 첫번째 라인에서만 사용가능하므로 에러 발생
    Member(String hobby) {
      super(hobby);
      this();
    }
  ```
  * super.attribute :
  * super.method() : 상속받은 메소드 호출시, 현재 수행중인 객체와 상속받은 객체의 메소드명이 같을 경우 사용한다.

### 3.3 단일상속
Java는 다른 OOP와는 다르게 단일 상속만을 지원한다. 이는 다중상속의 모호성(다이아몬드 상속구조 등)으로 인한 문제를 피하기 위함이다.  
단일상속만을 사용하여 단순한 클래스 구조로 복잡도를 낮추고, Interface라는 레퍼런스타입을 사용하여 다중상속의 이점을 취할 수 있다.

### 3.4 객체타입의 형변환
Primivite 타입과 같이 객체타입 또한 형변환을 할 수 있다. 다만 크기를 기반으로 하는 것이 아니라, 상속을 기반으로 형변환을 해야 한다. 예제를 살펴보자.
#### 3.4.1 Upcasting  
```
  class Customer {  }
  class MainCustomer extends Customer { }
  public static void main(String[] args) {
    Customer c = new MainCustomer();
  }
```
![upcastImg01](https://github.com/puzzlepcs/TIL/blob/master/Java/img/polymorphism01.PNG)
위의 코드를 실행하면 메모리상에는 위의 그림과 같이 객체가 형성된다. MainCustomer가 Customer로 Casting이 될 수 있다. 주의해야 할 점은 힙 메모리 영역의 MainCustomer가 Shadowing 될 뿐, 그 객체 자체가 Customer로 바뀌는 것이 아니라는 것이다. 가리키고 있는 인자의 타입만이 바뀌는 것이다.
#### 3.4.2 Down Casting - 위험한 형변환
다음의 코드는 컴파일 에러발생한다. (Down Casting시 메모리상 에러. 프로그램 실행 중 접근할 수 없는 영역에 접근하여 에러가 발생할 수 있다.) 여기서 주의해야 할 점은 Down Casting시 컴파일에러는 없고, 호출은 가능하다는 것이다.  
```
MainCustomer mc = new Customer();   
// MainCustomer mc = new (MainCustomer) Customer();
// 명시적형변환시 컴파일에러가 사라지지만 런타임 에러가 발생할 수 있다.
```
![upcastImg02](https://github.com/puzzlepcs/TIL/blob/master/Java/polymorphism02.PNG)

이러한 다운 캐스팅은 메소드의 인자로 부모 클래스의 타입으로 Upcasting되어 Shadowed된 메소드들과 속성들에 접근하기 위해 사용된다.
```
  public static void main(String[] args) {
    Customer c = new Customer();
    MainCustomer mc = new Customer();

    printCustomer(c);
    printCustomer(mc);
  }

  public static void printCustomer(Customer c) {
    System.out.println(c.toString());
  }
```  

#### 3.4.3 안전한 형변화를 위한 `instanceof` 키워드
객체가 어떤 타입인지 알아낼 때 사용되는 키워드이다. 위와 같이 업캐스팅된 인자를 다시 다운 캐스팅 하기 위해 그 타입이 맞는지 확인할 때 많이 사용된다.
```
public static void printCustomer(Customer c) {
    if(c instanceof MainCustomer) {
      MainCustomer mc = (MainCustomer) c;
      System.out.println(mc.toString());
    } else {
      System.out.println(c.toString());
    }  
}
```

#### 3.4.4 예제

```
  Customer c = new Customer();        
  Customer cc = new MainCustomer();                       // Upcasting
  MainCustomer mc = new MainCustomer();
  // Error             
  // MainCustomer mc1 = (MainCustomer) new Customer();    // Down Casting

  // Customer을 상속받고 있는 모든 객체는 Customer 배열에 들어올 수 있다.
  Customer[] arrcc = new Customer[10];
	arrcc[0] = c;
	arrcc[1] = cc;
	arrcc[2] = mc;
	arrcc[3] = mc1;

  MainCustomer[] arrmm = new MainCustomer[10];
	arrmm[0] = mc;
	arrmm[1] = mc1;
	arrmm[2] = c;        // Error
	arrmm[3] = cc;       // Error
```
이와같이 부모클래스의 배열을 생성하면 그 자식 클래스들을 그 배열에 넣을 수 있다. 이를 응용해서  Object의 배열을 생성하면 그 안에 모든 자료형을 넣을 수 있다. (Java의 모든 자료형은 Object 객체로 Upcasting이 가능하다고 할 수 있다.)  배열에서 뿐만 아니라 메소드의 argument로 객체를 넘길 때, 인자 타입의 자식 클래스들을 모두 인자로 넘길  수 있다.
```
  Object[] obj = new Object[10];
  obj[0] = 1;               // int
  obj[1] = 1.1;             // double
  obj[2] = "hello";         // String
  obj[3] = new Customer();  // user defined class
```

### 3.5 Dynamic Runtime Binding
Java는 기본적으로 동적 런타임 바인딩을 한다. 자식 클래스에서 오버라이딩을 하지 않은 메소드를 호출하면 기본적으로 부모 클래스의 메소드를 사용하고, 오버라이딩을 했다면 기본적으로 오버라이딩 된 메소드를 사용한다. 맴버 변수의 경우 객체가 생성된 뒤 받은 stack의 변수의 타입을 따라간다. 다음과 같이 생각하면 편하다.
* 멤버 변수의 경우: 인자의 타입을 따라감
* 멤버 메소드의 경우: new한 객체를 따라감
```
class Parent{
	int k=10;
	void over()	{
		System.out.println("Parent Class over!");
	}
	void mParent(){
		System.out.println("Parent method");
	}
}
class Child   extends Parent{
	int k=20;
	@Override
	void over() {   //Overriding

		System.out.println("Child class over!");
	}
	void mChild(){

		System.out.println("Child method");
	}
	// Child의 메소드는 3개! over(), mChild, mParent
	// over()가 2가지가 아님.
}
class OverridingTest
{
	public static void main(String a[])
	{
		Parent p2 = new Child();
		System.out.println(p2.k);       // 10
		p2.over();                      // Child class over!
		p2.mParent();                   // Parent method
	}
}
```
![runtimeBindingImg](https://github.com/puzzlepcs/TIL/blob/master/Java/img/polymorphism03.PNG)
