# Thread
자바에서 스레드는 힙과 클래스 영역을 공유함
 top frame만 스케줄러가 작업해줌.
 n개의 메소드가 실행됨. 제일 위에 있는 메소드만 실행
 스레드를 만들면 스택이 새로 생성이 되는 거임~~
 스레드별로 스택이 생성되어 각각의 top 메소드를 실행.

```
Thread th = new Thread();
th.start();
```


스레드 종료방법
1. 런 메소드를 다 종료해서
2. 예외 발생 -> try-catch-finally문으로 처리



### Multi Thread & Concurrent Issue

lock flag 취득 - synchronized 블록


### 스레드 생성
```
//	1. 스레드 클래스 상속
class My1 extends Thread {
	@Override
	public void run() {
		super.run();
	}
}

// 2. 인터페이스 구현
class My2 implements Runnable {
	@Override
	public void run() {

	}
}

public class Thread5 {
	public static void main(String[] args) {
		My1 th1 = new My1();
		th1.start();

		Thread th2 = new Thread(new My2());
		th2.start();

		// 3. 인터페이스 객체화
		Runnable r = new Runnable() {
			public void run() {

			}
		};
		Thread th3 = new Thread(r);
		th3.start();

		// 4. 한번에
		Thread th4 = new Thread(new Runnable() {
			public void run() {}
		});

    // 5.
    Thread th5 = new Thread() {
      public void run() {};
    };
    th5.start();

    // 6.
    new Thread() {
      public void run() {};
    }.start();
  }
}
```

### priority setting
```
public class PriThread extends Thread {
	public PriThread(String name){
		super(name);
	}
	public void run(){
		for(int i=0;i<5;i++){
			System.out.println(getName() + "가 출력:"+i);
			//try{
			//	sleep(1);
			//}catch(InterruptedException e){}
		}
	}
	public static void main(String args[]){
		PriThread p1, p2, p3;

		p1 = new PriThread("max");
		p2 = new PriThread("norm");
		p3 = new PriThread("min");

		p1.setPriority(Thread.MAX_PRIORITY);  //10
		p2.setPriority(Thread.NORM_PRIORITY); //5
		p3.setPriority(Thread.MIN_PRIORITY);  //1
		System.out.println(p1.getName() + " 우선순위 : "+p1.getPriority());
		System.out.println(p2.getName() + " 우선순위 : "+p2.getPriority());
		System.out.println(p3.getName() + " 우선순위 : "+p3.getPriority());

		p3.start();
		p2.start();
		p1.start();
   }
}
```


안드로이드는 기본적으로 멀티 스레딩! 11개의 스레드가 돌아간다.
대표적으로 시간이 많이 걸리는 네트워킹은 스레딩이 꼭 필요하다.
스레드를 만드는 방법 알아둘 것


## Runnable vs Thread
Runnable은 interface이므로 다른 클래스를 상속 받고, 이를 스레드 처럼 사용하고 싶을 때 사용할 수 있다.

## Daemon Thread
- `t.setDaemon(true)` 메인 스레드가 종료되면 같이 종료함.
