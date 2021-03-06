# 2018 Summer MultiCampus - Computer Science

스마트폰과 피쳐폰의 차이점은 무엇일까?
원하는 어플리케이션을 사용할 수 있는가 없는가로 구분할 수 있다. 스마트폰에는 프로그램을 다운받고 사용하는 것이 가능하지만 피쳐폰은 불가능하다. (일종의 개인화라고 볼 수 있음)  

이 과정에서는 JAVA를 기반으로한 클라이언트측 플랫폼 개발하는 것에 집중할 것임.

## 기술의 흐름
Server/Client ->  Web -> Mobile -> IoT => Personalized Service
기술의 수명은 기술의 전파속도와 비례.
C -> C++ -> C# (마이크로소프트에서 웹 프로그래밍을 위해 개발)

### 웹(Server/Client)
네트워크의 발달로 등장. 서버에 접속하는 클라이언트 프로그램을 브라우저로 통일. 굉장히 많은 사용자들을 네트워크에 동원(시장의 확대).
* 프론트엔드(클라이언트): HTML(Document), CSS, Javascript(Browser에서 구동되는 언어) => Node.js, JQuery
* 백엔드(서버): JAVA -> Sublet, JSP, ASP => JSpirng(Framework 구축)

#### 수익구조 - 수혜자 vs 제공자
##### 구글과 야후
* 구글
서비스의 수혜자들에게 돈을 받는 것이 아니라, 서비스를 제공하는 사람들로부터 수익을 얻는 구조. 히트율과 비례하여 광고비를 받는 구조.
'모든 데이터들이 구글을 통한다.'라는 말이 있을 정도로 웹 시장을 독점.
브라우저 시장을 살펴보면 Chrome은 Javascript엔진(V8엔진)울 사용. 웹 1.0 시대에서 App시대로 넘어갈때 빠른 구동속도로 또 시장을 선점한다.
* 야후
유료화 정책 -> 배너 광고. 느린 실행속도와 유저들의 마음이 떠나 결국 시장에서 도태됨.
##### 싸이월드, 아이러브스쿨은 왜 성공하지 못했을까
싸이월드는 데이터가 부족해서 성공하지 못했다기 보다는 그 데이터를 공유하지 않아 성공하지 못했다고 할 수 있다.
또한 그 수익구조가 성공한 트위터와 페이스북과 달랐다.  
아이러브스쿨 같은 경우, 서비스를 제공받는 사람들(서비스 수혜자)로부터 수익을 얻는 구조로 전환하였고 유저들이 떠나가 서비스를 종료하였다.

싸이월드와 SK의 OK Cashback 서비스
SK의 입장에서 유저들의 포인트는 부채이고, 이 부채를 싸이월드에서 소모할 수 있게끔 함.

### Mobile
언제 어디서나 네트워크에 접속할 수 있음 (유비쿼터스 시대)
* 안드로이드 -> 구글에서 선점. JAVA의 재등장. 구글에서 또 모바일 시장을 선점하게 되었다. 안드로이드 플랫폼을 사용함으로서 검색엔진(웹서비스) 시장을 독점하게 됨.
#### 마이크로소프트에서 모바일시장에 성공적으로 진출하지 못 한 것은?
* MS는 모바일 폰을 만들었을 때, 이를 PC처럼 생각함.
* UI측면: 모바일 화면 구성을 컴퓨터의 축소판이라고 여김. 화면이 작아지면 글씨와 이미지가 커져야 한다.
  * 애플은 Input device를 키보드에서 마우스로, 마우스에서 손가락으로 전환시킴. Click을 Swipe로 바꿈.
이러한 요인들 떄문에 MS는 모바일 시장에 진출하지 않고, 클라우드 컴퓨팅시장으로 진출하게 된다.

### IoT
모든 사물에 인터넷을 연결. 방대한 양의 데이터 수집 가능. (Big Data -> Personal Service의 기반)
* AI를 이용한 Big Data의 처리. (서버측 기술) => 이를 클라이언트측에 제공. 클라이언트에 어떻게 제공하는지, 어떤 플랫폼을 사용하는지에 관한 고민을 해볼 것.
* Andriod의 분화 -> 핸드폰, TV, wearables, auto, RasberryPie(오픈서킷보드)

