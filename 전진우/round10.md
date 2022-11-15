# 10회차 - Annotation

<aside>
➡️ 작성일 : 2022.11.13

</aside>

---

# 애노테이션이란

- 주석, 메모라는 사전적 의미
- 메타데이터의 한 형태인 애노테이션은 프로그램 그차제의 일부는 아니지만 프로그램에 대한 데이터를 제공한다.
    - 애노테이션은 주석처럼 프로그래밍 언어에 영향을 미치지 않으면서도 다른 프로그램에게 유용한 정보를 제공할 수 있다.

### 애노테이션의 용도

- **컴파일러에게 필요한 정보를 제공**
    - 애노테이션은 컴파일러가 에러를 체크하거나 경고를 억제할 수 있도록 정보를 제공
- **컴파일 및 배포 시 기능 처리**
    - 애노테이션은 소프트웨어 도구가 자동으로 코드, XML 파일 등을 생성할 수 있도록 정보를 제공한다.
- **런타임에 기능 처리**
    - 애노테이션은 런타임 시에도 특정 기능을 처리하도록 정보를 제공 . (Java Reflection)
    
- 형태
    
    ```java
    // 애노테이션 사용
    @Override 
    void mySuperMethod() { ... }
    
    // 애노테이션의 요소 
    @Author(
       name = "Benjamin Franklin",
       date = "3/27/2003"
    )
    class MyClass { ... }
    
    // 요소 이름 생략 가능 
    @SuppressWarnings("unchecked")
    void myMethod() { ... }
    
    // 요소가 없으면 괄호 생략 가능 
    @Author(name = "Jane Doe")
    @EBook
    class MyClass { ... }
    
    // 반복주석 - 자바8부터 가능 
    @Author(name = "Jane Doe")
    @Author(name = "John Smith")
    class MyClass { ... }
    ```
    
    - 위같은 형태로 @기호를 사용해 애노테이션임을 컴파일러에게 알린다.
    - @기호 뒤에 오는것이 애노테이션의 이름이다.
    - 애노테이션은 이름이 지정되거나 지정되지 않은 요소 가 포함될 수 있으며 
    해당 요소에 대한 값이 있다.
        - 요소가 하나만 있는 경우 요소의 이름을 생략할 수 있다.
        - 요소가 없는 경우 괄호를 생략할 수 있다.
    - 하나의 선언에 여러개의 애노테이션을 사용할 수 있다.
    
    - 적용 위치
        - 애노테이션은 선언에서 많이 사용된다.
            - 클래스, 필드, 메소드 및 기타 프로그램 요소의 선언등
            - 각 주석은 규칙에 따라 고유한 위치에 사용되는 경우가 많다.
            - 자바8부터 타입에 대한 애노테이션을 적용할 수 있게 되었다.
        - 대표적 적용 위치
            - 클래스에 대한 인스턴스 생성 표현식
                
                ```
                new @Interned MyObject();
                ```
                
            - 타입 캐스팅
                
                ```
                myString = (@NonNull String) str;
                ```
                
            - `implements` 사용시
                
                ```
                class UnmodifiableList<T> implements
                    @Readonly List<@Readonly T> { ... }
                ```
                
            - `throws` 를 사용해 예외 선언시
                
                ```
                void monitorTemperature() throws
                    @Critical TemperatureException { ... }
                ```
                

---

# 종류

## 1. 표준 애노테이션

- 자바에서 기본적으로 제공하는 애노테이션
- `@Override`
    - 조상의 메서드를 오버라이딩 하는 것이라는것을 컴파일러에게 알리는 역할
    - 컴파일 시 같은 이름의 메서드가 조상에 있는지 확인하므로 
    오버라이딩 하는 메서드의 메서드명을 잘못기입하는등의 상황을 방지할 수 있다.
- `@Deprecated`
    - 앞으로 사용하지 않을것을 권장하는 대상에 붙인다.
    - 해당 애노테이션이 붙은 대상은 다른것으로 대체되었으니 더이상  사용하지 않는것을 권한다.
    - 해당 애노테이션이 붙은 대상을 사용하는 코드를 작성한다면 컴파일 시 deprecated 된 대상을 사용하고 있다고 알려준다.
