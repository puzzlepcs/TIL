# API(Application Programming Interface)
## 1. API란?
API(Application Programmaing Interface, 응용 프로그래밍 인터페이스)는 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻한다. 주로 파일 제어, 창 제어, 화상처리, 문자 제어등을 위한 인터페이스를 제공한다.

절차식 언어에서의 API는 특정한 작업을 수행할 함수의 집합을 규정한다. 특정 소프트웨어 구성요소와 상호 작용할 수 있게 한다.

객체지향에서 class단위로 미리 구현되어 제공되는 프로그램을 API라고 한다. class단위의 library이다.

## 2. API의 종류
- 표준 API: Java와 함께 구현되어 제공되는 프로그램.
  - jre 폴더에 rt.zip파일에 class 파일이 포함되어 있다.
- vendor API: 기업에서 (프로젝트에 사용하기 위해) 미리 작성해 놓은 프로그램.
- 사용자 정의 API: 개발자가 미리 작성하여 사용하는 프로그램.

## 3. 표준 API
- class file: jdk설치 폴더/jre/lib/rt.jar로 java 샐행시에 사용한다.
- Documentation file: 라이브러리의 클래스에 관한 설명이 문서화되어 있다. 온라인, 오프라인 도큐먼트가 존재한다.
### 3.1 표준 API의 package구조
- java.awt: 자바의 기본 그래픽 화면 클래스를 제공한다. 현재 만히 사용되지 않는 추세
- java.io: 자바의 입출력 관련 클래스와 인터페이스를 제공
- **[java.lang](https://github.com/puzzlepcs/TIL/blob/master/Java/javalang.md): 자바의 기본적인 클래스를 제공한다.**
  - import하지 않아도 사용할 수 있다.
  - String 클래스가 이 package에 포함되어 있다.
- java.net: 네트워크 관련 클래스
- java.sql: Java가 DB를 연동하기 위한 관련 클래스와 인터페이스를 제공.
- java.text: 문자열의 포맷 관련 클래스 제공.
- **java.util: 자료관리에 필요한 클래스 및 기타 클래스**
  - Stack, Queue 등 기본적인 자료구조인 [collection](https://github.com/puzzlepcs/TIL/blob/master/Java/collection.md)이 포함되어 있다.
- java.swing: 자바의 확장된 그래픽 관련 클래스.

클래스들을 관리하기 위해 폴더와 유사한 package를 사용한다.

## 4. 사용자 정의 API
직접 작성한 클래스들을 JAR형태의 파일로 저장하여 이를 라이브러리처럼 사용할 수 있다.
