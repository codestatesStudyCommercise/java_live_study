<br>

# **쓰레드의 우선순위**

<br>

## **✅** 쓰레드의 우선순위

<br>

- Java의 각 쓰레드는 우선순위(priority)에 관한 자신의 필드를 갖고 있다.
- 우선순위에 따라 특정 쓰레드가 더 많은 시간을 작업할 수 있게, 설정한다.

<br>

### **⏺** 우선순위 관련 필드

| 필드 | 설명 |
| --- | --- |
| static int MAX_PRIORITY | 쓰레드가 가질 수 있는 최대 우선순위 명시 |
| static int MIN_PRIORITY | 쓰레드가 가질 수 있는 최소 우선순위 명시 |
| static int NORM_PRIORITY | 쓰레드가 생성될 때 가지는 기본 우선순위 명시 |

<br>

### **⏺ 우선순위 설정과 확인**

<br>

getter /setter

**`getPriority()`**

- **설정된 우선순위 값 확인**

<br>

**`setPriority(int newPriority)`**

- **우선순위 설정**
- **(단, 쓰레드 시작 전에만 우선순위 변경 가능**

<br>

예제

```java
public class Main {
    public static void main(String[] args) {

        Thread t1 = new Thread(()-> System.out.println("Doing a task: t1"));
        Thread t2  = new Thread(()-> System.out.println("Doing a task: t2"));
        Thread t3  = new Thread(()-> System.out.println("Doing a task: t3"));

        System.out.println("Priority of t1: " + t1.getPriority());
        System.out.println("Priority of t2: " + t2.getPriority());
        System.out.println("Priority of t3: " + t3.getPriority());

        t1.setPriority(Thread.MIN_PRIORITY);
        t2.setPriority(Thread.NORM_PRIORITY);
        t3.setPriority(Thread.MAX_PRIORITY);

        System.out.println("Priority of t1: " + t1.getPriority());
        System.out.println("Priority of t2: " + t2.getPriority());
        System.out.println("Priority of t3: " + t3.getPriority());

        t1.setPriority(6);
        t2.setPriority(7);
        t3.setPriority(8);

        System.out.println("Priority of t1: " + t1.getPriority());
        System.out.println("Priority of t2: " + t2.getPriority());
        System.out.println("Priority of t3: " + t3.getPriority());

        t1.start();
        t2.start();
        t3.start();

    }
}
```

<br>

**< 결과 이미지 >**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/599ee760-ae4b-444a-bed0-fa53be0d6a2d/Untitled.png)

### **⏺  우선순위의 범위**

- 1 ~ 10
- (숫자가 높을수록 **우선순위가 높다**.)

* **쓰레드의 우선순위는** 비례적인 절댓값이 아닌, **상대적인 값이다.**

→ 우선순위가 10인 쓰레드 A와 우선순위가 1인 쓰레드 B가 존재한다 가정

→ A가 B보다 10배 더 빨리 수행되는것이 아님 (절댓값 X)

→ B에 비해 A가 실행큐에 **많이 포함**되고, 더 많은 작업 시간을 할당받을 뿐임 (상대적)

<br>             

---

<br>

### **⏺  main 메서드를 수행하는 쓰레드 (**우선순위 5)

➡ 메인 메서드 내에서 생성하는 쓰레드의 우선순위는 자동으로 5

- 쓰레드가 5보다 크면 시스템은 5인 쓰레드보다 더 우선해 **CPU 스케줄링**을 해줌.
- **OS 스케줄러에 종속적**이라, **희망사항을 말하는 느낌**
    - OS 스케줄러가 최종적으로 결정
- **두개 쓰레드의 우선순위가 같을 경우**, 무엇을 우선할지 **알 수 없음**

<br>

---

<br>

## **✅**  용어사전

**프로세스 :** 간단하게 작업이라고 생각하면 됨 

OS에선, 실행중인 프로그램(Application)이라고 말한다.

**멀티 태스킹 :** 두 가지 이상의 작업을 동시에 처리하는 것

<br>

### **⏺** 멀티 프로세스

ex) 우리가 워드로 **문서작업을 하는 동시에 음악을 듣는 것 →**  OS가 프로세스마다 작업을 병렬로 처리하기에 가능하다.

<br>

- 운영체제(OS)가 CPU 및 메모리 자원을 프로세스마다 적절히 할당,

병렬로 실행시켜 실행시킨다.

- 우리 눈엔 동시 실행되는 것처럼 보여도, 실제론 엄청 빠르게 바꾸고 있었던것.

- **멀티 프로세스는 프로세스마다 운영체제로부터 할당받은 고유의 메모리를 서로 침범할 수 없다.** 

이러한 이유로 하나의 프로세스에서 오류가 발생해도 다른프로세스에 영향을 미치지 않는다. (워드에 오류났는데 엑셀이 안되는 경우는 없다.)

