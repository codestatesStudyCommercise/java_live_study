# 7 주차 - 인터페이스의 Method

<aside>
➡️ 작성일 : 2022.11.08

</aside>

---

> 인터페이스의 메서드는 public abstract 여야 하며 이를 생략할 수 있다. 
단, static 메서드와 디폴트 메서드는 예외(JDK 1.8)
> 

- 자바 8 이전의 인터페이스는 추상 메서드만 가질수 있었으나 자바8 이후
    
    default method 와 statatic method 를 정의할 수 있도록 변경되었다.
    

# 전체 코드

```java
public class ClassTest {
    interface PrintAble{

        // public 과 abstract 는 생략가능
        // static 메서드와 default 메서드를 제외한 모든 메서드에 public abstract 기본으로 추가
        public abstract String getTitle();
        int getPageNum();

        // static 메서드 : public 은 생략가능
        public static void staticMethod(){
            System.out.println("this is Static Method ");
        };
        // static 메서드 : 내부에서 private static 메서드 사용
        public static void staticMethodUsingPrivateMethod(){
            System.out.println("this is Static Method with Private Method");
            System.out.println(getPrivateStatic());
        };

        // default 메서드 : public 은 생략가능
        public default void doNotAnythig(){

        };

        // default 메서드 : 내부에서 private 메서드 사용
        public default void doSomeThing(){
            System.out.println("doSomeThing 1 !!! -> " + getPrivateNotStatic());
        }

        // private 메서드
        private String getPrivateNotStatic(){
            return "using Private Method Not Static";
        }
        // private static 메서드
        private static String getPrivateStatic(){
            return "using Private Method Static";
        }
    }

    // PrintAble 를 구현한 Paper 클래스
    static class Paper implements PrintAble{
        @Override
        public String getTitle() {
            return "연간보고서";
        }

        @Override
        public int getPageNum() {
            return 600;
        }
    }

    // main
    public static void main(String[] args) {
        Paper paper = new Paper();
        System.out.println("1) 인터페이스의 메서드를 구현한 메서드 호출");
        System.out.println(paper.getTitle());
        System.out.println(paper.getPageNum());
        System.out.println();

        System.out.println("2) default 메서드 호출");
        paper.doNotAnythig(); // default Method 호출 : 내용 없음
        paper.doSomeThing(); // default Method 호출 : 내부에서 private 메서드 호출
        System.out.println();

        System.out.println("3) static 메서드 호출");
        // paper.isThisStaticPaper(); // static 메서드이므로 불가능
        PrintAble.staticMethod(); // static Method 호출
        PrintAble.staticMethodUsingPrivateMethod(); // static Method 호출 : 내부에서 private static 메서드 호출
        System.out.println();

        System.out.println("4) private 메서드 호출");
        // paper.getPrivateNotStatic(); // private 메서드 외부 호출 불가능
    }
}
```

---

# 인터페이스의 Static Method - 자바8 이후

```java
// static 메서드 : public 은 생략가능
public static void staticMethod(){
    System.out.println("this is Static Method ");
};
// static 메서드 : 내부에서 private static 메서드 사용
public static void staticMethodUsingPrivateMethod(){
    System.out.println("this is Static Method with Private Method");
    System.out.println(getPrivateStatic());
};

//----------------------------------------------------
// main 에서 호출 시

// paper.isThisStaticPaper(); // static 메서드이므로 불가능
PrintAble.staticMethod(); // static Method 호출
PrintAble.staticMethodUsingPrivateMethod(); // static Method 호출 : 내부에서 private static 메서드 호출
```

- static 메서드는 인스턴스와 관계 없는 독립적인 메서드
- 인터페이스의 static 메서드 는 접근제어자가 항상 `public` 이며 생략 가능
- 당연히 static 메서드는 다른 static 메서드에서 사용될 수 있지만 
static 이 아닌 메서드는 다른 static 메서드에서 사용될 수 없다.

---

# 인터페이스의 Default Method - 자바8 이후

```java
// default 메서드 : public 은 생략가능
public default void doNotAnythig(){

};

// default 메서드 : 내부에서 private 메서드 사용
public default void doSomeThing(){
    System.out.println("doSomeThing 1 !!! -> " + getPrivateNotStatic());
}

//----------------------------------------------------
// main 에서 호출 시

paper.doNotAnythig(); // default Method 호출 : 내용 없음
paper.doSomeThing(); // default Method 호출 : 내부에서 private 메서드 호출
```

- 인터페이스 내부에 메서드가 추가되는 변경사항이 생긴다면 해당 인터페이스를 상속받아 구현하는 구현체는 이 메서드를 구현해줘야하는 치명적인 불편사항이 존재
- 이를 해결하기 위한 개념으로 자바8 부터 도입되었다.
- 인터페이스에 default method 로 작성된 메서드는 구현체에서 반드시 구현하지 않아도(구현체를 변경하지 않아도) 동작에 문제되지 않는다.
- `default 반환형 메서드명(){}` 형식으로 작성하며 메서드 바디가 있어야한다.
    - default 메서드는 접근제어자가 `publilc` 이며 생략이 가능함
- **주의**
    - 새로 추가된 default 메서드가 기존의 메서드와 이름이 중복되어 충돌하는 경우가 발생할 수 있다.
    - 이러한 두가지 상황에 대한 충돌을 해결하는 규칙이 있다.
        1. 여러 **인터페이스의 default 메서드간의 충돌**이 일어나는 경우 
            - 인터페이스를 구현한 클래스에서 디폴트 메서드를 오버라이딩 해야한다.
        2. 인터페이스의 **default 메서드와 조상 클래스의 메서드 간의 충돌**이 일어나는 경우 
            - 조상클래스의 메서드가 상속되고 디폴트 메서드는 무시된다.
    - **단순하게는 필요한 쪽의 메서드와 같은 내용으로 오버라이딩 하는 방법이 있다.**

---

# 인터페이스의 Private Method - 자바9

```java
// private 메서드
private String getPrivateNotStatic(){
    return "using Private Method Not Static";
}
// private static 메서드
private static String getPrivateStatic(){
    return "using Private Method Static";
}

//----------------------------------------------------
// main 에서 호출 시

// paper.getPrivateNotStatic(); // private 메서드 외부 호출 불가능
```

- 인터페이스 내부에서만 쓰이고 외부에서는 쓰일 수 없는 메서드
    - 인터페이스 내부에서만 쓰고 싶은데 기존의 메서드는 public 이던 문제점을 개선하기위해 추가되었다. 또한 private 메서드를 사용해 인터페이스 내부에서 반복적인 코드를 줄이는것이 가능
    - default method, static method, private method 에서만 사용 가능하다고 볼 수 있다.
- 당연히 static 메서드는 다른 static 메서드에서 사용될 수 있지만 
static 이 아닌 메서드는 다른 static 메서에서 사용될 수 없다.
- `private 반환형 메서드명(){}`  형식으로 작성하며 메서드 바디를 가진다.

---

- 참고
    - 남궁성 - 자바의 정석