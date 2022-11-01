# 2회차

<aside>
➡️ 작성일 : 2022.10.31

</aside>

---

# **변수의 스코프와 라이프타임**

- *scope* of a variable ( 변수의 스코프 )
    - 범위
    - 변수에 엑세스 할 수 있는 프로그램의 영역 또는 섹션
    - 자바에서 변수 선언시 해당 변수가 접근이 가능한 범위가 있다.
    - 변수의 범위에 대한 포괄적인 관례는 변수가 선언된 블록 내에서만 접근 할 수 있다는 것이다.
- *lifetime* of a variable (변수의 라이프타임)
    - 수명
    - 변수가 메모리에서 얼마나 오래 살아있는지
- 변수의 스코프와 라이프타임을 결정짓게 되는 공통된 요소는 다음과 같다.
    - *변수가 어떻게 정의되었는가*
    - *변수가 어디서 정의되었는가*
    
- 선언된 위치에 따른 변수의 종류 및 각 변수들의 스코프와 라이프타임
    
    ```java
    public class scope_and_lifetime {
    
        int num1, num2;           //Instance Variables
        static int result;       //Class Variable
        int add(int a, int b){  //Local Variables
            num1 = a;
            num2 = b;
            return a+b;
        }
    
        public static void main(String args[]){
            scope_and_lifetime ob = new scope_and_lifetime();
            result = ob.add(10, 20);
            System.out.println("Sum = " + result);
        }
    }
    ```
    
    - **인스턴스 변수**
        - 특징
            - 클래스 내부에서 선언되었지만 메서드 블록 외부에서 선언된 변수
            - 클래스의 인스턴스를 생성할 시점에 만들어짐
            - → 인스턴스 변수의 값을 읽어오거나 저장하기 위해서는 먼저 인스턴스를 생성해야함
            - 인스턴스는 독립적인 공간을 가지므로 다른 인스턴스가 서로 다른 값을 가질 수 있다.
            - 인스턴스마다 고유한 상태를 유지해야하는 속성의 경우, 인스턴스 변수로 선언한다.
        - scope
            - 정적 메서드를 제외한 클래스 전체
        - lifetime
            - 클래스의 인스턴스를 생성할때 생성
            인스턴스가 메모리에 머무를때까지
    - **클래스 변수**
        - 특징
            - 클래스 내부, 메서드 블록 외부에 선언되고 static 으로 선언된 변수
            - 인스턴스 변수에 static 이 붙은 형태
            - 클래스 변수는 모든 인스턴스가 공통된 저장공간(변수)를 공유하게 된다.
            - 한 클래스의 모든 인스턴스들이 공통적인 값을 유지해야하는 속성의 경우
            클래스 변수로 선언한다.
            - 클래스변수는 클래스가 메모리에 로딩될때 생성되어(따라서 메모리에 한번만 올라간다.) 프로그램 종료까지 유지
            - 인스턴스를 생성하지 않고도 `클래스이름.클래스변수명` 의 형태로 사용 가능
            - public 을 붙이면 같은 프로그램 내의 어디서나 접근 가능한 전역변수의 성격을 갖는다.
        - scope
            - public 적용시 : 프로그램 내의 어디서나 접근 가능
                
                (`클래스이름.클래스변수명`)
                
            - public 미적용시 : 같은 Class 내부라면 어디서나
                
                (클래스 변수는 모든 인스턴스가 공통된 저장공간(변수)를 공유하게 된다.)
                
        - lifetime
            - 클래스가 메모리에 로딩될때 생성
                
                프로그램 종료 시 까지
                
    - **지역 변수**
        - 특징
            - 인스턴스 또는 클래스 변수가 아닌 모든 변수
                
                (ex : 메서드 내의 변수, 매개변수, loop 문 내의 변수, 스코프 내의 변수 등 )
                
        - scope
            - 선언된 블록 내
        - lifetime
            - 선언된 블록에 제어가 넘어올때 생성
                
                지역변수가 선언된 블록에서 제어가 떠날때까지
                

- 정리
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2f7aab30-764e-4b67-8080-2461400be1f5/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221101%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221101T130049Z&X-Amz-Expires=86400&X-Amz-Signature=48622f7f6ab1953fa1d4c11c2f52ea2a7392c6cf79e4524517f3cc7d9f226675&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
---

# 타입 변환, 캐스팅 그리고 타입 프로모션

- **Type Casting** 형변환의 넓은 의미
    - 변수나 리터럴(상수)의 타입을 다른 타입으로 변환시키는 것

# **Type Casting 캐스팅**

