

# **✅** 함수형 인터페이스

하나의 **추상메소드**만 선언된 인터페이스

- @FunctionalInterface가 있으면 좋음
- 
복습) 추상메서드 - 선언중에 구현이 필요하지 않고, 인터페이스를 구현하는 클래스에 의해 무조건 재정의 되어야하는 메서드

<br>

## **⏺ 일단 함수형 프로그래밍이 무엇인지부터 알아보자.**

- 명령형이 아닌 **선언적 방식**으로 구현
    - **명령형 프로그래밍 : 프로그래밍의 상태와 상태를 변경시키는 구문의 관점에서의 연산을 설명**
        - 절차 지향 프로그래밍 : 수행되어야 할 연속적인 계산 과정을 포함(C, C++)
        - 객체 지향 프로그래밍 : 객체들의 집합으로 프로그램의 상호작용을 표현(C++, Java, C#)
    - **선언형 프로그래밍 : 어떻게(HOW) 할 것인가 보다는 무엇(WHAT)을 할 것인가를 표현**
        - 함수형 프로그래밍 : 순수 함수를 조합하고 프로그램을 만드는 방식(Clojure, Haskell, Elixir)
- 흐름제어를 명시적으로 기술하지 않고 프로그램 로직이 표현된다

<br>

## **✔️ 함수형 프로그래밍의 특징**

<br>

### **불변성 (순수함수)**

- **상태를 변경하지 않는다.**
- 상태 변경시 **부수 효과**가 생겨 **순수함수**의 조건을 만족할 수 없음
    
    <aside>
    💡 부수효과(Side Effect)
    
    - 콘솔에 출력하거나 사용자의 입력을 읽는 것
    - 변수를 수정하거나, 객체의 필드를 저장하는 것
    - 예외를 던지거나 오류를 발생시키며 실행을 중단하는 것
    - 파일에 읽고 쓰는 작업
    </aside>
    
    <aside>
    💡 순수함수
    
    - 같은 입력에 대해 같은 출력을 반환하는 함수
    - 부수효과가 없는 함수
    - 함수의 실행이 외부에 영향을 끼치지 않음
    </aside>
    
<br>

### 참조 투명성

프로그램 변경 없이 **어떤 표현식을** **값으로 대체 가능**

<br>

### 일급객체/ 고차함수

- **함수의 매개변수로 함수를 전달**할 수 있다.
- **함수의 리턴값으로 함수를 사용**할 수 있다.
- 변수나 자료구조에 함수를 담을 수 있다.

<br>

### 익명 함수

- 이름이 없는 함수
- 람다식으로 표현되는 함수 구현

<br>

### 게으른 평가

- 함수형언어가 아닌것들은 실행 즉시 값을 평가함
- 함수형에선 **값이 필요한 시점**에 평가한다.


<br><br>

## **⏺ JAVA - 함수형 인터페이스를 사용하는 이유**

[quora.com/Why-do-we-need-Functional-interface-in-Java](http://quora.com/Why-do-we-need-Functional-interface-in-Java)

- Java엔 실제로 function이라는게 없다.
클래스에 속한 함수인 메서드가 존재할 뿐이다.
- 메서드는 객체가 아니다
- 클래스에 속하는 함수인 **정적 메서드** 역시 객체가 아니다.
- 결국 자바에서는 어떤 함수(메서드)를 사용하려면  객체가 필요하다.

- 만약 함수형 인터페이스가 없다면, 익명 클래스를 사용해야한다. 익명클래스에 비하면 함수형 인터페이스가 코드가 더 읽기 쉽다.
- 익명클래스 대신 람다식을 사용해서 인스턴스화할 수 있다는게 가장 큰 장점이다.

<br>

```java
public class AnonymousClassExample {
	public static void main(String[] args) {
    Thread thread = new Thread(){
        public void run(){
            System.out.println("Understanding what is an anonymous class");
        }
    };
    thread.start();
	}
}
```

<br>

```java
public class AnonymousClassExample {
	public static void main(String[] args) {

    Runnable runnable = () -> {
        System.out.println("Understanding functional interfaces");
    };
    runnable.run();
	}
}
```

<br>

—  대부분 함수형에서 사용할 법한 함수 디스크립터는 비슷

그래서 **JAVA8 라이브러리 설계자들은 java.util.function에 미리 사용할 법한 함수 인터페이스를 정의했다.**

<br>

- 자주 사용되는 인터페이스

![image](https://user-images.githubusercontent.com/48430781/203315509-0928ec75-b74d-4f37-85a6-734df6118715.png)


<br>

- 매개변수가 2개인 함수형 인터페이스

![image](https://user-images.githubusercontent.com/48430781/203315553-fd429c5e-39f6-41a0-b13f-f01fbf01d734.png)


<br>

- 매개변수타입과 반환타입이 일치하는 함수형 인터페이스

![image](https://user-images.githubusercontent.com/48430781/203315593-b9c13f64-5e57-46a4-b007-f66e9ca147a9.png)


<br>

응용

→  [https://doohyun.tistory.com/15](https://doohyun.tistory.com/15)

<br>

```java

public class Main {
    public static void main(String [] args){

        /*
				미리 정의된 인터페이스 예시
        @FunctionalInterface
        public interface BinaryOperator<T> {
            T createObject(T t1, T t2);
        }
        */

        //예제
        BinaryOperator<Integer> intSum = (Integer a, Integer b) -> a+b;
        Integer res1 = intSum.apply(3,5);

        //실습
        BinaryOperator<String> pairReminder = (String a, String b) -> {
            return a + "님, " + b + "님 오늘 페어로 매칭되었습니다!";
        };

        String[] reminder = new String[]{};

        ArrayList<Pair> pairList = new ArrayList<>(){};
        pairList.add(new Pair("강지은","김례화"));
        pairList.add(new Pair("전진우","곽훈정"));

        for (int i=0;i<pairList.size();i++){
            String result = pairReminder.apply(
										(String) pairList.get(i).getOne(), 
										(String) pairList.get(i).getTwo()
						);
            
						System.out.println(result);
        }

    }

}

class Pair<T>{
    T one, two;
    Pair (T one, T two){
        this.one = one;
        this.two = two;
    }

    public T getOne() {
        return one;
    }

    public T getTwo() {
        return two;
    }
}

```

<br>

![image](https://user-images.githubusercontent.com/48430781/203315682-3260066b-2230-49bb-946e-8f47b6c3f758.png)

<br>

ex) Runnable인터페이스 - run()만 명시되어있음.

Runnable클래스의 구현체를 Thread의 생성자로 넘겨줬었어야했는데 

이젠 무명클래스를 통해 Thread 생성자를 넘겨줄 수있다. 

<br>

```java
public static void main(){
        //기존 방식
        Thread t1 = new TestThread();
        Runnable r1 = new TestRunnable();
        Thread t3 = new Thread(r1);

        //익명 클래스를 이용한 생성
        Thread t4 = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("Hello!");
            }
        });

        //람다식을 이용한 스레드 생성
        // 추상메서드가 한개밖에 없는 함수형인터페이스이기 때문에 이런 형태가 가능해짐
        Thread t5 = new Thread(() -> System.out.println("Lambda Hello"));
        t5.start();
    }
```

<br>


### **⏺ 람다식과 익명 클래스**

<br>

```java
//익명 클래스
DrinkAble drink = new DrinkAble() {
    @Override
    public void Info() {
        System.out.println("안녕 나는 음료수");
    }
};
drink.Info();

//람다식
DrinkAble drink2 = ()->{ System.out.println("안녕 나는 음료수"); };
drink2.Info();
```

<br>

**1. this 키워드의 사용**

<br>

- **람다식의 this** ::  **람다식이 작성된 클래스**를 가리킴
    - 만약 **람다식**이 Main 클래스 내부에 작성이 되어 있다면, 
    this ::   메인 클래스를 가리킴
- **익명 클래스에서의 this** 는   ::  **익명 클래스 자신**을 가리킴

<br>

```java
public class Main {
    public static void main(String [] args){

        Test test = new Test();
        test.gettestThis();
        test.drinkTest();
		}
}

class Test{

    void gettestThis(){
				System.out.println();
        System.out.println("안녕 나는 테스트 클래스");
        System.out.println("this:" + this);
    }

    void drinkTest(){
        DrinkAble drink = new DrinkAble() {
            @Override
            public void Info() {
                System.out.println();
                System.out.println("안녕 나는 음료수");
                System.out.println("this:" + this);

            }
        };

        drink.Info();

        DrinkAble drink2 = ()->{
            System.out.println();
            System.out.println("안녕 나는 음료수 2번 ");
            System.out.println("this:" + this);

        };

        drink2.Info();

    }
}
```

<br>

![image](https://user-images.githubusercontent.com/48430781/203315833-0a3b0bdd-11ea-4126-89b0-67176e1a7b6e.png)

//  테스트클래스의 this와  음료수 2번의 this 주소값이 같은 것을 확인할 수 있다. 

<br>


### ⏺ **람다식의 내부 동작과정**

**컴파일 방식**

<br>

<aside>
💡 ### 컴파일 타임에 일어나는 일 ###

1. 람다식은 컴파일 타임에 클래스가 정의되지 않고 **런타임에 JVM이 하도록 떠넘긴다**. 
대신, 그 **레시피만을 제공**

2. 레시피 : invokedynamic 바이트코드
레시피의 3가지 준비물 :
bootstrap method
static args
dynamic args

3. bootstrap method :  LambdaMetafactory.metafactory()

4. static args로는 **람다식이 구현하는 인터페이스**와 **람다식 코드를 그대로 복사해
새 private static method를 생성**, 이를 전달함

5. dynamic args로는 **자유 변수(~= 지역변수)**들을 전달한다.

 이제 남은 것들은 런타임 - JVM의 몫이 됨.

</aside>

<br>

<aside>
💡 ### 런타임에 일어나는 일 ###

1. JVM은 컴파일 타임에 만들어진 레시피대로 
bootstrap method에 static args, dynamic args를 넘겨, 
**`람다식이 실행되는 시점`**에 **`동적으로 클래스를 정의`**하고 **`그 객체를 생성해 반환`**한다.

2. JVM이 동적으로 정의한 **람다 클래스**는
                                            →  **static args로 넘겨 받은 타겟 인터페이스를 구현**한다.

3. JVM이 동적으로 정의한 람다 클래스는

실행 메소드(Runnable의 경우 run)에서, 
컴파일 타임에 본래 클래스에 생성된, 
람다식 내부 코드를 담은 private static method를 호출한다.

4. 호출된 본래 클래스의 private static method가 실제 람다식 내부 코드를 수행함
</aside>

<br>

출처 : [https://dreamchaser3.tistory.com/5](https://dreamchaser3.tistory.com/5)
<br>

요약 :   람다식은 결국 **클래스의 private 메소드로 변환됨**


<br><br>

## **✅** Variable Capture

자바 람다식은 특정 상황에서 **몸체 바깥에 선언된 변수들에 접근 가능**하다.

<지역변수, 인스턴스 변수, 정적변수>에 접근가능!

<br>

### **⏺ 지역 변수 캡처(Local Variable Capture)**

람다식 몸체 외부에 선언된 **지역변수의 값에 접근 가능**하다.

단 참조하는 지역변수가 final/ effectively final(유사 final)이어야 한다.

effectively final : 해당 변수의 값이 할당 된 후 변경되지 않음. (재할당 되면 안되고 (final처럼 쓰여야한다. )

아래 코드는 호출 후 지역변수의 값을 변경시키려고 해서 안되는 것. 


<br>

![image](https://user-images.githubusercontent.com/48430781/203316032-b277e271-cd7c-4a6a-9639-a4bc170ae709.png)


// 값변경하는 줄을 주석처리하면 해당 에러는 삭제된다. 

<br>

### **⏺ 인스턴스 변수 캡처 (Instance Variable Capture)**

### **⏺ 정적 변수 캡처 (Static Variable Capture)**

반면 인스턴스와 정적변수는 동일한 변수를 참조할 수 있기 때문에 

컴파일러는 람다가 힙영역의 str (가장 최신의 값)을 참조할 수 있도록 보장 가능하다. 

→ 멀티 스레드에선 주의해서 사용

<br>

```java
public class LambdaClass {

    String instanceStr = "인스턴스 변수";
    static StringstaticStr= "정적 변수";

    public static void main(String[] args){
        LambdaClass lambdaClass = new LambdaClass();
        lambdaClass.stack();
    }
    void stack(){
        String str = "지역변수!";
        LambdaTest lmd = ()-> System.out.println(str);
        lmd.helloLambda();
        //str ="값변경?";

        LambdaTest lmd2 = ()-> System.out.println(instanceStr);
        lmd2.helloLambda();
        instanceStr = "인스턴스 값 변경 테스트";

        LambdaTest lmd3 = ()-> System.out.println(staticStr);
        lmd3.helloLambda();
staticStr= "인스턴스 값변경테스트";

    }
}

```

<br>

🔴  **왜 지역변수는 effectively final이어야 할까?**

JVM의 메모리구조를 생각해보면 된다. 

- 지역변수는 스택영역에 생성되고, 쓰레드별로 스택영역이 별도로 생성됨
- 즉 지역변수는 스레드끼리 공유할 수 없다.
- 인스턴스변수나 정적변수는 힙영역에 생성되므로 스레드끼리 공유가 가능하다.
- 람다가 자유변수를 참조할 때 변수를 직접 참조하지 않고, 자신의 stack에 복사해 참조하기 때문에 variable capture라는 발을 쓰는것.

→ 만약 람다식을 여러개의 쓰레드가 동시에 사용할 경우  
→ 지역변수가 effective final이 아니라면 동기화가 불가능해지는 문제가 생긴다. 


 
<br><br>

### References
남궁성-자바의정석
자료별 출처 자료주변에 링크 기입

