# Component
## 1. 4가지 Main component
Android 애플리케이션 개발은 주요 Component(Activity, Service, BroadcastReceiver, ContentProvider)를 상속받아 정의된 메소드를 Override하여 구현한다. 주요 component를 구현한 클래스가 하나 이상 존재해야 한다. 주요 component를 상속받은 클래스는 반드시 `AndroidManifest.xml`파일에 등록되어야 Framework가 인식하여 처리한다.
### 1.1 Activity
화면, 데이터를 보여주고 입력받고 이벤트 처리
안드로이드 화면의 기본 단위.

#### 1.1.1 Activity LifeCycle


### 1.2 Service
백그라운드 작업.  화면이 필요 없는 경우(백그라운드): 다운로드, 음악

### 1.3 ContentProvider
데이터의 공유
- 주소록 프로그램을 예로 들어 보자.
- 주소록의 데이터를 전화 프로그램, 카카오톡 등에서 필요함.
- 주소록의 데이터를 요청하는 프로그램을 클라이언트(caller), 데이터를 제공해야 하는 쪽이 서버(callee)가되어 통신을 한다.

- 리눅스 퍼미션으로 파일, 데이터 접근 제어. 파일을 생성한 앱만 접근이 허용됨.
- 직접적 접근이 불가능 하기 때문에 통신!

- 데이터를 제공할 서버 기능을 구축해놓음.
  - 데이터 제공해야 할 경우 ContentProvider클래스를 상속받으면 된다.
  - SQLite DB에 저장된 데이터를 공유

ContentProvider의 구현
  - ContentProvider 클래스를 상속 받아, 공유하고자 하는 DB나 File을 처리하는 클래스를 구현한다.
  - 구현된 ContentProvider를 접근하고자 할 때에는 직접적으로 ContentProvider메소드를 호출 할 수 없고, 대신 ContentResolver객체의 메소드를 사용하여 호출한다.
  - ContentResolver는 Uri를 용
### 1.4 BroadcastReceiver
- caller 와 callee
  - caller는 callee의 주소를 알아야 함. 주소를 알아내는 방식은 2가지가 있다.
    - 명시적 호출방식
      - caller가 callee의 이름을 직접 호출
    - 암시적 호출방식(broad casting)
      - target의 이름을 모를 때 호출
  - 안드로이드에서는 주로 암시적 호출방식을 사용한다.  
- `onReceive()`메소드를 꼭 오버라이딩 해야 한다.

## 2. Component 선언
프레임워크가 객체 생성. 따라서 프레임워크에게 이 4개의 클래스를 상속받은 클래스들를 `AndroidManifest.xml` 파일에 기록을 해주어야 한다. 또한 메소드들을 오버라이딩 해놓으면 그 기능을 프레임워크가 실행해준다. 따라서 다음의 클래스들의 메소드가 어떤 일을 하는지, 어떤 때에 호출되는 지 알아야 한다.
- `<activity>, <service>, <provider>`
  - Manifest 파일에 반드시 선언되어야 할 component. 선언되지 않으면 실행되지 않는다.
- `<reciever>`
  - Manifest 파일에 선언될 수 있고, 코드안에서 직접 생성 가능
  - BroadcastReceiver 객체로 생성되어 `registerReciver()`로 시스템에 등록
