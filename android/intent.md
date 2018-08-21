# Intent
동일하거나 다른 Application안에 있는 Component 사이의 Run-time binding 실행하기 위한 객체이다.
- Activity 사이의 정보 전달은 intent객체를 사용한다.
- 다음에 실행될 component의 구체적인 행동을 설명한다.
- `startActivity(Intent)`메소드를 사용해서 ActivityManager에게 전달 intent객체를 넘겨줌. 이러한 구조 때문에 다른 앱의 화면을 호출할 수 있다.  

![img1](https://github.com/puzzlepcs/TIL/blob/master/android/img/intent01.PNG)

## 1 Intent 객체의 목적
Intent 객체를 사용하는 이유는 크게 두가지로 볼 수 있다. 첫번째는 target component를 활성화 시키는 것이며, 두번째는 상대 component에 데이터를 전달하는 것이다.
- target을 활성화
- 상대방에게 data를 보내기
  - 전달가능한 객체의 종류
    - Primitive Datatype
    - Serialized

## 2 종류
Intent 객체를 보낼 component가 명시되어 있는 경우와 그렇지 않는 경우에 따라서 구분할 수 있다.
### 2.1 Explicit Intents

  - 명시적 호출 방식
  - 클래스 객체나 컴포넌트 이름을 지정하여 호출할 대상을 확실히 알 수 있는 경우
  - Component를 명시하여 클래스가 실행될 때 정보를 제공하는 방법
  - 생성시 다음과 같이 특정 컴포넌트를 명시한다.
  ```
    Intent i = new Intent(this, SubActivity.class);
  ```
  - 시스템이 즉시 `Intent`객체에서 지정된 앱 구성 요소를 시작한다.  

다음 두 그림은 명시적 인텐트가 작동되는 원리를 보여준다.   
![img2](https://github.com/puzzlepcs/TIL/blob/master/android/img/intent02.PNG)
![img3](https://github.com/puzzlepcs/TIL/blob/master/android/img/intent03.PNG)

### 2.2 Implicit Intents
  - 특정 Component를 명시하지 않고, 일정한 조건을 통과한 Component를 찾아가는 방식
  - 일종의 broad casting과 같다.
  - Action, Category, Data 세 가지 값을 통해서 target을 찾음
  - MIME 타입에 따라 안드로이드 시스템에서 적절한 다른 앱의 엑티비티를 찾은 후 띄우는 방식을 사용
  - 매니피스트 파일에서 선언된 인텐트 필터와 비교하는 방법을 사용한다.


## 3 Intent 클래스 속성
### 3.1 ComponentName (구성 요소 이름)
  - 시작할 구성 요소의 이름
  - 값이 존재한다면: 명시적 호출 방식.
    - `Service`를 시작하는 경우, 항상 구성 요소 이름을 지정해야 한다. 그렇지 않으면 인텐트에 어느 서비스가 응답할지 확신할 수 없고, 사용자도 어느 서비스가 시작되는지 볼 수 없게 된다.
  - 값이 존재 하지 않는다면: 암시적 호출 방식. Action, Category, Data 세 가지 값을 통해서 target을 찾음
  - 정규화된 클래스 이름을 사용해 지정한다.

### 3.2 Action (작업)
- 수행할 일반적인 작업을 나타내는 문자열.
- 암시적 호출방식에서 이 속성을 보고 타겟 컴포넌트를 찾는다.
- 보통 `Intent` 클래스나 다른 프레임워크 클래스가 정의한 작업 상수를 사용한다.
  - `ACTION_VIEW` : 액티비티가 사용자에게 표시할 수 있는 어떤 정보를 가지고 있을 때 `startActivity()`가 있는 인텐트에서 사용한다.
  - `ACTION_SEND` : "공유" 인텐트라고도 하며, 사용자가 다른 앱을 통해 공유할 수 있는 데이터를 가지고 있을 때, `startActivity()`가 있는 인텐트에서 사용해야 한다.
- 인텐트에 대한 작업을 지정하려면 `setAction()` 또는 `Intent` 생성자를 사용하면 된다.

### 3.3 Data (데이터)
작업을 수행할 데이터 및 또는 해당 데이터의 MIME 유형을 참조하는 URI(`Uri` 객체)이다. 제공된 데이터의 유형을 나타낸다.  

URI의외에도 데이터의 유형(MIME 유형)을 지정할 수 있다. 예를들어, 인텐트에 음성파일이나 이미지 같은 특수한 유형의 데이터를 가리키는 URI를 넘겨줄 때 MIME 유형을 지정해주면 안드로이드 시스템이 인텐트를 수신할 최상의 구성 요소를 찾는데 도음이 된다.

데이터 URI를 설정 하려면 `setData()`를 호출하고, MIME 유형만 설정 하려면 `setType()`을 호출하면 된다. 이때 주의할 점은 두가지 모두 설정하고 싶을 때 이 메소드 두개를 사용하면 안된다는 것이다. 서로의 값을 무효화 하기 때문이다. 두가지 모두를 명시적으로 설정하고 싶다면 `setDataType()`을 사용하여 두가지를 모두 명시적으로 설정하면 된다.

### 3.4 Category (카테고리)
- 인텐트를 처리해야 하는 구성 요소의 종류에 관한 추가 정보를 담은 문자열.
- 꼭 필요한 값은 아니다.
- 보편적인 카테고리
  - `CATEGORY_BROWSABLE` : 대상 액티비티를 웹 브라우저 처럼 시작되도록 허용하는 것.
  - `CATEGORY_LAUNCHER` : 작업의 최초 액티비티임을 뜻하며, 시스템 애플리케이션 시작 관리자 목록으로 게재되어 있음.
- 카테코리를 지정하려면 `addCategory()`를 사용하면 된다.


### 3.5 Extras
  - target에게 전달할 정보를 여기에 저장.
  - `putExtras()`로 정보 저장
    - key-value를 받을 수 있음.
    - 모든 추가 데이터를 가진 Bundle 객체를 생성하여 이를 넣을 수 있음.
  - `getExtras()`메소드를 사용해서 여기에 저장된 값을 얻을 수 있음.
  - `Map`으로 구현되어 있음. key값을 사용해 그에 맞는 value를 찾을 수 있음.
  - 1MB 이하의 데이터 전달 가능

### 3.6 Flag (플래그)
- `Intent`클래스에서 정의된 플래그.
- 인텐트에 대한 메타데이터와 같은 기능을 함.
- Android 시스템에 액티비티를 시작할 방법에 대한 지침을 줄 수 있다.
- `setFlags()`메소드 사옹.
