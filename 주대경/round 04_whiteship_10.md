# 프로세스

Process

- 사용자가 작성한 프로그램이 운영체제에 의해 메모리 공간을 할당받아 실행 중인 프로그램.
- 프로그램에 사용되는 데이터와 메모리 등의 자원 그리고 스레드로 구성.
- 프로세스끼리는 정보를 주고받을 수 없음.

# **스레드**

Thread

- 프로세스(process) 내에서 독립적으로 실행되는 하나의 작업 단위 혹은 실제로 작업을 수행하는 주체.
- 모든 프로세스에는 한 개 이상의 스레드가 존재하여 작업을 수행.
- 두 개 이상의 스레드를 동시에 실행시도록 작성하는 기법 프로세스를 멀티스레드 프로세스(multi-threaded process)
  멀티 스레드 작업 시에는 각 스레드끼리 정보를 주고받을 수 있어 처리 과정 오류를 줄이고, 작업 속도를 높일 수 있음.

### Thread in Java

JVM에 의해 하나의 프로세스가 발생하고 `main()`가 하나의 스레드.

`main()`이외의 또 다른 스레드를 만들려면 `Thread` 클래스를 상속하거나 `Runnable` 인터페이스로 구현 가능.

## Thread 클래스와 Runnable 인터페이스

자바에서 스레드를 구현하는 방식에는 두 가지 존재.

java.lang.Thread
java.lang.Runnable

```java
// Thread 클래스 상속
class MyThread extends Thread {
	public void run() {} // 부모 Thread 클래스의 run 메소드를 오버라이딩
}

// Runnable 인터페이스 구현
class MyThread implements Runnable {
	public void run() {} // Runnable 인터페이스의 run 메소드 구현
}
```

결국 run 메소드를 어떻게 구현하느냐일뿐 기본적으로는 동일 하지만 몇 가지 차이점이 존재

## **차이점**

- Thread 클래스로 상속 받으면 다른 클래스를 상속 받을 수 없기 때문에 Runnable을 일반적으로 사용.
- 인스턴스 생성 방법

  ```java
  // Thread   => MyThreadT
  // Runnable => MyThreadR

  MyThreadT t1 = new MyThreadT();

  Runnable r = new MyThreadR();
  Thread t2 = new Thread(r)
  ```

  Thread 클래스 상속으로 구현한 클래스의 경우 getName() 같은 내부 메소드를 바로 호출가능.
  Runnable 구현 클래스는 Thread.currentThread().getName() 정적 메소드로 호출가능.

  ```java
  public class App {
      public static void main(String[] args) {
          MyThreadT t1 = new MyThreadT();

          Runnable r = new MyThreadR();
          Thread t2 = new Thread(r);

          t1.start();
          t2.start();
      }
  }

  class MyThreadT extends Thread {
      public void run() {
          for (int i = 0; i < 5; i++) {
              System.out.println(getName());
          }
      }
  }

  class MyThreadR implements Runnable {
      public void run() {
          for (int i = 0; i < 5; i++) {
              System.out.println(Thread.currentThread().getName());
          }
      }
  }
  ```

  ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3376e4f2-e837-4bb1-b462-063cd4e1cc17/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221103%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221103T150035Z&X-Amz-Expires=86400&X-Amz-Signature=3d85c20ed7bf152e6cc2099cb208c08d7f35090372c97e20a2ebcbdba6fa164c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

  ## 스레드의 상태

  스레드는 생성된 후부터 종료될 때까지 여러 상태를 가질 수 있음.(Life Cycle)
  | 상태 | 설명 |
  | ------------------------------------------- | -------------------------------------------------------------------- |
  | NEW | 스레드가 생성되고 아직 start()가 호출되지 않은 상태 |
  | Runnable | 실행되기위한 준비 단계 |
  | Running | 스레드가 실행중인 상태 |
  | blocked | 동기화블럭에 의해서 일시정지된 상태 |
  | Waiting, |
  | Timed_Waiting | 쓰레드의 작업이 종료되지는 않았지만 실행가능하지 않은 일시정지 상태. |
  | Timed_Waiting은 일시정지 시간이 지정된 경우 |
  | Terminated | 스레드의 작업이 종료된 상태 |
  ![study.drawio.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e9714170-1c47-4d0f-880b-3e664cd19dfd/study.drawio.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221103%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221103T150117Z&X-Amz-Expires=86400&X-Amz-Signature=e4008c32d435bd95e9eb88894dcef20fab797985bac76a3a089ccc3f0b042253&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22study.drawio.png%22&x-id=GetObject)

  [추가 예제](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=qbxlvnf11&logNo=220921178603)