## 운영체제와 안드로이드
### OS란
프로세스를 실행해주는 프로그램. general purpos computer의 등장으로 하드웨어의 제어가 필요해짐. 결국 app이라는 것은 OS의 보조기능.
* 모든 OS는 리눅스라고 할 수 있을 정도로 리눅스가 OS시장을 독점하고 있다. 안드로이드의 OS는 리눅스 기반.
### 안드로이드 구현 방식
* Native : 제공되는 기본 라이브러리를 사용하여 개발. 기기마다 앱을 개발해야 함. => 이 방식을 이용해 개발. 퍼포먼스 문제
* Hybrid : 화면은 HTML을 사용하고, 기능은 JavaScript로 구현. => 퍼포먼스가 떨어짐.
* Web-App : 안드로이드앱을 브라우져로 개발. (OS무관. Client기반)

## DB
데이터를 저장하기 위해 1950년대에 등장. 데이터가 필요할 때 데이터를 잘 찾을 수 있게끔 저장. DBMS는 1970년대에 등장하기 시작.
### 데이터를 저장하는 방식
* HDB(Heirarchical DB): (주로 File System에 사용) 각각의 노드에 데이터를 저장. 노드의 성격에 맞는 데이터를 저장.
  * 장점: Simple
  * 단점: 항상 정렬이 되어있어야 함(노드의 삽입, 삭제). 데이터 자체에는 순서라는 것이 없음. 데이터 자체의 특성이. 데이터의 변화에 취약.
* NDB(Network DB): 데이터를 평면으로 배치. 노드들 간의 관계를 설정해야함. 실제로 상용화되지 못함
  * 장점: 데이터 변화에
  * 단점: 노드들 관의 관계를 구축하는 것이 어려움. 노드들간의 삽입과 삭제시 인터페이스를 전명
* RDB(Relational DB): 최근에 사용하는 기본 DBMS. 각각의 데이터를 어떠한 하나의 기준치를 두어 묶고 이를 노드라고 함. 노드와 노드간의 한개 이상의 속성을 공유함. Oracle, SQL

### 데이터의 종류
* 정형데이터: 이미 정제가 되어있는 데이터. 기존의 방식
* 비정형데이터: 정제되어있지 않은 데이터. 이러한 데이터를 관리하기 위해 Big Data라는 개념의 등장.

## 네트워크
두개의 Pier인 Caller(Client)와 Callee(Server)간의 소통. 네트워크에 연결하게 되면 물리적으로 연결되는 것 뿐만이 아니라 논리적으로 서버와 클라이언트 간의 약속을 맺어야 소통이 가능하다. 이러한 논리적인 약속을 프로토콜이라고 한다.
* Protocol
  * TCP/IP: 전송계층을 담당하는 프로토콜 중의 하나. 연결지향성(클라이언트가 연결을 요청하면, 연결을 끊기 전 까지 계속 연결을 유지함. 서버에게 부담. 동시접속자수가 한정되어 있음. 한 서버당 약 200~300명의 동시접속자까지 수용할 수 있음.)
  * HTTP: 연구원들 사이의 파일 전송을 위해 버너스 리가 개발. 비연결성 프로토콜. 파일을 보낼 때만 연결을 유지함.
    * 데이터 통신 시 콘텐츠만 전송하면 이 데이터가 무슨 의미인지 알 수 없음. 데이터에 관한 정보인 메타데이터를 함께 전송.
    * 메타데이터의 표준화, sgml- 시작과 끝을 알리는 Tag의 개념 (eg. <Head, script='hello.js'></Head>)
    * 하이퍼 링크 개념의 도입 -> Hypertext meta language
    * HTML형태의 문서를 보여주는 뷰어의 개발: Mosaic -> Escape
  * FTP: 파일전송을 위한 프로토콜을
  * Telnet
* 물리계층
  * Ethernet
  * Internet: 어떠한 중앙 서버를 두지 않고, 각각의 컴퓨터가 노드가 되어 서로 연결을 유지할 수 있음. TCP/IP 프로토콜을 사용
이러한 네트워크의 기술의 발전으로 웹 시대가 열리게 된다.

## 소프트웨어 공학
고객의 니즈를 맞춰준다는 점에서 IT는 서비스업이라는 말을 할 수 있다.
### 개발 방법론 - 폭포수 모델
다음의 단계를 반복하여 개발한다.
* 계획
* 요구사항 분석
* 설계
* 구현
* 테스트
* 설치 및 유지 보수

커뮤니케이션리스크;
