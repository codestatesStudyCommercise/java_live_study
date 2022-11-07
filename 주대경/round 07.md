# 제어자와 접근 제어자

**modifier**

- 제어자란 클래스, 멤버(필드, 메소드, 생성자 등) 선언 시 부가적인 의미를 부여하는 키워드.
- 접근 제어자와 기타 제어자로 구분.
- 기타 제어자는 경우에 따라 여러 개를 함께 사용 가능하지만, 접근 제어자는 여러 개를 동시에 사용 불가.

| 제어자      | 종류                                |
| ----------- | ----------------------------------- |
| 접근 제어자 | public, protected, default, private |
| 기타 제어자 | static, final, absteact, …          |

# 접근 제어자

**access modifier**

- (캡슐화를 통한) 정보의 은닉화 구현을 위해 존재.
- 클래스 외부에서의 직접적인 접근을 허용하지 않는 멤버를 설정하여 정보 은닉을 구체화
- 자바에서는 네 가지의 접근 제어자 제공

| 접근 제어자 | 접근 제한 범위                            |
| ----------- | ----------------------------------------- |
| public      | 접근 제한 없음.                           |
| protected   | 동일 클래스 및 패키지 + 하위(자손) 클래스 |
| default     | 동일 패키지 내에서만 접근 가능            |
| private     | 동일 클래스 내에서만 접근 가능.           |

| 제어자    | 클래스 내부 | 패키지 내부 | 다른 패키지 내부의 자식 클래스 | 다른 패키지의 다른 클래스 |
| --------- | ----------- | ----------- | ------------------------------ | ------------------------- |
| public    | o           | o           | o                              | o                         |
| protected | o           | o           | o                              | x                         |
| default   | o           | o           | x                              | x                         |
| private   | o           | x           | x                              | x                         |

# Public

- public 제어자로 선언된 클래스의 멤버는 외부로 공개됨.

- 해당 객체를 사용하는 프로그램 어디에서나 접근이 가능.

- 보통 private 멤버에 안전하게 접근하기 위해 public 메소드를 선언하여 선언.

![study.drawio-3.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/951f9cb4-2e7d-48ce-b495-d0e8336b1141/study.drawio-3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221107%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221107T041514Z&X-Amz-Expires=86400&X-Amz-Signature=7962b344623dd22ec752cc988054dda96b39ebb239bba22210efbc0a311cb445&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22study.drawio-3.png%22&x-id=GetObject)

```java
package org.other;

public class A {
  public String var = "누구든지 허용"; // public 필드

  public String getVar() {          // public 메소드
    return this.var;
  }
}

// 다른 패키지
package org.App;

import org.other.A;

public class App {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        A a = new A();
        System.out.println(a.var);      // "누구든지 허용"
        System.out.println(a.getVar()); // "누구든지 허용"
    }

}
```

# Protected

- 같은 패키지와 외부 패키지 내부의 자식 클래스까지 접근 가능.

![study.drawio-4.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ba955939-dc86-4e68-b925-d11e06327a66/study.drawio-4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221107%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221107T041538Z&X-Amz-Expires=86400&X-Amz-Signature=f9893bcd057e32d6d62751b30428b105f3f738998c1f1a05006b9b029a584106&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22study.drawio-4.png%22&x-id=GetObject)

```java
package org.other;

public class A {
  protected String sameVar = "다른 패키지에 속하는 자식 클래스까지 허용"; // protected 필드
}

// 다른 패키지
package org.App;

import org.other.A;

class B extends A {
    public void msg() {
        System.out.print(sameVar);
    }
}

public class App {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        A a = new A();
        // System.out.println(a.sameVar); 멤버가 보이지 않아 참조 불가
        B b = new B();
        b.msg();                       // "다른 패키지에 속하는 자식 클래스까지 허용"
    }
}
```

# Default

- 기본 접근 제어자.

- 별도의 접근 제어자 삽입 불필요.

- 같은 클래스의 멤버와 같은 패키지 내의 모든 멤버에서 접근 가능.

![study.drawio-5.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/9996cc19-9bfd-42dd-8f5d-a3ddb9f964d1/study.drawio-5.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221107%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221107T041556Z&X-Amz-Expires=86400&X-Amz-Signature=cbf5332806f7c7930ed2a0481fe444e97128a50d5e588d75b641fd89378087fb&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22study.drawio-5.png%22&x-id=GetObject)

```java
package org.other;

public class A {
  String sameVar = "다른 패키지에 속하는 자식 클래스까지 허용"; // default 필드
}

// 다른 패키지
package org.App;

import org.other.A;

// 다른 패키지의 자식
class B extends A {
    public void msg() {
        // System.out.print(sameVar);    멤버가 보이지 않아 참조 불가
    }
}

// 같은 패키지
class C {
    String str = "같은 패키지까지 허용";    // default 필드
}

public class App {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        A a = new A();
        // System.out.println(a.sameVar); 멤버가 보이지 않아 참조 불가
        C d = new C();
        System.out.print(d.str);       // "같은 패키지까지 허용"
    }
}
```

# Private

- 해당 클래스 멤버는 외부에 공개되지 않음. (외부에서 접근 불가.)

- 해당 객체의 public 메소드를 통해서만 접근이 가능.

- 클래스 내부의 세부적인 동작을 구현하는데 사용하는 멤버에 적용.

![study.drawio-7.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/bdc9d53b-c3ea-4181-803f-2124d42102a0/study.drawio-7.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221107%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221107T041614Z&X-Amz-Expires=86400&X-Amz-Signature=db32bde51ff214cd6472a9bfc428c1819bab5602bbb9e427e52ee35f52fb218e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22study.drawio-7.png%22&x-id=GetObject)

```java
package org.App;

class A {
    private int data = 40;                // private 필드

    private void msg() {
        System.out.println("Hello java"); // private 필드
    }

    public void setter(int a) {           // public 메소드
        this.data = a;
        System.out.println("Hello java" + data);
    }
}

public class App {
    public static void main(String args[]) {
        A obj = new A();
        // System.out.println(obj.data); 멤버가 보이지 않아 참조 불가
        // obj.msg();                    멤버가 보이지 않아 참조 불가
        obj.setter(50);               // "Hello java50"
    }
}
```
