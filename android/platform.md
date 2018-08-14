# Andriod 파일구조
## 1. Andriod Application 실행 구조
빌드할 때 `.class`파일이 `.dex`파일이 됨
resource파일들이 `resources.arsc`라는 하나의 파일로 컴파일된다.
이 두개의 파일을 합처서 `.apk`파일이 된다. 이 파일은 안드로이드 프레임워크에서 실행되는 것이기때 문에 일반 pc에서는 실행하지 못한다.
`.apk`파일을 프레임워크(패키지 매니저가 인스톨을 관리, 인스톨 시 리소스 파일 중 `AndroidManifest.xml`에서 실행시 필요한 값들을 table에 저장함.)
런처라는 애플리케이션에서 해당 앱을 실행 하면 ActivityManager가 실행되고, ActivitiyManager가 PackageManager로부터 해당 앱의 실행 값들을 불러오고 실행하게 된다.

Node마다 객체를 생성하는 것과 같고, Node의 속성은 그 객체의 메소드이다.

## 2. 리소스 관리
### 2.1 AndroidManifest.xml
Application구성과 관련된 정보를 담고 있는 파일이다. build시 사용된다.

```
...
<activity android:name=".MainActivity">
           <intent-filter>
               <action android:name="android.intent.action.MAIN" />

               <category android:name="android.intent.category.LAUNCHER" />
           </intent-filter>
</activity>
...
```

프레임워크에게 알려줘야 하는 내용을 이 파일에 작성한다. 프레임워크가 앱에서 조작해줘야 하는 내용들을 알려 주어야 한다. Activity의 LifeCycle을 프레임워크가 직접 관리하기 때문에 앱에 여러개의 화면이 있어도, 위와 같이 intent filter를 사용하여 가장 먼저 실행할 Activity를 특정하면 그 Activity를 프레임워크가 실행해준다.

### 2.2 res - 리소스 파일 저장
Application에서 필요한 그림, 멀티미디어, 레이아웃, 문자열 등 다양한 리소스를 관리하기 위한 폴더이다. 다음과 같은 파일들이 있다.
  - drawable
  - strings
  - colors

**안드로이드에서는 source와 Resource를 완벽하게 분리하여 따로 관리한다.** 이로 인해 개발 생성성이 좋아진다. 리소스가 변해도 기존의 코드는 동일한 것을 사용할 수 있다. 모든 리소스는 xml파일에 저장하여 관리한다.
- Java에서 리소스로 접근하려면 `R`클래스로 접근한다.
  - final - 상속받지 않음
  - 자동적으로 리소스 마다 id값을 추가한다(추가된 id값은 final 키워드가 붙는 상수이다). 프레임워크는 이러한 리소스 id값을 가지고 리소스파일에 접근하여 이를 사용하게 된다.
- 리소스 파일에서 리소스 파일로 접근시 `@`를 사용하면 된다.

### 2.3 gradle
compile 정보 저장