- `@SuppressWarnings`
    - 경고의 종류를 지정하여 컴파일러의 특정 경고메세지가 나타나지 않게 해준다.
        - 발생하는 경고메세지 중에서 [ ] 안에 있는것이 메세지의 종류이다.
    - 넓은 범위에서 남발하여 사용하지 말고 반드시 필요한 범위에만 적절히 사용해야한다.
    - `@SuppressWarnings(”unchecked”)`
    - `@SuppressWarnings(”deprecation”, ”unchecked”, ”varargs”)`
        - 억제할 수 있는 경고 메세지의 종류는 여러가지가 있는데 JDK 의 버전이 올라감에 따라 계속 추가될 예정
        - 콤마를 통해 여러 종류를 함께 사용할 수 있다.
    - 자주 사용되는 몇가지 종류가 있다.
        - deprecation : @Deprecated 가 붙은 대상에 대한 경고
        - unchecked : 제네릭 타입을 지정하지 않았을때 발생하는 경고
        - rawtypes : 제네릭을 사용하지 않아서 발생하는 경고
        - varargs : 가변인자의 타입이 제네릭 타입일 때 발생하는 경고
- `@SafeVarargs`
    - 제네릭 타입의 가변인자에 사용한다.(JDK 1.7 부터)
    - static 이나 final 이 붙은 메서드와 생성자에만 붙일 수 있다.
        - 오버라이드 될 수 있는 메서드에는 사용할 수 없다는 뜻
    - 메서드에 선언된 가변인자의 타입이 non-reifiable 타입일 경우
    해당 메서드를 선언하는 부분과 호출하는 부분에서 unchecked 경고가 발생
        - reifiable : 컴파일 후에도 제거되지 않는 타입
        - non-reifiable : 컴파일 후 제거되는 타입 : 제네릭, 경계타입
        - [https://cla9.tistory.com/52](https://cla9.tistory.com/52)
    - 코드에 문제가 없다면 이 경고를 억제하기 위해 `@SafeVarargs` 를 사용해야한다.
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b39571da-eb0f-4947-92d0-e67353043a5e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T085432Z&X-Amz-Expires=86400&X-Amz-Signature=f99bc47b4387eb74bc369a72eb0139cdc7144d95e135464ef0766118b0d90062&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

        - Arrays 클래스의 asList ()
        - 매개변수가 가변인자(…)인 동시에 제네릭타입
            - 가변인자는 컴파일시 배열로 처리된다.
        - T는 컴파일 과정에서 Object 로 바뀐다.
        - Object[] 가 된다면 모든 타입의 객체가 들어갈수 있으므로 이 배열을 통해 `ArrayList<T>` 를 생성하는것이 위험하다고 경고
        → 컴파일러가 타입T 가 아닌 다른 타입이 들어가지 못하도록 막으므로 코드에 아무런 문제가 없다.
        → `@SafeVarargs` 를 사용해 타입안정성이 있다고 컴파일러에게 알려 경고 억제
    - 참고
        - `@SafeVarargs` 와 `@SuppressWarnings`
            - 메서드 선언부에 `@SafeVarargs` 사용시 메서드를 호출하는 곳에서 발생하는 경고도 억제됨
            - `@SuppressWarnings(”unchecked”)`를 통해 억제하고싶다면, 메서드 선언부와 호출부 모두 애노테이션을 사용해야한다.
        - `@SafeVarargs` 사용시 `@SuppressWarnings(”varargs”)` 를 함께 사용
            - `@SafeVarargs` 를 통해 unchecked 경고는 억제 가능한 반면에 
            varages 경고는 억제 불가능
            - `@SuppressWarnings(”varargs”)` 를 함께 사용해 varargs 경고를 억제한다.
- `@FunctionalInterface`
    - 함수형 인터페이스라는것을 알린다. (JDK 1.8 부터)
    - 함수형 인터페이스를 올바르게 선언했는지 확인하고 잘못된 경우 에러 발생
- `@Native`
    - native 메서드에서 참조되는 상수 필드 앞에 붙이는 애노테이션 (JDK 1.8 부터)
        - *** native 메서드란
            - JVM 이 설치된 OS 의 메서드
            - 네이티브 메서드는 보통 C 언어로 작성되었는데 자바에서는 메서드의 선언부만 정의하고 구현은 하지 않는다. → 선언부만 있고 바디는 없다.
            - native 메서드를 호출시 실제 호출되는것은 OS 의 메서드이다.
                - 호출하기 위해선 자바에 정의된 네이티브 메서드와 OS 의 메서드를 연결해주는 작업이 추가로 필요하다. 
                (JNI : Java Native Interface 에 대한 이해가 필요)

---

## 2. 메타 애노테이션

- 애노테이션을 위한 애노테이션
- 애노테이션에 붙이는 애노테이션
- 주로 애노테이션을 정의하기 위해 사용
- `@Target`
    
    ```java
    @Target({FIELD, TYPE, TYPE_USE})
    public @interface MyAnnotation{  }
    ```
    
    - 애노테이션이 적용 가능한 대상을 지정
    - 여러 값을 지정하고 싶을 떄는 괄호`{}` 를 사용
    - 지정 가능한 타입은 `java.lang.annotation.ElementType` 열거형에 정의
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/94083762-612b-4a9b-b97c-967e7b33a6e2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T085551Z&X-Amz-Expires=86400&X-Amz-Signature=e013e4862b51f5f808101a5d1ec62c804933a6e440710775ce52b253a71343e6&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
        
        - TYPE_PARAMETER 와 TYPE_USE 는 JDK 1.8 부터 가능
        - FIELD 는 기본형에, TYPE_USE 는 참조형에 사용된다.
- `@Retention`
    
    ```java
    @Target(ElementType.METHOD)
    @Retention(RetentionPolicy.SOURCE)
    public @interface Override { }
    ```
    
    - 애노테이션이 유지되는 기간을 지정하는데 사용
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/79b57317-f1dd-45af-8fc6-2a0c5e30b52b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T085614Z&X-Amz-Expires=86400&X-Amz-Signature=28dca913f282fb0362c654627d404c14e06cfd815736603ec4ec84f2a54d7055&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
        
        - `SORCE`
            - 컴파일러를 직접 작성할 것이 아니면 해당 유지정책은 필요 없다.
            - `@Override` 나 `@SuppressWarnings` 처럼 컴파일러가 사용하는 애노테이션은 유지정책이 SOURCE 이다.
        - `CLASS`
            - CLASS 유지정책이 기본값임에도 잘 사용되지 않는다.
                - 컴파일러가 애노테이션의 정보를 클래스 파일에 저장할 수 있게는 하지만 
                클래스 파일이 JVM 에 로딩될 때는 애노테이션의 정보가 무시
                - 실행시에 애노테이션에 대한 정보를 얻을 수 없다.
                    
                    → 잘 사용 안되는 이유
                    
        - `RUNTIME`
            - 실행 시에 리플렉션(reflection)을 통해 클래스 파일에 저장된 애노테이션의 정보를 읽어서 처리할 수 있다.
            - `@FunctionalInterface` 의 경우 컴파일러가 체크해주는 애노테이션이지만, 실행시에도 사용되므로 유지정책이 `RUNTIME` 으로 되어있다.
            - *** 리플렉션이란
                
                > 리플렉션이란 객체를 통해 클래스의 정보를 분석해 내는 프로그램 기법을 말한다.
                리플렉션은 구체적인 클래스 타입을 알지 못하더라도 그 클래스의 메서드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API
                컴파일 타임이 아닌 런타임에 동적으로 클래스의 정보를 추출할 수 있다.
                > 
- `@Documented`
    
    ```java
    @Documented
    @Retention(RetentionPolicy.RUNTIME)
    @Target(ElementType.TYPE)
    public @interface FunctionalInterface { }
    ```
    
    - 애노테이션에 대한 정보가 javadoc 으로 작성한 문서에 포함되도록 한다.
    - 자바에서 제공하는 기본 애노테이션 중 `@Override` 와 `@SuppressWarnings` 를 제외한 모두는 해당 애노테이션이 붙어있다.
- `@Inherited`
    
    ```java
    @Inherited
    @interface SupperAnnotation{}
    
    @SupperAnnotation
    class Parent{}
    
    class Child extend Parent{}
    ```
    
    - 애노테이션이 자손 클래스에 상속되도록 한다.
    - 해당 애노테이션을 상위클래스에 붙이면 하위 클래스도 상위클래스에 붙은 애노테이션들이 동일하게 적용된다.
- `@Repeatable`
    
    ```java
    // 애노테이션을 묶을 애노테이션이 필요
    @interface ToDos{
    		ToDo[] value();
    }
    
    @Repeatable(ToDos.class)
    @interface ToDo{
    		String value();
    }
    
    @ToDo("delete test codes.")
    @ToDo("override inherited methods")
    class MyClass{...}
    
    ```
    
    - 해당 애노테이션을 적용한 애노테이션은 여러번 붙일 수 있다.
    - 같은 이름의 애노테이션이 여러개가 하나의 대상에 적용될 수 있으므로 
    해당 애노테이션들을 하나로 묶어서 다룰 수 있는 애노테이션도 추가로 정의해야한다.

---

# 3. 사용자 정의 애노테이션

- 사용자가 직접 정의하여 사용하는 어노테이션
- 프레임워크나 API 등을 만들어 사용할 때 주로 사용

- 직접 애노테이션 타입 정의

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface TestInfo{ 

		int count() default 1;
		String testedBy();
		String[] testTools() default "JUnit";
		TestType testType() default TestType.FIRST; // enum TestType
		DateTime testDate(); // 다른 애노테이션을 포함(@DateTime)
}

@interface 애너테이션이름 {
		타입 요소이름(); 
}
```

- 인터페이스를 정의하는것과 형태가 유사하다.
- `@Override` 에서 `@Override` 는 애노테이션이고, Override 는 `애노테이션의 타입`이다.
- **애노테이션의 요소**
    - 반환값이 있고 매개변수는 없는 추상 메서드의 형태
        - 상속을 통해 구현하지 않아도 된다.
        - 애노테이션 적용 시 해당 요소들을 모두 지정해주어야한다.
        - 애노테이션의 요소가 하나이면서 그 이름이 value 라면 요소의 이름을 생략가능
        - 요소의 이름을 같이 적으므로 순서는 상관없다.
    - 요소의 타입이 배열이라면 괄호`{}` 를 사용해 여러 값을 지정할 수 있다.
    - 애노테이션의 각 요소는 기본값을 가질 수 있다.
        - 기본값이 있는 요소는 애노테이션 적용시 값을 지정하지않으면 기본값이 사용된다.
- **요소 정의 시 규칙**
    - 요소의 타입은 기본형, String, enum, 애노테이션, Class 만 허용 가능하다.
    - ()안에 매개변수를 선언할 수 없다.
    - 예외를 선언할 수 없다. (throws 불가능)
    - 요소를 타입 매개변수로 정의할 수 없다.

---

# 마커 애노테이션

- Marker Annotation
- 값을 지정할 필요가 없는 경우
- 애노테이션의 요소를 하나도 정의하지 않은 애노테이션

---

# java.lang.annotation.Annotation

- 모든 애노테이션의 조상
- 상속이 허용되지 않는다.
- Annotation 은 애노테이션이 아니라 일반 인터페이스로 정의되어있다.
- Annotation 에 정의된 내용에 따라 모든 애노테이션 객체에 대해 메서드 호출 가능
    - `equals()`
    - `hashCode()`
    - `toString()`

```java
// 클래스에 있는 애노테이션 정보를 확인하기 위한 코드
Class<MyClass> myClass = MyClass.class;
Annotation[] annoArr = myClass.getAnnotations();

if (annoArr.length == 0) {
    System.out.println("empty !!");
} else {
    for (Annotation annotation : annoArr) {
        System.out.println(annotation);
        System.out.println("annotation.toString() = " + annotation.toString());
        System.out.println("annotation.hashCode() = " + annotation.hashCode());
        System.out.println("annotation.equals(annotation) = " + annotation.equals(annotation));;
        System.out.println("annotation.annotationType() = " + annotation.annotationType());
    }
}
```

- `@Retention()` 조건에 따라 애노테이션 정보를 가져오지 못할 수 있다.

---

# 애노테이션 프로세서

- 일종의 자바 컴파일러 플로그인으로 
컴파일 단계에서 애노테이션들을 스캐닝하고 프로세싱하는 javac 에 속한 빌드 툴
    - 소스 또는 리소스 파일 세트 생성
    - 기존 소스 코드를 변경
    - 기존 소스 코드 분석 및 진단 메세지 생성
- 특정 애노테이션이 동작하기 위해  애노테이션 프로세서를 만들어 등록할 수 있다.
- 모든 애노테이션 프로세서들은 AbstractProcessor 를 상속받아야한다.

- 애노테이션 프로세서 사용 예 (롬복이란)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4d9888dd-1155-4f1e-99b5-5506c6da0b7e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T085639Z&X-Amz-Expires=86400&X-Amz-Signature=e2f1570c1931be846b812c0fefed67fb549d76641f01d81505fe446fa209bf54&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8c8193bf-63ab-46ad-97b7-223478816e62/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T085656Z&X-Amz-Expires=86400&X-Amz-Signature=d8655592089c0a3e097e11e68c481a0596ad6c25a84a27c8a99fa01eed132d20&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    - 자바의 라이브러리로 반복되는 메소드를 애노테이션을 사용해서 자동으로 작성해주는 라이브러리
        - 주로 게터, 세터, 생성자 등 매번 작성해주어야하는 코드를 대신 작성
    - 애노테이션과 애노테이션 프로세서를 제공하여 개발자가 작성해야할 코드를 대신 작성해주는 라이브러리
    - 컴파일 시점에 애노테이션 프로세서가 애노테이션을 보고 AST 를 조작한다.
        - 롬복의 @Setter 애노테이션 사용시 해당 클래스를 AST 노드에 찾아가 setter 의 트리를 만들어 노드에 연결하는 방식
    - 컴파일러가 수정된 AST 를 컴파일한다.
        - 컴파일 이후 Setter 메서드 사용 가능
    
    - ***AST
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1f48f29c-548d-4ed8-98f1-4ca4697534cf/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T085718Z&X-Amz-Expires=86400&X-Amz-Signature=5b872e735604e8ca743555af61a219ba95157e4d94f5de8b9c7c695983b7ecaf&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
        
        [https://www.programcreek.com/2012/04/represent-a-java-file-as-an-astabstract-syntax-tree/](https://www.programcreek.com/2012/04/represent-a-java-file-as-an-astabstract-syntax-tree/)
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d36ebfbd-0026-4ddf-868a-8fe41ece047c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T085733Z&X-Amz-Expires=86400&X-Amz-Signature=23fa9b12a555bcab60a54dd5f9d2df9d6ab954f690a951772fd24d41d80f14ce&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
        
        [https://www.researchgate.net/figure/Java-Hello-World-AST_fig1_304539782](https://www.researchgate.net/figure/Java-Hello-World-AST_fig1_304539782)
        
        - 추상 구문 트리
        - abstract syntax tree
        - AST 가 컴파일 단계중 구문 분석 단계의 결과물
        - AST 는 프로그래밍 언어로 작성된 소스코드의 추상 구문 구조의 트리
            
            이 트리의 각 노드는 소스코드에서 발생되는 구조를 나타낸다. 
            
            → 소스코드를 문법에 맞게 노드들로 쪼개서 만든 트리
            

---

- 참고
    - 남궁성 - 자바의 정석
    - [https://docs.oracle.com/javase/tutorial/java/annotations/index.html](https://docs.oracle.com/javase/tutorial/java/annotations/index.html)
    - [https://steady-coding.tistory.com/614](https://steady-coding.tistory.com/614)
    - [https://cla9.tistory.com/52](https://cla9.tistory.com/52)
    - [https://roadj.tistory.com/9](https://roadj.tistory.com/9)
    - [https://catsbi.oopy.io/78cee801-bb9c-44af-ad1f-dffc5a541101](https://catsbi.oopy.io/78cee801-bb9c-44af-ad1f-dffc5a541101)
    - [https://im-recording-of-sw-studies.tistory.com/37](https://im-recording-of-sw-studies.tistory.com/37)
    - [https://www.javacodegeeks.com/2015/09/java-annotation-processors.html](https://www.javacodegeeks.com/2015/09/java-annotation-processors.html)
    - [https://medium.com/@jason_kim/annotation-processing-101-번역-be333c7b913](https://medium.com/@jason_kim/annotation-processing-101-%EB%B2%88%EC%97%AD-be333c7b913)
    - [https://blogshine.tistory.com/439](https://blogshine.tistory.com/439)
    - [https://shinwusub.tistory.com/150](https://shinwusub.tistory.com/150)
    - [https://www.happykoo.net/@happykoo/posts/256](https://www.happykoo.net/@happykoo/posts/256)
    - [https://gyrfalcon.tistory.com/entry/Java-Reflection](https://gyrfalcon.tistory.com/entry/Java-Reflection)