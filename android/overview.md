# Android Platform
## 1. Overview
### 1.1 Andriod란?
- 모바일 디바이스를 위한 소프트웨어 스택
- Google, Open Handset Alliance
- 운영체제, 미들웨어를 비롯한 필수 응용프로그램을 포함.
- 오픈소스 기반의 개방적 플랫폼
- 컴포넌트 기반의 아키텍쳐
  - application을 하나의 컴포넌트로 봄
  - 교체가 좋아짐
    - 통신구조일때 교체성이 가장 뛰어남.
    - 안드로이드는 기본 구조 관계가 통신구조
    - 프로토콜만 지키면 됨.
    - 그러나 통신구조는 연결에 비용이 큼
    - 서로 원격으로 메소드를 호출 (직접 호출 제한)
    - 메모리를 사용해서 원격으로 소통
    - ipc 통신구조 사용
  - Launcher라는 애플리케이션으로 차별화가 가능
- 응용프로그램의 LifeCycle 자동 관리
  - 프레임워크가 관리한다.
- Andriod Application 개발에 필요한 기본적인 Tool을 제공
- Java 기본- 호환성
- 기본적으로 클라이언트 프로그램
  - 사용자로부터 이벤트를 받거나, 정보를 받거나 보여주는 목적이 없다면 화면을 만들지 않아도 됨
### 1.2 주요 특징
- 응용 프레임위커: 컴포넌트를 교체, 재사용 가능
- Dalvic VM: 모바일 디바이스에 최적화
- SQLite: 데이터베이스

### 1.3 Application Framework
반제품 형태의 구조를 사용자가 활용할 수 있게끔 되어있음. Java에서 상속과 오버라이드의 개념으로 구현할 수 있다.
메소드를 선언하고 구현한다. 메소드를 호출하는 것은 플랫폼이 한다. 객체 생성도 하지 않는다. 이를 모두 플랫폼이 담당하기 때문이다.
- Java Programming Language로 작성
- Android Application이란?
  - Andriod package(* .apk) 형태
  - 스마트폰 등 디바이스로 다은로드 하는 단위
  - Java code+data/resource files로 구성
  - aapt tool을 사용하여 제작
- Core Application
  - Email Client
  - SMS program
  - Calendar
  - Maps
  - Browser
  - Contacts 등

### 1.4 Andrid Platform 관련기술
- Linux
- Java
- **XML** 
  - data저장의 용도,
  - 화면 설계의 용도,
  - 통신의 문서교환 형식으로 XML을 사용

#### 1.4.1 Android 개발환경 구축
- Java JDK 8.0 (9.0, 10.0버전 사용불가)
- Android SDK(Software Develop Kit)
  - build tools
  - Android SDK version
    - 1 ~ 28 versions..
      - 3.0 ~ 3.2 : 태블렛버전. 이제는 사용하지 않음
      - 4.0(icecream sandwich) : 통합버전. NFC, Blutooth Low Energy, Pay
      - 5.0: VM을 번경,(Andriod ru) 32bit에서 64bit으로 변경, Matrial Design추가
      - 6.0(Jellybean): 64bit체계로 정착
      -  7.0(Nougat), 8.0(Oreo), 9.0(Pie)
    - 버전을 잘 골라야됨 ^^, 지원하는 기능과 안드로이드가 제공하는 기능을 고려해서 개발.
    - 보통 15버전 gingerbread를 target version으로 잡음
- 개발툴 : Android Studio or Eclipse
  - Eclipse : Java를 사용하기 때문
  - Andriod Studio : Google에서 개발한 개발툴.
    - multi module 지원
      - 같은 application id를 가지게 됨.
- Andriod Emulator

## 2. 안드로이드의 플랫폼 아키텍처
기본적으로  Java를 사용하며, 일부는 C/C++로 구현되어있다.
### 2.1 Linux Kernel
ART는 스레딩 및 하위 수준의 메모리 관리와 같은 기본 기능에 Linux 커널을 사용한다.

### 2.2 HAL(Hardware abstraction layer)
상위 수준의 Java API 프레임워크에 기기 하드웨어 기능을 기능을 노출하는 표준 인터페이스를 제공한다. HAL은 여러 라이브러리 모듈로 구성되어 있으며, 카메라 또는 블루투스 모듈과 같은 특정 유형의 하드웨어 구성요소를 위한 인터페이스를 구현한다. 프레임워크 API가 기기 하드웨어에 엑세스하기 위해 호출을 수행하면 Android 시스템이 해당 하드웨어

### 2.3 ART
컴파일을 할때 byte코드로 하고 , install 할 떄 os가 이해할 수 있게끔 일부컴파일 하여 실행 속도를 빠르게 하게끔 하였다. (인스톨 시간을 늘리고 실행 시간을 줄임)
Java를 사용하지만 JVM을 가지고 오지 못하고 그 대신 Dalvic이라는 가상머신을 사용한다.
- AOT(Ahead-of-Time, 실행시간 전에 미리 컴파일 하는 것) 컴파일 및 JIT(Just in time)컴파일
- Concurrent Garbage Collector 기법
  - 메모리가 부족할 때(heap에서 공간이 부족할 때) GC를 수행
    - GC도 일종의 스레드. priority가 보통 스레드보다 낮음. (GC의 priority는 보통 2에서 3)
    - GC가 필요한 상황에서 priority를 높여서 스레드를 수행.
  - CPU가 한가할 때
    - priority가 낮아도 수행할 스레드가 없을 때 수행됨

## 3. 참고사이트
- 안드로이드 공식 사이트 [www.android.com](https://www.android.com)
- 안드로이드 개발자를 위한 사이트 [developer.android.com](https://developer.android.com)
  - 안드로이드의 플랫폼 아키텍처, 버전정보등을 볼 수 있다.
    - Linux, HAL, Native C/C++ Libraries까지 C/C++로 구축
    - Android Runtime, Java API Framework, System Apps는 Java로 구현
    - System Apps 밑의 Java API Framework의 구조와 기능을