<br>

### **⏺** 멀티 쓰레드

<br>

**멀티 스레드 역시 멀티태스킹의 한 영역**

**멀티 스레드 :: 한 프로세스 내에서 멀티 태스킹을 할 수 있도록 만들어진 것** 

ex ) 메신져 프로세스  → 채팅 기능을 제공하면서 동시에 파일 업로드 기능을 수행

- **멀티 스레드는 공유되는 자원이 있다**
왜? 같은 어플리케이션(프로세스)이니까…  당연한 이야기임
- 그래서 **하나의 스레드에서 예외가 발생한다면 프로세스 자체가 종료될 수 있음. (메모리에 심각한 문제가 생겼는데, 다른 스레드가 접근해서 사용해버리면 안되는 느낌!)**

<br>
---
<br>

# Main 쓰레드

Java application은 JVM(Java Virtual Machine)에서 돌아가는데, 이것이 하나의 프로세스이다.

<br>

## **✅** Main 쓰레드

`public static void main(String[] args)`

<br>

- main메소드를 실행하면서 시작된다.
- 메인쓰레드의 시작점
- 메인스레드는 **main메소드의 코드 흐름**
- 메인스레드가 없으면 멀티스레드가 나올 수 없다.

<br>

### **⏺** 싱글 쓰레드 애플리케이션

- main() 메소드만 실행하는 것
- 스레드가 1개이려면,  메인스레드만 동작 해야함.

<br>

### **⏺  멀티 쓰레드 애플리케이션**

- 메인쓰레드에서 쓰레드를 생성해 실행하는 것
- 위에서 봤던 우선순위 예제도 멀티 쓰레드

<br>

![image](https://user-images.githubusercontent.com/48430781/201671367-9419d83c-f544-427a-9c24-8ec73e10a688.png)

<br>

![image](https://user-images.githubusercontent.com/48430781/201671334-e1b1855b-7429-473a-baba-f252b6aa5039.png)


<br>


## **✅** 데몬 쓰레드

- 메인 쓰레드의 작업을 돕는 **보조적인 역할**을 하는 쓰레드
- 메인 쓰레드 종료시 강제로 자동 종료 됨

→ 메인의 보조역할이라 메인이 사라지면 의미가 없어져서

일반 스레드와 큰 차이는 없다.

<br>

### **⏺ 적용 예시**

1. 워드프로세서의 **자동 저장**

2. 미디어 플레이어의 **동영상 및 음악 재생**

→ 주 스레드(워드프로세스, 미디어 플레이어, JVM)가 종료되면 같이 종료

<br>

### **⏺ 데몬스레드 사용**

- 데몬이 될 쓰레드에 `setDeamon(true)` 호출시 데몬 쓰레드가 된다.
(**start() 메소드호출 전에 ((New 상태))  호출해야함)**
- 스레드를 실행하는 start() 메소드가 호출되고 나서 setDaemon(true)를 호출하면 ***IllegalThreadStateException***이 발생

<br>

```java
public class Main {

    public static void main(String[] args) {
        AutoSaveThread autoSaveThread = new AutoSaveThread();
        autoSaveThread.setDaemon(true);  //AutoSaveThread를 데몬 스레드로 만듬
        autoSaveThread.start();

        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
        }

        System.out.println("메인 스레드 종료");

    }

    public static class AutoSaveThread extends Thread {

        public void save() {
            System.out.println("작업 내용을 저장함.");
        }

        @Override
        public void run() {
            while(true) {
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    break;
                }
                save();
            }
        }
    }

}
```

<br>

**실행결과**

작업 내용을 저장함.
작업 내용을 저장함.
작업 내용을 저장함.
메인 스레드 종료

<br>

### **⏺ start() vs run()**

| start() | run() |
| --- | --- |
| native 영역에서 새로운 Thread가 생성되며 Thread가 시작되면 run() 메서드가 실행된다. | Thread가 생성되지 않으며 그냥 run() 메서드만 실행된다. |
| 동일한 객체에서 두번이상 호출 시 IllegalThreadStateException 예외가 발생된다. | 호출수에 제한없이 계속 호출할 수 있다. |
| 멀티쓰레드로 동작한다. | 싱글쓰레드로 동작한다. |

---

<br>


### References

[https://sujl95.tistory.com/63](https://sujl95.tistory.com/63)

[https://velog.io/@bongf/study-java-whiteship-javaStudy-week10](https://velog.io/@bongf/study-java-whiteship-javaStudy-week10)

[https://codechacha.com/ko/java-thread-priority/](https://codechacha.com/ko/java-thread-priority/)

[https://gosmcom.tistory.com/19](https://gosmcom.tistory.com/19)
