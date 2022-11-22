# **람다(Lambda)**
---
람다 함수는 프로그래밍 언어에서 사용되는 개념으로 익명 함수를 지칭하는 용어이다.


## **함수형 인터페이스(Functinal interface)**

- Java 8에서부터 제공하는 함수형 인터페이스는 단 **한개의 추상 메서드를 갖고 있는 인터페이스**를 말하며 @FunctionalInterface을 붙여서 함수형 인터페이스임을 표현한다.
- 한개의 추상 메서드 외에 다른 추상 메서드가 있으면 오류가 발생하기 때문에 함수형 인터페이스 규칙을 잘 지켜서 만들어야 한다.
- 함수형 인터페이스로 만들어진 변수에는 값을 갖지 않고 메서드처럼 사용하게 된다. => '함수형 프로그래밍을 한다.'
```java
public class Sample01{
  public static void main(String[] args) {
    Sample01Funtion f = () -> System.out.println("샘플01테스트 출력");
    f.test();
   }
}
@FunctionalInterface
interface Sample01Function {
  public abstract void test(); // 한 개의 추상 메서드
}
// 샘플01테스트 출력
```


## **람다식(Lambda expression) 사용법**

(매개변수 ...) -> 실행문 // 실행문이 한 줄일 경우

(매개변수 ...) -> { // 실행문이 여러 줄일 경우
  실행문1
  실행문2
};

- 매개변수가 없다면 아무것도 넣지 않아도 된다. 매개변수는 추상 메서드에서 매개변수의 자료형을 정의하기 때문에 따로 적어줄 필요가 없다. 스스로 추론하여 인식하기 때문이다.
- java파일이 컴파일되면 class파일은 익명 내부 클래스인 경우에는 내부 클래스 수만큼 class파일이 생성되었지만 람다식을 이용하면 추가로 파일이 생성되지 않는다.
- 자주 쓰이는 함수형 인터페이스는 미리 만들어져 제공하고 있으니 잘 찾아 사용할 것.
[java.util.function API:]<https://docs.oracle.com/en/java/javase/13/docs/api/java.base/java/util/function/package-summary.html>


## **메서드 참조(Method reference)**

정확히 매개변수를 추론할 수 있다면 메서드 참조를 할 수 있다.
- 메서드 참조의 종류
  - static 메서드 참조
  - 특정 개체의 인스턴스 메서드 참조
  - 특정 타입의 임의 개체에 대한 인스턴스 메서드 참조
  - 생성자 참조
- 메서드 참조 기본 문법
  - (Obejct name)::(Method name) : 개체의 이름과 메서드의 이름 사이에 더블 콜론을 구분하는 연산자로 사용한다.

### static 메서드 참조
클래스 내에 static으로 구성된 메서드를 참조 메서드로 사용할 경우이다. 
```java
public class Sample02 {
  public static void main(String[] args) {
    List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
    list.forEach(Writer::doWrite);        // --> 람다식으로 바꾸면 list.forEach( (s) -> Writer.doWrite(s) );
    }
}

class Writer {
  public static void doWrite(Object msg) {
      Systme.out.println(msg);
      }
  }
```
forEach() 메서드는 Consumer로 구성되어있다. - 반환자료형이 없으며 매개변수는 1개인 함수형 인터페이스
doWrite() 메서드와 같은 형태를 띄고 있기 때문에 오류 없이 실행되는 것이다.
매개변수로 함수형 인터페이스를 사용했기 때문에 값을 갖는 변수를 넘기는게 아니라 람다식이라 메서드 참조 형태의 메서드를 넘겨야 한다는 점에 유의해야 한다.

### 특정 개체의 인스턴스 메서드참조
생성된 인스턴스의 메서드를 참조할 수도 있다.
```java
public class Sample03 {
  public static void main(String[] args) {
    String greeting = "Hello";
    Consumer<String> consumer = System.out::println; //static 메서드 참조
    counsumer.accept(greeting);
    
    writeString(greeting::toString); // 인스턴스 메서드 참조
  }
    public static void writeString(Supplier<String> supplier) {
      System.out.println(supplier.get());
    }
}
//실행결과
//Hello
//Hello
```








