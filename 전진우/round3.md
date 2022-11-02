# 3주차 - 화살표연산자

<aside>
➡️ 작성일 : 2022.11.01

</aside>

---

# → (화살표) 연산자

- 람다 표현식을 구성하는 데 사용

---

# 익명함수

- 람다식은 함수의 이름 없이 사용되기때문에 익명함수라고 불리기도 한다.
    
    (사실은 익명객체이다.)
    

---

# 람다식에 대한 간략한 이해

- 하위 내용은 화살표 연산자에 대한 조사로 인해 
람다가 무엇인지, 어떻게 이루어지는지 가볍게이해하기 위한 정리글
- 람다의 정확한 개념과 활용을 위한 지식은 추후에 다룰 예정
    - 람다식의 타입과 형변환
    - 람다식의 외부 변수 참조
    - java.util.function 패키지
    - 메서드 참조 등

---

# 람다식 소개

- 람다란
    - 자바의 큰 두가지 변화
        - JDK 1.5부터의 Generics ( 제네릭 )
        - JDK 1.8부터의 Lambda expression ( 람다식 )
    - 람다식의 도입으로 인해 
    자바는 객체지향 언어임과 동시에 함수형 언어의 기능을 갖출 수 있었다.
        - 람다는 특정 클래스에 속하지 않고도 사용 가능하기때문에 
        클래스 내에 속하는 함수라는 의미를 내포하는 메서드라는 용어 대신 함수라는 용어를 채택하였다.
    - 람다는 메서드를 하나의 식으로 표현한 것
        
        ```java
        // 일반 메서드 
        int max (int a, int b) {
        	return a > b ? a : b; 
        }
        
        // max() 와 같은 역할을 하는 람다 표현식
        (a, b) -> a > b ? a: b
        
        // -------------------------------------------
        
        // 일반메서드 
        void printVar(String name, int i) {
        	System.out.println(name + " = " + i);
        }
        // printVar() 와 같은 역할을 하는 람다식
        (name, i) -> System.out.println(name + "=" + i)
        ```
        
    - 장점
        - 간결면서도 이해하기 쉽다.
        - 함수를 정의하기 위해 클래스를 새로 만들 필요없이 필요시 바로 람다식을 통한 메서드 역할 수행이 가능하다.
        - 람다식을 사용하여 메서드를 변수처럼 다루는것이 가능하다.
            - 람다식은 다른 메서드의 매개변수로 전달되어지는것이 가능하다.
            - 람다식은 메서드의 결과로 반환되는것이 가능하다.
    - 단점
        - 지나치게 남발하면 코드가 이해하기 어렵고 지저분해짐.
        - 람다를 사용하여 만든 무명함수는 재사용이 불가능함.

---

# 람다에서의 타입추론

- 자바 컴파일러가 타입을 추론하는 것을 타입추론이라고 한다.
    - 컴파일러는 타입을 추론하기 위해 메서드 호출과 이에 상응하는 선언부를 살펴본다.
- 람다식에 선언된 매개변수의 타입은 추론이 가능한 경우 생략이 가능하다.
- 반환타입이 없는 이유 역시 추론이 가능하기때문
- **추후 람다파트에서 자세히 기술**

# Anonymous class 익명클래스

- 이름이 없는 클래스 (조상의 클래스이름 또는 인터페이스 이름을 통해 정의)
- 클래스의 선언과 객체생성을 동시에 진행
    - 따라서 한번만 사용될 수 있고 오직 하나의 객체만을 생성할 수 있는 일회용 클래스
- **조상의 클래스 이름 또는 구현하고자 하는 인터페이스 이름을 통해 정의**
    - 때문에 오로지 단하나의 클래스를 상속받거나 단하나의 인터페이스만 구현 가능 (둘이상은 불가능)
    
    ```java
    
    class Example {
    	// 익명클래스 정의 형태 
    	Object annyClass01 = new Object() { void methodEx() {}}; 
    	static	Object annyClass01 = new Object() { void methodEx() {}};
    
    	void methodNormal(){
    		Object annyClass02 = new Object() { void methodEx() {}};
    	}
    }
    ```
    
