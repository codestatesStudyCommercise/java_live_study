# 5주차 - import

<aside>
➡️ 작성일 : 2022.11.06

</aside>

---

# import 란

- 소스 코드작성시 패키지명을 포함한 클래스명을 매번 사용하는것이 불편함
- 이를 코드 작성 전 import 문을 통해 사용하고자 하는 클래스의 패키지를 미리 명시
    - import문 은 컴파일러에게 소스파일에 사용된 클래스의 패키지에 대한 정보를 제공하는 것
    - 컴파일 시 컴파일러는 import 문을 통해 소스파일에 사용된 클래스들의 패키지를 알아내어 모든 클래스 이름 앞에 패키지명을 자동으로 붙여준다.
- 소스코드에 서용되는 클래스 이름에서 패키지명 생략 가능

> ***
import 문은 프로그램의 성능에 전혀 영향을 미치지 않는다.
import 문을 많이 사용하면 컴파일 시간이 아주 조금 더 걸릴 뿐이다.
> 

---

## import 문의 선언 위치

- 참고 이미지 : 프로젝트 구조
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d1eebe31-cc10-417b-8c5f-5a417328541a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221107%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221107T130131Z&X-Amz-Expires=86400&X-Amz-Signature=57cabcf71159bd37a881bb6a3f68fab9f2f35694b317adbf9b7ba220cabcbb40&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    [https://boyboy94.tistory.com/13](https://boyboy94.tistory.com/13)
    

```java
// 패키지 
package com.importexam.examtest

// import 문 
import java.util.Date;
import java.lang.Math.*;

// class 선언
class SomeThingClass { ... }
```

- 위처럼 package, import, class 선언 순으로 선언한다.

---

## 동일 패키지 내 여러 클래스 import

- 같은 패키지에서 여러 클래스가 사용될 때 import 문을 여러번 사용해 주는 대신
    
    `패키지명.*` 과 같이 사용해 지정된 패키지에 속하는 모든 클래스를 사용할 수 있다. 
    
    → 실행시 성능상의 차이는 전혀 없다.
    
- 단, import 하는 패키지의 수가 많을 때는 어느 클래스가 어느 패키지에 속하는지 구별하기 어렵다는 단점이 존재하니 무분별한 사용은 자제할것
- System 이나 String 같은 java.lang 패키지의 클래스들을 import 문없이 패키지명을 생략해서 사용할 수 있는 이유는 
모든 소스파일에 묵시적으로 `import java.lang.*` 이 선언되었기 때문이다.
    - `java.lang 패키지`는 매우 빈번히 사용되는 중요 클래스들이 속한 패키지이므로 기본적으로 import 되도록 하였다.
- **주의**
    - `패키지명.*` 은 하위패키지의 클래스까지 포함하는것이 아니다.

---

## static import

- 특정 클래스의 static 맴버를 자주 사용하는 경우 
static import 문을 통해 static 맴버를 호출 시 클래스 이름을 생략할 수 있다.
    - 이를 사용하면 반복적인 클래스 이름을 적지 않아도 되므로 코드작성이 편해진다.
    - 코드가 간결해진다.
    
    ```java
    // 기존 - static import 미사용
    public class ImportTest {
        public static void main(String[] args) {
    				// 아래와 동일한 역할을 하는 예시를 위한 코드 
            System.out.println(Double.parseDouble(String.valueOf(Math.random())));
    // ,,, 이하 생략 
    
    // -----------------------------------------------------------------------
    	
    // static import 사용
    import static java.lang.Math.*;
    import static java.lang.System.out;
    import static java.lang.Double.*;
    
    public class ImportTest {
        public static void main(String[] args) {
    				// 위와 동일한 역할을 하는 예시를 위한 코드 
    				out.println(parseDouble(String.valueOf(random())));
    // ,,, 이하 생략 
    
    ```
    

---

- 참고
    - 남궁성 - 자바의 정석
