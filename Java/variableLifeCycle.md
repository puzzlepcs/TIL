# Variable Life Cycle
## 1. Member Variable
class내에 정의되는 variable이다. 메모리 영역 중 heap에 생성된다.  
- static (class) variable: class가 메모리에 로딩시에 메모리 할당이 이루어지며, 자동초기화된다. class 제거시 제거된다.
- instance variable: 객체 생성시 자동으로 초기화 되어지며, 객체 제거시 제거된다.
- default initialization
  - 정수형(byte, short, int, long) : 0
  - 실수형(float, double): 0.0
  - boolean: false
  - char: \u0000
  - reference type: null

## 2. local variable
method나 constructor 내에 정의되는 variable이다. 메모리 영역 중 stack에 생성된다. method나 constructor 호출시 생성되었다가 수행 종료시 사라진다. *자동으로 초기화되지 않기 때문에 반드시 초기화하여 사용해야 한다.*  

[참고-래퍼런스타입 로컬변수 초기화](https://stackoverflow.com/questions/415687/why-are-local-variables-not-initialized-in-java)