- 명시적 타입 변환
    - 형변환 연산자를 사용
    
    ```java
    double d = 85.4;
    // ( 변환하고 싶은 타입 ) 피연산자
    int score = (int) d;
    ```
    
    - 주의 :
        - 형변환 연산자는 그저 피 연산자의 값을 읽어서 지정된 타입으로 형변환 하고
            
            결과를 반환할 뿐이다. 
            
        - 위 코드에서 변수 d 의 값은 형변환 후에도 변하지 않는다.
    - primitive type (기본형) 에서 boolean 을 제외한 나머지 값들은 서로 형변환 가능
        - **정수형간 형변환**
            - 작은 타입에서 큰 타입으로 변환할 경우 값 손실이 발생하지 않으며 메모리에서 남는 공간은 0(일반적인 경우) 또는 1(변환하려는 값이 음수인 경우) 로 채워진다.
                - `Integer.toBinaryString(int i)` 를 사용하여 
                10진수 정수를 2진수 정수로 변환한 문자열 획득 가능
            - 큰 타입에서 작은 타입으로 변환할 경우 부족한 공간만큼 잘려나간다.
                - 값손실에 주의
        - **실수형간 형변환**
            - 참고
                - 실수형
                - [https://jobdahanit.tistory.com/25](https://jobdahanit.tistory.com/25)
            - 정수와 유사하나 큰범위에서 작은 범위로 변환할 때 오차발생 
            (데이터가 버려질때 반올림 수행으로 인함 )
            - float 타입의 범위를 넘는 값을 float 으로 형 변환하는 경우 +-무한대 또는 +-0을 결과로 얻는다.
        - **정수형  ↔   실수형 간의 형변환**
            - 정수를 실수로 변환 시
                - 실수형으로 인한 오차가 발생할 수 있음에 유의
                - 표현범위가 넓어 오차가 적은 double 을 사용하자
            - 실수를 정수로 변환시
                - 형변환시 실수형의 소수점 이하 값은 버려진다.
    - primitive type 과 reference type(참조형) 간의 형변환은 불가능하다.
        - 참조형간의 형변환은 가능
    - **참조형 타입과 참조형 타입의 형변환**
        - 상속관계가 아닌 클래스간의 형변환은 불가능
        - 참조변수의 형변환을 통해 참조하고 있는 인스턴스에서 사용할 수 있는 멤버의 범위를 조절하는 느낌으로 사용한다.
        - 객체지향 - 다형성과 관련된 내용
            - 다형성
                - 여러가지 형태를 가질 수 있는 능력
                
                > 자바에서는 한타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 함으로써 다향성을 프로그램적으로 구현하였다.
                > 
                - 조상클래스 타입의 참조변수로 자손 클래스의 인스턴스를 참조할 수 있도록 하였다는 뜻
                - 같은 타입의 인스턴스라도 참조변수의 타입에 따라 사용할 수 있는 맴버의 갯수가 다르다.
                - 단, 참조변수가 사용할 수 있는 멤버의 개수는 인스턴스의 맴버 개수보다 같거나 적어야한다.
                - 조상타입의 참조변수로 자손타입의 인스턴스를 참조할 수 있다.
                - 자손타입의 참조변수로 조상타입의 인스턴스를 참조할 수 없다.
        
        ```java
        // Class FireEngine 은 Class Car 를 상속받는다. 
        Car car = null;
        Car rearCar = new Car();
        FireEngine fe = new FireEngine();
        FireEngine fe2 = null;
        FireEngine fe3 = null;
        
        car = fe; // 자동 형변환 진행 car = (Car) fe;
        fe2 = (FireEngine) car; // 형변환 생략 불가능
        
        fe3 = (FireEngine) rearCar; // 에러 : ClassCastException
        // 조상타입의 인스턴스를 자손타입의 참조변수로 참조하는것은 허용되지 않는다.
        ```
        
        - 자손타입 → 조상타입 으로 형변환
            - Up-casting
            - 형변환 생락 가능
        - 조상타입 → 자손타입 으로 형변환
            - Down-casting
            - 형변환 생략 불가능

# **Type Promotion**

- 묵시적 타입 변환
- 자동 형변환
- 서로 다른 타입간의 대입이나 연산을 수행 시 원칙적으로 타입을 일치시켜야 하지만 
경우의 따라 편의상의 이유로 이를 생략 가능
- 이 경우 컴파일러가 생략된 형변환을 자동적으로 추가하여 이루어진다.
- 그러나 자동형변환을 수행하려고 해도 형변환이 불가능한 상황이라면 에러가 발생한다.
    - ex : 좁은 데이터형에 큰 데이터를 넣으려 시도할때 `incompatible type`
- 명시적 형변환을 사용한 경우 에러가 발생하진 않지만 값 손실이 발생한다.
    - 컴파일러가 개발자의 의도적인 행동이라고 간주
- 두 타입이 다른 연산에서 빈번히 발생한다.
    - 연산과정에서 자동적으로 발생하는 형변환을 산술변환이라고 함
    
    ```java
    int intA = 30;
    double doubleA = 1.0 + intA // intA 앞 (double)intA 생략
    ```
    
    - 표현의 범위가 더 넓은 타입으로 형변환을 통해 타입을 일치시킨 후 연산을 수행
        
        → 값손실의 위험을 최소화 하기 위함 
        
- 자동 형변환 규칙
    - 서로 다른 두 타입 중 기존 값을 최대한 보존할 수 있는 타입으로 자동 형변환한다.
        - 표현의 범위가 더 넓은 타입으로 형변환하여 값손실의 위험을 최소화
        - 따라서 의도적으로 작은 타입으로 형변환 하기위해선 형변환 연산자를 사용해야한다.
    

---

- 참고
    - 변수의 스코프와 라이프타임
        - 남궁석 - 자바의 정석
        - [https://www.learningjournal.guru/article/programming-in-java/scope-and-lifetime-of-a-variable/](https://www.learningjournal.guru/article/programming-in-java/scope-and-lifetime-of-a-variable/)
        - [https://itmining.tistory.com/20](https://itmining.tistory.com/20)
        - [https://codechacha.com/ko/java-variable-scope/](https://codechacha.com/ko/java-variable-scope/)
    - 타입 변환, 캐스팅 / 타입 프로모션
        - 남궁석 - 자바의 정석
        - [http://www.tcpschool.com/java/java_datatype_typeConversion](http://www.tcpschool.com/java/java_datatype_typeConversion)
