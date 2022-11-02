# instanceof

## **✅ instanceof**

변수가 참조하고 있는 **객체의 실제타입을 확인**하기 위해 사용하는 연산자

- **형변환이 가능**한지 여부를 알기 위해 사용
- boolean (true/false) 타입을 이용해 결과값 반환

```java
참조변수 instanceof [타입/class명]  → 결과 : boolean
```

<br><br> 

**⏺언제 사용할까?**   (설명용으로 급하게 만든 예시입니다..)
<br>


자동차 <- 현대자동차  <-  투싼 A , B,  C (대문자는 차 종류)  —  a (인스턴스)  

현대자동차 기업이 운영하지만, 어떤차든 이용할 수 있는 서비스를 만들었음  <br>

근데 현대 자동차에만 어떤 동작을 시키려고 해


```java
if( a instanceof 현대자동차 == tru) {   
   // 어떤 동작
}
```
<br><br>

### **⏺ 상위클래스와 하위클래스의 관계**

변수의 타입 클래스가 다른 클래스를 상속받는 클래스인 경우, 상위클래스를 대상으로 instanceof 연산 수행하면, true반환

`[하위클래스instance] instanceof [상위클래스]`


![image](https://user-images.githubusercontent.com/48430781/199501265-82700006-adae-4d80-a6a2-79c5a2e719b0.png)
<br>
![image](https://user-images.githubusercontent.com/48430781/199501226-78548175-65a1-46ef-aea4-2944a13b4d68.png)


**예제코드**

```java
public class Main {
    public static void main(String[] args) {
        BreadMachine myMachine = new BreadMachine();
        System.out.println(myMachine instanceof BreadMachine);
        System.out.println(myMachine instanceof redBeanFishBread);

        BreadMachine yourMachine = new redBeanFishBread();
        System.out.println(yourMachine instanceof BreadMachine);
        System.out.println(yourMachine instanceof redBeanFishBread);

    }
    public static class BreadMachine{
        public BreadMachine(){
            //만능 빵을 만들어내는 기계 (생성자)
        }
    }

    public static class redBeanFishBread extends BreadMachine {
        public redBeanFishBread(){
            //팥빵만 생성 가능한 기계 (생성자)
        }
    }
}
```

- 코드를 보면, 자식클래스가 부모를 선택하는것을 볼 수 있음   //   (팥빵기계) extends (빵기계)

<br><br><br>


### **⏺ 인터페이스와 클래스(구현부)의 관계**

인터페이스를 구현하는 클래스의 경우 인터페이스를 대상으로 instanceof연산 수행하면, true반환

`[구현 클래스] instanceof [인터페이스]`

```java
public class Main {
    public static void main(String[] args) {
				
				//연산 수행 [class instance] instanceof [interface]
        System.out.println(myMachine instanceof Machine);
        System.out.println(yourMachine instanceof Machine);
				
				// yourMachine instanceof 연산자로 Machine 으로 바꿀 수 있음을 알았다
				// yourMachine에 myMachine을 할당해보고 출력해보자.
        myMachine.run();
        myMachine.stop();
        System.out.println();
        yourMachine.run();
        yourMachine.stop();
        yourMachine = myMachine;
        yourMachine.run();
        yourMachine.stop();

    }

    public interface Machine{
        // 인터페이스는 -- 필요한 기능과 변수를 강제함.

        // 기계의 경우 공통적으로 <동작한다. 멈춘다> 등의 기능이 있을 수 있음  
				// run() ,stop()  ...

        // 기계의 경우 공통적으로 <전원상태, 제작년도> 등의 변수가 있을 수 있음  
				// boolean onState, string date  ...

        public boolean onState =false;
        public void run();
        public void stop();

    }
    public static class BreadMachine implements Machine{
        public BreadMachine(){
            //만능 빵을 만들어내는 기계 (생성자)
        }

        @Override
        public void run(){
            System.out.println("빵기계가 동작합니다.");
        }
        @Override
        public void stop(){
            System.out.println("빵기계를 멈춥니다.");
        }
    }
    public static class redBeanFishBread extends BreadMachine {
        public redBeanFishBread(){
            //팥빵만 생성 가능한 기계 (생성자)
        }
        @Override
        public void run(){
            System.out.println("팥빵기계가 동작합니다.");
        }
        @Override
        public void stop(){
            System.out.println("팥빵기계를 멈춥니다.");
        }
    }

}
```

![image](https://user-images.githubusercontent.com/48430781/199501130-fdc5473b-73a4-4add-b715-8a372d6eb98c.png)

<br><br>
---
<br><br>
 

# (optional) Java 13. switch 연산자

# ****✅**** switch 연산자

## ****⏺ 기존 switch****

- **값을 return하고 싶으면 result 변수를 만들어 주어야 함**
- **multiple case는 지원하지 않음**
case 1:
case 2: 이런식으로 붙힘.
- **다수의 case와 break가 존재**하고, **break를 빼먹을 경우 다음 분기로 넘어가게 됨**

```java
int test(int num) {
        int result = 0;
        switch(num){
            case 1:
            case 2:
                result = 1;
                break;
            case 3:
            case 4:
                result = 2;
                break;
            default:
                result = 3;
                break;
        }
        return result;
    }
```
<br><br>

## ****⏺ Java 13. switch연산자****

 ********
 
- 문장이 아닌, 식으로 가능해서 **return값으로 사용 가능**하다.  (**switch문 뒤에 세미콜론; 쓰기**)
- 값을 return할 때 **yield 키워드** 사용 (자바 13)
- **multiple case**를 지원한다.
- **->** 사용 가능 (자바 12)

<br><br>

```java
int test(int num) {
        return switch (num) {
            case 1, 2:
                yield 1;
            case 3, 4:
                yield 2;
            default:
                yield 3;
        };
}
```


<br><br>

## **⏺ Java 12. switch 연산자**

- **:  대신**  **->** 를 사용
- **multicase : 여러 조건을  ,   로 구분해 한번에 처리** 가능
- **break문 생략 가능**
- **->**  를  사용했다면, **실행문이 2개이상이거나, 반환값이 존재할 경우**  **{ }**   를 **사용**해야 함.
- **:**  를 사용했다면, **실행문이 여러개여도**  **{ }   사용하지 않아도 됨.**

```java
public class Main {
    public static void main(String[] args) {

        System.out.println(condition_check("soso"));
        System.out.println(condition_check("sad"));
        System.out.println(condition_check("happy"));

        System.out.println(condition_check2("soso"));
        System.out.println(condition_check2("sad"));
        System.out.println(condition_check2("happy"));
    }
		
		// -> 사용  
    public static String condition_check(String emotion){
        return switch (emotion){
            case "happy", "fun" -> "best";
            case "sad", "angry" -> "not good";
            default -> "--";
        };
    }

		//yield 사용
    public static String condition_check2(String emotion){
        return switch (emotion){
            case "happy", "fun": yield "best";
            case "sad", "angry": yield "not good";
            default: yield "--";
        };
    }
}
```

<br><br><br><br>


---

### References

[https://gintrie.tistory.com/63](https://gintrie.tistory.com/63)

[https://logical-code.tistory.com/151](https://logical-code.tistory.com/151)

[https://velog.io/@eledev/JAVA-STUDYwith-whiteship-3주차](https://velog.io/@eledev/JAVA-STUDYwith-whiteship-3%EC%A3%BC%EC%B0%A8)

[https://castleone.tistory.com/6](https://castleone.tistory.com/6)
