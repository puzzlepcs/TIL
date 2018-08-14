# Android Application UI
## 1. User Interface

- Android Application에서는 View와 ViewGroup 객체를 이용하여 UI를 만든다.
- Android 화면의 기본 단위는 Activity이다. 그 자체로는 아무것도 보여주지 않는다.  


![img1](https://github.com/puzzlepcs/TIL/blob/master/android/img/ui01.PNG)  

- View class
  - UI의 가장 기본적인 단위
  - Widget의 기본 클래스-TextView, EditText, Button, RadioButton, CheckBox등 interactive UI component
- ViewGroup class
  - 전체를 포함하는 컴포넌트를 Layout을 넣고, 이 안에 addView()등을 이용해 View 요소들을 배치시킨다.
  - 다양한 형태의 View들의 집합
  - `addView(View)`메소드로 view 추가
  - Layouts의 기본 클래스- ViewGroup을 가지고 있는 invisible containers
  - widget뿐만이 아니라 layout을 포함할 수 있다. (Java의 Conversit 패턴구현)

### 1.1 View class
모든 UI 요소의 부모 클래스이다.

`onDraw()`메소드: UI를 화면에 그려주는 메소드.
`width, height`
  - 안드로이드에서는 이러한 값을 유동적으로 설정할 수 있게끔 한다.  
  - 반응형 웹디자인
  - 상대값을 주어 디자인을 해야 다양한 사이즈의 화면에 맞을 수 있다.
  - match_parent: 부모 클래스의 크기에 맞추기
  - wrap_content: widget의 content의 크기에 맞추기




### 1.2 Attribute ID의 사용
Java 파일로 가지고 와서 유동적으로 변동해야 할 때, UI마다 ID를 부여하여 그 ID로 Java코드에서 View 객체를 불러올 수 있다.
- 선언
  - `@id`의 경우 id가 이미 리소스에 존재하는 경우 불러온다는 뜻이며, `@+id`의 경우 새로운 값을 만든다는 의미이다.
```
id="@+id/first_button"
```

- 사용  
xml파일의 View요소들을 Java파일에서 사용할 수 있도록 `findViewById()`메소드를 사용하여 그 객체를 불러온다.
```
Button firstButton = (Button)findViewById(R.id.first_button);
```

## 2. UI Event
View 클래스에는 Event 처리 기능이 있기 때문에 모든 UI는 Event를 발생시킬 수 있다.
특정 Event가 발생하면 Event source에서 특정 메소드를 호출하도록 Andriod Framework에 요청한다.

Event를 처리하기 위해서는 다음의 세가지를 결정하고 이에 따라 구현해야 한다.
- EventAction
  - 어떤 이벤트가 발생하였을 때 반응할지 결정해야 한다.
- EventSource
  - View 클래스에 존재한다.
  - Event가 오는 것을 기다린다.
  - Evnet가 오면 Event Listener에게 이벤트가 발생하였다고 알려준다.
  - 모든 UI는 Event Source가 될 수 있다.
- EventListener
  - View 클래스에 nested interface로 존재한다.
  - 이벤트를 핸들링하는 메소드들을 오버라이드 하여 작성해주어야 한다.


### 2.1 Event Handling 예제 코드
1. 해당 Activity에 EventListener를 implement 하기
```
public class UITest extends AppCompatActivity implements View.OnClickListener{
    TextView tv;
    EditText et;
    Button b;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_uitest);
        et = findViewById(R.id.first_edit);
        tv  = findViewById(R.id.first_text);
        // Event Source
        b = findViewById(R.id.first_button);
        b.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        String s = et.getText().toString();
        tv.setText(s);
        Log.e("UITest", "click.....");
    }
}
```
2. Activity안의 멤버 클래스에 EventListener를 implement하기
```
public class UITest extends AppCompatActivity {
    TextView tv;
    EditText et;
    Button b;

    // Event Listener
    class MyClick implements View.OnClickListener {
        @Override
        public void onClick(View v) {
                String s = et.getText().toString();
                tv.setText(s);
                Log.e("UITest", "click.....");
        }
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_uitest);
        et = findViewById(R.id.first_edit);
        tv  = findViewById(R.id.first_text);

        // Event Source
        b = findViewById(R.id.first_button);
        b.setOnClickListener(new MyClick());
        //b.setOnClickListener(this);
        //MyClick click = new MyClick();
    }

}
```
3. 내부에서 바로 구현해주기
어떤 UI가 어떤 Event action이 발생했을 때 어떤 Event Handler가 어떻게 처리하는지 한눈에 볼 수 있기 때문에 가독성이 좋다.
```
public class UITest extends AppCompatActivity {
    TextView tv;
    EditText et;
    Button b;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_uitest);
        et = findViewById(R.id.first_edit);
        tv  = findViewById(R.id.first_text);

        // Event Source
        b = findViewById(R.id.first_button);

        // unannounced 내부클래스
        View.OnClickListener click = new View.OnClickListener(){
            @Override
            public void onClick(View v) {
                String s = et.getText().toString();
                tv.setText(s);
                Log.e("UITest", "click.....");
            }
        };
        b.setOnClickListener(click);
    }
}
```
혹은 다음과 같이 객체생성을 메소드 안에서 바로 할 수 있다.
```
b.setOnClickListener(new View.OnClickListener(){
    @Override
    public void onClick(View v) {
        String s = et.getText().toString();
        tv.setText(s);
        Log.e("UITest", "click.....");
    }
});
```
4. xml파일에 처리해주기
가독성이 떨어지고, Click 이벤트만 처리해 주기 때문에 이 방식보다 위의 방법을 사용하는 것을 추천한다.
```
<Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/first_label"
        android:id="@+id/first_button"
        android:onClick="handler"/>
```
Button이 클릭되면 해당 Activity의 `handler()` 메소드가 수행된다.
