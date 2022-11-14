<br>

# **✅** Annotation 정의하는 방법

<br>

애너테이션도 직접 만들어서 사용할 수 있다. 

<br>

![image](https://user-images.githubusercontent.com/48430781/201668247-16552828-f9d0-4a70-a796-a800bb8ad37e.png)

<br>

## **⏺**  왜 Custom Annotation을 사용할까?

<br>

- 코드 작성 노력을 줄이기 위해(컴파일 시 주석 프로세서가 코드를 생성합니다).
- 추가 정확성 보장을 제공하기 위해(컴파일 시 주석 프로세서가 오류에 대해 경고합니다). 이를 위한 좋은 도구 중 하나 는 null 포인터 역참조, 동시성 오류 등을 방지 하는 [Checker Framework 입니다.](http://checkerframework.org/)
- 동작을 사용자 지정하려면(런타임에 코드가 리플렉션을 사용하여 주석을 확인하고 주석이 있는지 여부에 따라 다르게 동작합니다). [Hibernate](http://www.tutorialspoint.com/hibernate/hibernate_annotations.htm)[Oracle 기사](http://www.oracle.com/technetwork/articles/hunter-meta-3-092019.html)

    와 같은 프레임워크는 이러한 방식으로 주석을 사용합니다.

<br>

- 어노테이션을 써서  런타임 또는 컴파일 시간에 사용할 수 있는 **클래스 파일에 메타 정보를 직접 추가** 함.
    
    → 컴파일 시 annotation processor가 추가적인 정확성을 보장하기 위해 오류에 대해 경고를 날림
    
- **웹기술 프레임워크에서 XML을 피하기 위해 주석(애노테이션)을 사용한다.**
    
    →  web.xml : **DD** (Deployment Descriptor : 배포 설명자)라고 불리며, **Web Application의 설정파일**이다. DD는 Web Application 실행 시 메모리에 로드된다.
    
<br>

✔️  **Spring에서 주석과 xml 기반 프로그래밍의 차이점은?**

<br>

[Difference between annotation and xml based programming in Spring? Which one is better?](https://www.quora.com/Difference-between-annotation-and-xml-based-programming-in-Spring-Which-one-is-better)

1) annotation이 없었을 땐 xml기반 구성을 했으며, 각 클래스가 무슨 역할을 하는지 보기 위해서 xml파일로 이동해 확인해야했다. 

2) annotation은 클래스 바로 위에 어떤 역할을 하는지 명시하기 때문에 이동할 필요가 없고, 간결 및 가독성이 뛰어나다.

<br>

<<어떤 사람>>

🧑‍💻 XML

<br>

→ 변경가능성이 낮은, 수십개의 소스파일에서 configurators, factories 등을 크롤링할 필요가 없는 경우에 주로 사용

→ XML을 통해 모든 서비스, 개체 및 엔터티를 정의하는 것을 고통스러움.

<br>

🧑‍💻 Annotation 

→ 서비스, 개체 및 엔터티에 추가하는것이 좋다.

→ 조인테이블을 사용해 다대다 관계로 두 객체 조인할 때 XML은 악몽이지만 주석은 매우 간단했음

<br>

## **⏺  Annotation 정의하는 방법**

- 인터페이스 정의하는 것 앞에 @ 기호를 붙히면 됨.
- 요소를 선언해서 사용할 수 있다.

<br>

```java
public @interface Make {
	타입 요소이름(); //Annotation의 요소 선언
}
```

<br>

## **⏺** Annotation 요소

<br>

반환값이 있고 매개변수 없는 추상메서드의 형태를 가짐, 상속을 통해 구현하지 않아도 됨.

- 애너테이션 적용시 **요소들의 값을 빠짐없이 지정해주어야 함**
- 요소의 이름도 같이 적어주기 때문에 **순서는 상관 없음**
- 요소는 **기본 값을 가질 수 있다** (애너테이션 적용시 값을 지정하지 않으면 기본값이 사용 됨)
    - default 3;                            // 값 지정
    - default {”aaa”, ”bbb”};       // 기본 값이 여러개인 경우 괄호 {} 사용
    - default “ccc”;                     //  기본값이 하나인 경우 괄호 생략 가능

<br>

```java
enum TestType {FIRST, FINAL}

@interface TestInfo {
	int count() default 1;
	String testedBy();
	String[] testTools() default "aaa";
	TestType testType();
	DateTime testDate(); // 자신이 아닌 다른 애너테이션을 포함할 수 있음.
}

@interface DateTime{
	String yymmdd();
	String hhmmss();
}

--------------------------

@TestInfo(
	testedBy = "Kang",
	testTools= {"Junit","AutoTester"},
	testType = TestType.FIRST,
	testDate = @DateTime(yymmdd="221113", hhmmss="235959"),

)
public class myClass {  .....   }

```

<br>

### 애너테이션 요소 선언시 규칙

- 요소의 타입은 **기본형, String, enum, 어노테이션, Class**만 허용

- ()안에 **매개변수는 선언할 수 없다.**

- **예외를 선언할 수는 없다.(??)**

- **요소를 타입 매개변수로 정의 할 수 없다.**

<br>

## **⏺ 애너테이션 조상**

java.lang.annotation.Annotation → 인터페이스로 구성되어있음

<br>

즉  구현하기 위해 **implements   or   익명클래스**로 만들어야한다. 

<br>

```java
Annotation annotation = new Annotation() {
     @Override
     public Class<? extends Annotation> annotationType() {
        return null;
};
```

<br>

### **⏺**  애너테이션의 배치 및 사용 예시

참고 : [https://honeyinfo7.tistory.com/56#2. 어노테이션의 배치 및 사용](https://honeyinfo7.tistory.com/56#2.%20%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98%EC%9D%98%20%EB%B0%B0%EC%B9%98%20%EB%B0%8F%20%EC%82%AC%EC%9A%A9)

<br>

⚫️ **어노테이션의 사용**
클래스를 참고하는 소스의 흐름상에서   <Reflection을 사용하는 방법> 을 통해서 어노테이션 값을 활용하도록 함

<br>

---

<br>

### 후행개념 : Reflection

Reflection은 클래스의 구조를 분석하는 기능 api

Reflection를 통해서 클래스의 구조를 분석해서 메소드를 검색하고 실행할 수 있다.

- JVM이 클래스 정보는 대부분 .class에 적힌 바이트 코드대로 메모리에 올리게 된다.
- .class 파일에 적힌 자바 바이트코드대로 메모리에 올라가 있지만, 리플렉션 코드에 의해 세세한 부분까지도 접근이 가능하게 한다.
    - 구체적인 클래스 타입을 알지 못해도, 그 클래스의 메소드, 타입 변수들에 접근할 수 있도록 해주는 자바 API
    - Class  /  Constructor / Method  /Field 와 같은 정보를 찾을 수 있다.
    - 객체 생성/ 변수 변경 / 메서드 호출 등을 할 수 있다.

<br>

대충 예제

- `클래스.class` 로 가져오기
- `인스턴스.getClass()` 로 가져오기
- `Class.forName("클래스명")` 으로 가져오기

<br>

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Method;

// 테스트할 클래스  
class Node {

  // 생성자
  public Node() { }

  // 함수 생성
  public void print() {
    System.out.println("Hello world");
  }

}

public class Example {
  // 실행 함수
  public static void main(String... args) {
    try {

      // Node 클래스의 타입을 찾는다.
      Class<?> cls = Class.forName("Node");

      // Node 클래스의 생성자를 취득한다.
      Constructor<?> constructor = cls.getConstructor();

      // 생성자를 통해 newInstance 함수를 호출하여 Node 인스턴스를 생성한다.
      Object node = constructor.newInstance();

      // Node 클래스의 print함수를 취득한다.
      Method method = cls.getMethod("print");

      // 취득한 함수에 생성한 인스턴스를 넣고 실행시킨다.
      method.invoke(node);

    } catch (Throwable e) {
      e.printStackTrace();
    }
  }
}
```

<br>


### 예제 소스코드

1. Tester.java (어노테이션)

2. Service.java (사용되는 클래스)

3. Main.java (Service를 사용하는 클래스)
 
<br>
 
 ![image](https://user-images.githubusercontent.com/48430781/201668784-6ee8ddca-4769-4b05-985f-ea9e736e6265.png)

- Main 클래스가 Service 클래스의 메서드에  Tester 어노테이션 설정이 있는지 확인
- 각 메서드에 설정된 어노테이션에 삽입된 값에 따라 결과를 출력하는 예제임

<br>
 
[Tester.java]

- element로 테스터의 이름(name)과 테스트횟수(testCount) , 테스트도구 배열(testTools) 를 주었다.
- 테스터가 사람이 아닐경우, default auto machine 지정
- 테스트횟수의 기본값은 1
- 테스트도구 미지정시 Junit5를 사용한다.

<br>

```java
package Annotation_code;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
public @interface Tester {
    String name() default "auto machine";
    int testCount() default 1;
    String[] testTools() default "Junit5";
}
```

<br>

[Service.java]

- 테스터 메서드를 3개 생성
- 각 메서드 위에 @Tester 를 이용해 name과 테스트횟수, 테스트 도구를 각각 지정해줌

<br>

```java
package Annotation_code;

public class Service {

    @Tester(name = "강지은", testCount = 3, testTools = {"Junit5", "JSUnit","Qunit"})
    public void tester01(){
        System.out.println("<tester01> 테스트를 진행합니다.");
    }
    @Tester(name = "김례화", testTools = "JSUnit")
    public void tester02(){
        System.out.println("<tester02> 테스트를 진행합니다.");
    }

    @Tester(name = "전진우", testCount = 2, testTools = {"Junit5", "JSUnit"} )
    public void tester03(){
        System.out.println("<tester03> 테스트를 진행합니다.");
    }
}
```

<br>

[Main.java]

- Service.class.getMethods()

<br>

```java
package Annotation_code;
import java.lang.reflect.Method;
public class Main {

    public static void main(String[] args) {
        Method[] methodList = Service.class.getMethods();

        for (Method m : methodList) {

            if (m.isAnnotationPresent(Tester.class)) {
                System.out.println(m.getName());
                Tester tester = m.getDeclaredAnnotation(Tester.class);

                String name = tester.name();
                String[] tools = tester.testTools();
                int count = tester.testCount();
                for (int i = 0; i < count; i++) {
                    System.out.print(name + "님이 " + tools[i] + "를 이용해 테스트를 완료했습니다.\n");
                }
                System.out.println();
            }
        }
    }
}
```

<br>

**결과값**

![image](https://user-images.githubusercontent.com/48430781/201668926-85fe0f30-7b7c-4dd4-80e1-dd7bc95c6c07.png)


- **필드, 생성자, 메소드에 적용된 어노테이션 정보는 위에서 처럼 .class로부터 얻을 수 있다.**

<br>

<리플렉션>

[클래스.class.메소드]

- 다음 메서드를 이용해   java.lang.reflect 패키지의 Field, Constructor, Method 클래스의 배열을 얻어냄

| 리턴타입 | 메소드명(매개변수) | 설명 |
| --- | --- | --- |
| Field[] | getFields() | 필드 정보를 Field 배열로 리턴 |
| Constructor[] | getConstructors() | 생성자 정보를 Constructor 배열로 리턴 |
| Method[] | getDelclaredMethods() | 메소드 정보를 Method 배열로 리턴 |
|  |  |  |


<br>

**[어노테이션 정보를 얻기 위한 메소드]**

| 리턴타입 | 메소드명(매개변수) |
| --- | --- |
| boolean | isAnnotationPresent(Class<? Extends Annotation> annotationClass) |
| 지정한 어노테이션이 적용되었는지 여부. Class에서 호출했을 경우 상위 클래스에 적용된 경우에도 true를 리턴한다. |  |
| Annotation | getAnnotation(Class<T> annotationClass |
| 지정한 어노테이션이 적용되어 있으면 어노테이션을 리턴하고 그렇지 않다면 null을 리턴한다. Class에서 호출했을 경우 상위
클래스에 적용된 경우에도 어노테이션을 리턴한다. |  |
| Annotation[] | getAnnotations() |
| 적용된 모든 어노테이션을 리턴한다. Class에서 호출했을 경우 상위 클래스에 적용된 어노테이션도 모두 포함한다. 적용된
어노테이션이 없을 경우 길이가 0인 배열을 리턴한다. |  |
| Annotation[] | getDeclaredAnnotations() |
| 직접 적용된 모든 어노테이션을 리턴한다. Class에서 호출했을 경우 상위 클래스에 적용된 어노테이션은 포함되지 않는다. |  |

<br>

---

<br>

나중에 JPA 엔티티 매핑할 때 사용할 예제.. 

Employee 테이블을 사용해 객체를 저장하는 상황

<br>

```sql
create table EMPLOYEE (
   id INT NOT NULL auto_increment,
   first_name VARCHAR(20) default NULL,
   last_name  VARCHAR(20) default NULL,
   salary     INT  default NULL,
   PRIMARY KEY (id)
);
```

<br>

Employee 테이블로 객체를 매핑하기 위해, 주석을 추가한 Employee classs mapping

<br>

```java
import javax.persistence.*;

@Entity
@Table(name = "EMPLOYEE")
public class Employee {
   @Id @GeneratedValue
   @Column(name = "id")
   private int id;

   @Column(name = "first_name")
   private String firstName;

   @Column(name = "last_name")
   private String lastName;

   @Column(name = "salary")
   private int salary;

   public Employee() {}

   public int getId() {
      return id;
   }

   public void setId( int id ) {
      this.id = id;
   }

   public String getFirstName() {
      return firstName;
   }

   public void setFirstName( String first_name ) {
      this.firstName = first_name;
   }

   public String getLastName() {
      return lastName;
   }

   public void setLastName( String last_name ) {
      this.lastName = last_name;
   }

   public int getSalary() {
      return salary;
   }

   public void setSalary( int salary ) {
      this.salary = salary;
   }
}
```

<br>

@Entity 

클래스를 엔터티 빈으로 표시

<br>

@Table

데이터베이스에서 엔터티를 유지하는데 사용할 테이블의 세부정보 지정 가능

<br>

@Id , @GeneratedValue

엔터티 빈에 @Id 를 사용해 기본키를 설정할 수 있음.

<br>

@Column 

필드, 속성이 매핑될 열의 세부정보를 지정함. 

name : 열 이름을 명시적으로 지정

nullable : 스키마 생성시 열이 NOT NULL 표시되도록 허용

unique : 열이 고유값만 포함된것으로 표시 가능

…

### References

[https://www.quora.com/What-are-annotations-and-why-are-they-used](https://www.quora.com/What-are-annotations-and-why-are-they-used)

[https://velog.io/@prayme/whiteship-12주차-Enum](https://velog.io/@prayme/whiteship-12%EC%A3%BC%EC%B0%A8-Enum)

[https://b-programmer.tistory.com/264](https://b-programmer.tistory.com/264)

[https://mangkyu.tistory.com/130](https://mangkyu.tistory.com/130)

[http://www.tutorialspoint.com/hibernate/hibernate_annotations.htm](http://www.tutorialspoint.com/hibernate/hibernate_annotations.htm)

[https://www.quora.com/Difference-between-annotation-and-xml-based-programming-in-Spring-Which-one-is-better](https://www.quora.com/Difference-between-annotation-and-xml-based-programming-in-Spring-Which-one-is-better)

