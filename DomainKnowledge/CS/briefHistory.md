# 2018 Summer MultiCampus - Computer Science

스마트폰과 피쳐폰의 차이점은?? 원하는 어플리케이션을 사용할 수 있는지에 여부. 스마트폰에는 프로그램을 다운받고 사용하는 것이 가능하다. (일종의 개인화라고 볼 수 있음)

이 과정에서 JAVA를 기반으로 클라이언트 측의 플랫폼

## 기술의 흐름
Server/Client ->  Web -> Mobile -> IoT => Personalized Service

C -> C++ -> C# (마이크로소프트에서 웹 프로그래밍을 위해 개발)

### 웹(Server/Client)
* 프론트엔드(클라이언트): HTML(Document), CSS, Javascript(Browser에서 구동되는 언어) => Node.js, JQuery
* 백엔드(서버): JAVA -> Sublet, JSP, ASP => JSpirng(Framework 구축)

### Mobile
언제 어디서나 네트워크에 접속할 수 있음 (유비쿼터스 시대)
* 안드로이드 -> 구글에서 선점. JAVA의 재등장

### IoT
모든 사물에 인터넷을 연결. 방대한 양의 데이터 수집 가능. (Big Data -> Personal Service의 기반)
* AI를 이용한 Big Data의 처리. (서버측 기술) => 이를 클라이언트측에 제공. 클라이언트에 어떻게 제공하는지, 어떤 플랫폼을 사용하는지에 관한 고민을 해볼 것.
* Andriod의 분화 -> 핸드폰, TV, wearables, auto, RasberryPie(오픈서킷보드)

### 안드로이드 구현 방식
* Native : 제공되는 기본 라이브러리를 사용하여 개발. 기기마다 앱을 개발해야 함. => 이 방식을 이용해 개발. 퍼포먼스 문제
* Hybrid : 화면은 HTML을 사용하고, 기능은 JavaScript로 구현. => 퍼포먼스가 떨어짐.
* Web-App : 안드로이드앱을 브라우져로 개발. (OS무관. Client기반)