- 사용예
    
    ```java
    // 익명클래스 사용 X 
    public class NoAnny {
        public static void main(String[] args) {
            Button buttonStart = new Button("Start");
            buttonStart.addActionListener(new **EventHandler**());
        }
    }
    
    class **EventHandler** implements **ActionListener** {
        @Override
        public void actionPerformed(ActionEvent e) {
            System.out.println("ActionEvent Occurred !!! ");
        }
    }
    //---------------------------------------------------------------
    
    // 익명클래스 사용시 
    public class YesAnny {
        public static void main(String[] args) {
            Button buttonStart = new Button("Start");
            buttonStart.addActionListener(new **ActionListener**() {
                @Override
                public void actionPerformed(ActionEvent e) {
                    System.out.println("ActionEvent Occurred !!! ");
                }
            });
        }
    }
    
    //---------------------------------------------------------------
    //---------------------------------------------------------------
    
    interface **MyFunction** {
        public abstract int max(int a, int b);
    }
    
    // ...생략 main() 
    MyFunction f = new **MyFunction**() {
                @Override
                public int max(int a, int b) {
                    return a > b ? a : b;
                }
            };
    
    int maxNum = f.max(3, 50);
    // ...생략 
    
    ```
    

# 함수형 인터페이스

- 이해
    - 람다식은 어떤 클래스에 포함되어있을까
    - 자바에서 모든 메서드는 클래스 내에 포함되어야한다.
    - 사실 람다식은 익명 클래스의 객체와 동등하다.
        
        ```java
        interface **MyFunction** {
            public abstract int max(int a, int b);
        }
        
        // 익명의 클래스의 메서드
        MyFunction f = new **MyFunction**() {
                    @Override
                    public int max(int a, int b) {
                        return a > b ? a : b;
                    }
                };
        
        // 해당 람다식은 위 익명 클래스의 객체와 동등하다.
        MyFunction f = (int a, int b) -> a > b ? a : b;
        
        // 호출 
        int maxNum = f.max(3, 50);
        ```
        
    - 익명클래스에서의 메서드 호출과 마찬가지로
        
        람다식이 익명클래스의 객체와 동등하다면 같은 방법으로 호출 가능 
        
    - MyFunction 인터페이스를 구현한 익명 객체를 람다식으로 대체 가능한 이유
        - 람다식도 실제로는 익명 객체이기때문
        - MyFunction 인터페이스를 구현한 익명 객체의 메서드 max() 와
        - 람다식의 매개변수의 타입과 갯수 , 반환값이 일치하기 때문
    - 위와 같은 사실들을 통해 하나의 메서드가 선언된 인터페이스를 정의해서 람다식을 다루면 
    기존의 자바의 규칙들을 어기지 않으면서 자연스럽게 구현 가능
        
        → 따라서 인터페이스를 통해 람다식을 다루기로 결정 
        
        → 람다식을 다루기 위한 인터페이스 : Functional Interface (함수형 인터페이스) 라고 한다.
        
- 함수형 인터페이스
    
    ```java
    **@FunctionalInterface**
    interface MyFunction{
        public abstract int max(int a, int b);
    }
    
    // 함수형 인터페이스를 참조변수로 사용 : MyFunction f 
    MyFunction f = () -> System.out.println("myMethod is occurred !!!");
    ```
    
    - 함수형 인터페이스는 오직 하나의 추상 메서드만 정의되어있어야 한다.
        - 람다식과 인터페이스의 메서드가 1:1 로 연결되어야 하기 때문
        - static 메서드와 defualt 메서드의 개수는 제약이 없다.
    - @FunctionalInterface 을 붙이면 컴파일러가 함수형 인터페이스 정의를 검사해준다.

# 람다식의 사용예시

- 람다식은 매개변수로 사용 가능
    
    ```java
    @FunctionalInterface
    interface MyFunction{
        public abstract int max(int a, int b);
    }
    
    // --------------------------생략 
    // 다음과 같이 함수형 인터페이스가 어떤 메서드의 매개변수 형으로 선언되어있을때 
    void aMethod(MyFunction f) {
            f.myMethod();
    }
    
    // --------------------------생략 
    
    MyFunction f = () -> System.out.println("myMethod is occurred !!!");
    
    // 람다식을 참조하는 참조변수가 매개변수로 지정될 수 있다.
    aMethod(f);
    
    // 또는 다음과 같은 방식 역시 가능하다.
    aMethod(() -> System.out.println("myMethod is occurred !!!"));
    ```
    
- 람다식은 반환될 수 있다.
    
    ```java
    @FunctionalInterface
    interface MyFunction{
        public abstract int max(int a, int b);
    }
    // --------------------------생략 
    
    // 다음과 같이 함수형 인터페이스가 어떤 메서드의 매개변수 형으로 선언되어있을때 
    MyFunction myMethod() {
    	MyFunction f = () -> {};
    	
    	// 람다식을 가리키는 참조변수를 return 
    	return f;
    	// 또는 다음과 같은 방식 역시 가능
    	return () -> {}; // myMethod 함수의 리턴타입이 지정되어있으므로 가능
    }
    ```
    

---

- 참고
    - 남궁성 - 자바의 정석
    - [https://live-everyday.tistory.com/207](https://live-everyday.tistory.com/207)