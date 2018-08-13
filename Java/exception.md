# Exception
## 1. 예외(Exception)란?
### 1.1 exception vs error
예외(exception)는 개발자가 구현한 로직에서 발생한다. 즉 예외는 발생할 상황을 미리 예측하여 처리할 수 있다. 예외는 개발자가 처리하는 것이 가능하기 때문에 예외를 구분하고 그에 따른 처리 방법을 명확히 알고 적용하는 것이 중요하다. Java에서는 이러한 상황을 java.lang 패키지의 Exception이라는 클래스를 통해 관리한다.
반면 오류(error)는 시스템에 비정상적인 상황이 생겼을 때 발생한다. Java에서는 이러한 오류를 Error라는 클래스로 따로 관리한다.
- Exception class
  - 정확한 프로그램(*sondness?completeness? [link](https://math.stackexchange.com/questions/105575/what-is-the-difference-between-completeness-and-soundness-in-first-order-logic)*)
  - 예외가 발생할지 모르는 상황을 체크해 준다.(Compiler)
  - 예외가 발생하더라도 프로그램을 중단시키지 않고, 복구하여 프로그램을 지속적으로 실행 할 수 있도록 한다.
- Error class
  - Fatal situations (serious error)
  - Unchecked exceptions
  - Not expected to attempt recovery
  - 치명적 오류로 SW적으로 복구가 불가능
  - **컴파일러가 체크하지 않는다.**

### 1.2 예외 클래스의 구조
[img01](https://github.com/puzzlepcs/TIL/blob/master/Java/img/exception01.PNG)
모든 예외클래스는  Throwable클래스를 상속 받으며, Throwable은 최상위 클래스 Object의 자식 클래스이다.  
Throwable을 상속받는 클래스에는 Error와 Exception이 있다. Error는 시스템 레벨의 심각한 수준의 에러이기 때문에 시스템에 변화를 주어 문제를 처리해야 하는 경우가 일반적이다. 반면 Exception은 개발자가 로직을 추가하여 처리할 수 있다.  

### 1.3 Checked(Compile) Exception vs Unchecked(Runtime) Exception
구분  |Checked Exception|Unchecked Exception
------|-----------------|-------------------
처리여부|반드시 예외를 처리해야 함|명시적인 처리를 강제하지 않음
확인시점|컴파일 단계|실행단계  

두 Exception의 구분 기준은 '꼭 처리를 해야 하는가'이다. Checked Exception이 발생할 가능성이 있는 메소드라면 반드시 로직을 try/catch로 감싸거지 throw로 던져서 처리해주어야 한다. 반면 Unchecked Exception은 명시적인 예외 처리를 하지 않아도 된다.  

컴파일러는 RuntimeException, Error의 경우 SW적으로 복구가 불가능 하기 때문에 이를 체크하지 않는다. RuntimeException을 제외한 모든 Exception클래스들은 컴파일러가 체크하여 복구 코드를 구현한다.  

- Checked Exception - RuntimeException을 제외한 모든 Exception
  - 예기치 못한 경우 경미한 오류
  - SW적으로 복구 가능
  - 오류가 발생하여 프로그램이 중단되는걸 막기 위해 컴파일시에 컴파일러가 체크하여 복구 코드를 구현하도록 하고 있다.
  - 컴파일 단계에서 명확하게 Exception 체크가 가능한 예외
  - IOException, SQLException
- Unchecked Exception(RuntimeException) & Error클래스
  - SW적으로 복구가 불가능하기 때문에 컴파일러가 체크하지 않는다.
  - 컴파일 단계에서 확인할 수 없는 예외
  - RuntimeException : 코드작성이 잘못된 오류. 실행시 오류 발생.
  - NullPointerException, IllegalArgumentException, IndexOutOfBoundException, SystemException

## 2. Exception Handling
### 2.1 try-catch블럭
```
try {
  // 예외 발생시 코드 실행을 중지하고 catch블럭으로 넘어간다.
  // 따라서 중간에 예외가 발생한다면 발생한 지점 다음의 코드는 실행되지 않는다.
} catch (XxxException e) {
  // 예외 발생시 복구 코드
}
```
여러가지 예외가 발생하는 경우는 catch블럭을 여러개 정의하면 된다. 단, Exception 클래스들이 상속 관계일 경우, 서브클래스부터 정의해야 올바르게 수행된다.

예외 발생 여부와 관계없이 마지막으로 꼭 수행해야 할 코드가 있다면 finally 블럭을 구현한다.
```
  try {
    ...
  } catch (XxxException e){
    ...
  } finally {
    // 꼭 수행해야 할 코드
  }
```
catch블럭 없이 try-finally 블럭을 사용할 수 있으나 이런 경우 try 블럭에서 에러가 날 경우 처리가 불가능하다.
### 2.2 Declare Exception 예외처리 회피, throws
#### 2.2.1 throws 사용법
```
  public void methodName() throws XxxException {
    // 예외가 발생할지도 모르는 문장
  }
```
예외를 처리하지 않고, 호출한 메소드에서 예외처리를 넘겨버릴 수 있다. 호출한 메소드에게 처리 중 예외가 발생했음을 알리기 위해서 사용한다.  
간단해 보이지만 아주 신중해야 하는 로직이다. 예외가 발생하면 throws를 통해 호출한 쪽으로 예뢰를 던지고 그 처리를 회피하는 것이다. 호출한 쪽에서 다시 예외를 받아 처리하도록 하거나 해당 메소드에서 이 예외를 던지는 것이 최선의 방법이라는 확신이 있을 때만 사용해야 한다.  

#### 2.2.2 Overriding되는 메소드의 경우
1. Super 클래스의 메소드가 throws 하고 있는 것을 **그대로** throws 할 수 있다.
2. Super 클래스의 메소드가 throws하고 있는 것의 **Sub Exception** 클래스를 throws 할 수 있다.
3. Sub 클래스의 메서드에서 필요 없다면 throws을 **기술하지 않아도 된다.**

## 3. Customize Exception
VM이 발생하지 않은 예외를 개발자가 직접 문제가 있는 상황에서 예외를 발생시킬 수 있다. API에서 정의된 알맞는 예외가 없을 경우 필요한 예외를 직접 설계할 수 있다. Exception 클래스를 상속받아 구현한다.
필요한 Exception 클래스를 객체 생성한 뒤 그 객체를 `throw`키워드 사용하여 예외로 발생시킨다. (`throws`와 다르다!)
```
  IOException me = new IOException();
  trow me;
```
혹은
```
  throw new IOException();
```

#### 참고 사이트
1. [Java 예외 처리에 대한 작은 생각](http://www.nextree.co.kr/p3239/)
2. [Java-예외란? 체크예외와 RuntimeException](http://hyeonstorage.tistory.com/199)
3. [Checked vs Unchecked Exceptions in Java](https://www.geeksforgeeks.org/checked-vs-unchecked-exceptions-in-java/)
