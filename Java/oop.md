# 객체지향
## 1. 객체 지향이란?
SW의 모든 구성원이 객체(object)로 구성되며, 객체들의 관계성으로 프로그램이 작동되는 것이다. 그렇기 떄문에 객체를 만들기 위해 클리스를 이용하여 객체가 가져야 할 구성요소를 설계하게 된다.

객체(Object)는 데이터(Data)와 기능(Method)을 포함한다.

- Abstraction => class => new = object
- Encapsulation => Access Modifier(public, protected, default, private)
- Inheritance => extends
- Polymorphism => Method Polymorphism(Override, Overload) & Object Polymorphism()

## 2. OOP에서의 4가지 개념
### 2.1 **Abstraction**(추상화)
*'무엇을 객체로 도출해야 하는가?'* 라는 질문에서 시작한, 객체의 설계라고 할 수 있다. Java에서는 추상화를 통해 **Class** 라는 객체를 만든다.
  * class와 object
    class는 객체의 설계도라고 생각하면 된다. class는 프로그램 내에서 직접 사용되는 것이 아니다. 반면 class를 이용해 생성된 객체는 메모리 상에 존재한다.
    object는 class의 dynamic instance이고, class는 object의 blueprint라고 한다.

### 2.2 **Encapsulation**(은닉화)
클래스 설계시에 데이터와 기능을 클래스라는 틀에 넣어서 설계하고, 중요한 데이터나 **복잡한 구현을 숨기고** , 사용에 꼭 필요한 기능만을 공개하여 정의하는 기법. Java에서는  **Access Modifier로 객체무결성을 지키는 기능** 을 한다. [더보기-Access Modifier](https://github.com/puzzlepcs/TIL/blob/master/Java/class.md#5-access-modifier-%EC%A0%91%EA%B7%BC%EC%A0%9C%ED%95%9C%EC%9E%90)  
- 중요하거나 상세한 구현은 private 키워드를 사용하여 숨긴다.
- 접근에 필요한 기능만을 public을 사용하여 공개한다.
- setter와 getter함수를 통해 접근, 제어한다.
  - attribute는 private, method는 public을 사용한다
- 중요한 데이터의 은닉과 보호

은닉화를 적용하면 필요한 기능만 공개되어 있기 때문에 사용이 편리해지고 코드의 유지보수를 용이하게 만든다.  

제공되는 API의 대부분의 Encapsulation이 적용되어 있기 때문에 개발자가 보다 쉽게 API를 사용할 수 있게 된다.  

### 2.3 **Inheritance**(상속)
Sub(자식)가 Super(부모)의 **모든** 것을 물려받는 것. 즉, 선택적 상속은 되지 않는다. Java에서는 단일상속만을 지원하며, extends 키워드를 통해 부모클래스의 속성과 메소드들을 상속받을 수 있다.

### 2.4 **Polymorphism**(다형성)
- Method Polymorphism
  - Overload
  - Override
- Object Polymorphism: 같은 타입의 변수가 다양한 형태의 객체를 참조하는 것을 말하고 super type의 변수가 다양한 sub type을 참조하는 형태를 의미한다.

## 3. OOP의 장점
프로그램을 객체지향으로 설계하면 **유지 보수가 빠르고 쉽다**. 변경사항을 반영하기 쉬운것이 가장 큰 장점이다. 잘 설계된 프로그램은 한 부분을 바꾸어도 다른 코드에 영향이 없다. 이를 '위임'이라고 하며, 클래스 설계시 객체지향의 특성을 잘 반영한다면 유지 보수가 간단한 프로그램을 만들 수 있다.
