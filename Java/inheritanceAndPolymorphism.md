# Inheritance & Polymorphism
## 1. Inheritance(상속)
### 1.1 상속의 정의
![Inheritance image](https://github.com/puzzlepcs/TIL/blob/master/Java/inheritance.PNG)  
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
3. **~~**:

#### 1.2.1 Method Overriding
상속받은 super의 method중 특정 method의 내용을 수정하여 다시 정의하는 기법이다.
* 규칙: sub 클래스의 Overriding 되는 method는 상속받은 super 클래스의 아래 내용이 반드시 같아야 한다.
  * Name, Return type, Argument list, Access modifier
  * 만약 위의 내용 중 하나라도 같지 않다면 재정의가 아니라 확장의 의미를 갖는 메소드이다.
* `@Override`: 아래 정의된 method가 Overriding 문법에 맞는지를 컴파일러에게 확인 요청한다. 실행과 관계없다.
  * Java의 모든 클래스들은 단 하나의 클래스를 상속받고 있다. Java에서 모든 클래스의 부모 클래스는 `java.lang.Object`라는 클래스이다. (컴파일시 컴파일러가 자동으로 `extends Object`라는 코드를 삽입한다.)
    * `toString()` 메소드는 `Object`클래스의 메소드이다. 따라서 클래스에서 오버라이딩 하지 않는다면 부모 클래스인 Object의 `toString()`메소드가 호출되며, 그 변수의 hashcode를 String으로 반환해준다.

#### 1.2.2 Overriding vs Overloading
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

### 1.3 상속과 메모리
#### 1.3.1 상속과 객체 생성 순서
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
#### 1.3.2 상속과 생성자
 Sub 클래스의 생성자에는 super의 생성자가 컴파일시 자동으로 호출된다. 따라서 Super 클래스에서 생성자 오버로딩시에 default 생성자를 선언하지 않으면 존재하지 않는 메소드를 호출하는 것과 같기 때문에 에러가 발생한다.

### 1.4 super키워드
객체 생성시 자동으로 생성되는 두가지 변수 중 하나로, super가 있다. super변수를 사용하면 상속받은 부모의 속성들과 메소드들을 사용할 수 있다.


## 2. Polymorphism(다형성)
