# Inheritance & Polymorphism
## 1. Inheritance(상속)
### 1.1 상속의 정의
![Inheritance image](https://github.com/puzzlepcs/TIL/blob/master/Java/inheritance.PNG)
Sub(자식)가 Super(부모)의 **모든** 것을 물려받는 것. 즉 선택적 상속은 되지 않는다.  
설계적 관점에서 Generalization, Specialization을 위해 상속을 사용한다. 공통적인 특성을 모아 super class로 generalize하고, 새로운 specialized된 sub class를 만든다.
```
  class Sub extends Super {

  }
```

설계적 관점에서 Generalization, Specialization을 위해 상속을 사용한다.
### 1.2 상속의 목적
1. 확장: Super에 더 많은 기능을 확장하여 사용할 수 있다.

### 1.3 상속과 메모리
클래스 로더가 클래스 메모리 영역에 클래스 관련 정보를 로드한다. Sub 클래스를 객체화 하면, 클래스 영역의 Super 클래스의 인스턴스를 먼저 생성한 뒤, Sub 클래스의 인스턴스를 생성한다. 그 둘을 하나로 묶어서 Stack영역의 메모리에 주소값을 연결해주게 된다.

## 2. Polymorphism(다형성)
