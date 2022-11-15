# 1회차 - JVM

<aside>
➡️ 작성일 : 2022.10.29

</aside>


---

# JDK / JRE / JVM 

![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/7233e4a1-ce31-4863-a1be-93da068576f2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T090028Z&X-Amz-Expires=86400&X-Amz-Signature=ea75e301609d5bc5281ac65574c7d1396ac03d5c98b1a81d20dcce866c4ce81b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- [https://coderhalt.com/difference-between-jdk-jre-and-jvm-in-java/](https://coderhalt.com/difference-between-jdk-jre-and-jvm-in-java/)
- JDK , JRE, JVM 은 자바 프로그래밍에 사용되는 3대 핵심 기술 패키지
- *JDK 를 다운로드 시 호환버전의 JRE 가 포함되고 JRE 에는 JVM 이 포함된다.*
- 각각은 기술적 정의(스펙)임과 동시에 이를 토대로 만들어진(구현된) 여러 종류(제품)가 있다.

---

# JDK

- Java Development Kit
- 개발자가 자바 기반의 애플리케이션 개발을 위해 다운로드 하는 소프트웨어 패키지
- 자바로 개발하는데 사용된다. 
( JVM 과 JRE 에 의해 실행, 구동 될 수 있는 프로그램 개발 시 사용 )
- **설치**
    - 설치 시 자바 버전(8, 11 등 )과 자바 패키지(EE, SE, ME)를 선택해야한다.
        - 자바 패키지
            - 필요시 다른 JDK 로 전환 가능
            - SE : Standard Edition (일반적으로 JDK 에 포함)
            - EE : Enterprise Edition
                - 자바 EE > 자바 SE
                - 엔터프라이즈 자바 빈 , 객체 관계 매핑(ORM ) 지원같은 엔터프라이즈 앱 개발에 유용한 추가 도구를 가지고 있다.
            - ME : Mobile Edition
    - 설치 후 path 를 등록해주는 과정이 필요하다.
- **버전**
    - JDK 1.5 부터 5.0 이라고 부르기도 함
    - JDK 8.0 == JDK 1.8
    - LTS 버전 은 8 , 11, 17 이 있다.
- **구성**
    - 실행을 위한 JRE 를 포함하고 있다.
    - JDK 안에는 개발 시 필요한 라이브러리들과 javac, javadoc 등의 개발 도구들이 포함
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/ea032248-248d-486e-9c4b-510ae4bcfe89/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T090054Z&X-Amz-Expires=86400&X-Amz-Signature=d5f56a3ac7d5fb6acccbc669cf29ec42860a17ca825dce02738b203ce4923a95&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
        
        [https://docs.oracle.com/javase/8/docs/](https://docs.oracle.com/javase/8/docs/)
        
        - 주요 도구
            - JDK 의 bin 디렉토리에서 확인 가능
            - javac.exe
                - 자바 컴파일러
                - Java 클래스 및 인터페이스 정의를 읽고 바이트 코드 및 클래스 파일로 컴파일 할 수 있다. → 자바 소스코드(.java)를 바이트코드로(.class) 컴파일
            - java.exe
                - 자바 인터프리터
                - 컴파일러가 생성한 바이트코드를 해석하고 실행시킨다.
            - javap.exe
                - 역어셈블러
                - 컴파일 된 클래스 파일을 원래의 소스로 변환
            - javadoc.exe
                - 자동문서생성기
                - 소스파일에 있는 주석을 이용하여 Java API 문서와 같은 형식의 문서를 자동으로 생성
            - jar.exe
                - 압축프로그램
                - 클래스 파일과 프로그램의 실행에 관련된 파일을 하나의 jar(.jar)로 압축하거나 압축해제한다.
                - .jar 파일은 패키지 된 자바 클래스 세트이다.
                - .class 파일을 생성한다음 .jar

---

# JRE

- Java Runtime Environment
- JRE 와 JVM 을 통해 자바의 특징을 구현 (한번 작성하고 모든곳에서 실행한다.)
- JDK 를 다운로드 시 호환버전의 JRE 가 포함되고 JRE 에는 JVM 이 포함된다.
- **구성**
    - 클래스 로더
    - JVM
    - Java 플랫폼 코어 클래스 및 지원하는 Java 플랫폼 라이브러리로 구성
- **런타임 환경이란**
    - 운영체제가 응용프로그램이나 소프트웨어에 제공하는 실행환경
    - 프로그램 실행을 위해 클래스 파일을 로드하고 메모리 및 기타 시스템 리소스에 대한 엑세스를 확보한다.
- **자바 런타임 환경 ( JRE )**
    - 컴퓨터 운영체제 위에서 실행되면서 자바를 위한 부가적인 서비스를 제공하는 소프트웨어 계층이다.
    - 추상화의 전형적인 사례로 기반 운영체제를 자바 어플리케이션 실행을 위한 일관적인 플랫폼으로 추상화 한다.
    
    > *JRE 에는 자바 실행에 필요한 라이브러리와 소프트웨어가 포함된다. 
    (ex : 클래스 로더 )
    JRE 는 자바 코드를 받아 필요한 라이브러리와 결합한 다음 해당 코드를 실행할 JVM 을 시작하는 역할. 즉 온디스크 시스템이라고 볼 수 있다.*
    > 

---

- **JDK 의 자바 어플리케이션 개발에서의 생명주기**

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/45e544fa-0c23-45ca-b4d3-a036941ed021/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T090131Z&X-Amz-Expires=86400&X-Amz-Signature=b089e8027aca448705d6277e82e14dcc70a00138c93c4631b868276534f1192d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

[https://www.infoworld.com/article/3296360/what-is-the-jdk-introduction-to-the-java-development-kit.html](https://www.infoworld.com/article/3296360/what-is-the-jdk-introduction-to-the-java-development-kit.html)

# 컴파일 하는 방법 및 과정

- javac(컴파일러) 를 이용하여 컴파일 하는 방법
    - [https://docs.oracle.com/en/java/javase/11/tools/javac.html#GUID-AEEC9F07-CB49-4E96-8BC7-BCC2C7F725C9](https://docs.oracle.com/en/java/javase/11/tools/javac.html#GUID-AEEC9F07-CB49-4E96-8BC7-BCC2C7F725C9)
    - 파일 위치 이동 후
    
    ```bash
    	>>> javac 파일명.java
    ```
    
    - 컴파일 결과로 바이트코드(파일명.class)가 생성
    

---

# 바이트코드란 무엇인가 (Bytecode)

- 컴파일러가 컴파일 한 결과로 생성된다.
    
    > *자바 컴파일러에 의해 변환되는 코드의 명령어 크기가 1바이트라서 바이트 코드라고 불린다.*
    > 
- 자바로 컴파일 된 코드
- .class 확장자가 붙는다.
- JVM이 이해할 수 있는 기계어
JVM은 이 바이트코드를 해당 OS 의 기계어로 변환하여 OS 로 전달함

---

# 실행하는 방법

- JDK 의 java.exe 를 통해 실행
    - [https://docs.oracle.com/en/java/javase/11/tools/java.html#GUID-3B1CE181-CD30-4178-9602-230B800D4FAE](https://docs.oracle.com/en/java/javase/11/tools/java.html#GUID-3B1CE181-CD30-4178-9602-230B800D4FAE)
    
    ```bash
    >>> java 파일명 
    ```
    
    - class, jar 파일 등이 실행 가능 (사용법 문서 참고)
    - class 파일의 확장자는 붙이지 않는다.
        
        > *java 명령은 JRE 를 시작하고 지정된 클래스를 로드하고 해당 클래스의 `main()`메서드를 호출하여 이를 수행합니다.*
        > 

---

# JVM이란 무엇인가

- Java Virtual Machine
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b4e8c569-ddbf-46f0-8873-cbbf052c2d70/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T090202Z&X-Amz-Expires=86400&X-Amz-Signature=b7941c306213749e3c04cd77bb3932238a07ff4eced476254966641fb81f0fcb&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    [https://medium.com/@ahn428/java-jvm-java-virtual-machine-jre-java-runtime-environment-jdk-java-developement-kit-fed91def1d6f](https://medium.com/@ahn428/java-jvm-java-virtual-machine-jre-java-runtime-environment-jdk-java-developement-kit-fed91def1d6f)
    
- 자바(변환된 .class 파일)를 실행하기 위한 가상머신
- 자바 언어로 작성된 어플리케이션은 모두 JVM 에서만 실행
- 실행을 위해선 JVM 이 반드시 필요하다.
    
    > *자바 바이트코드는 플랫폼에 독립적이며 모든 자바 가상 머신은 자바 가상 머신 규격에 정의된 대로 자바 바이트코드를 실행한다. 따라서 표준 자바 API까지 동일한 동작을 하도록 구현한 상태에서는 이론적으로 모든 자바 프로그램은 CPU나 운영 체제의 종류와 무관하게 동일하게 동작할 것을 보장한다.*
    > 
- **JVM 의 주요 목적**
    1. 한번 작성한 자바코드로 
    어느 기기, 어느 운영체제상에서도 실행될 수 있도록 하는것 
    (한번 작성하고 모든곳에서 실행한다.)
    1. 프로그램 메모리를 관리하고 최적화 시키는것
- Java 어플리케이션은 JVM 하고만 상호작용을 하기 떄문에 OS 와 하드웨어에 독립적이다.
- **주의 : JVM 이 어플리케이션과 OS 사이에서 상호작용해주기에 Java 가 OS 에 독립적인것이다. JVM 은 OS 에 종속적이다.(JVM 은 OS 에 독립적이지 못하다.)**
- JVM 은 JRE 에 포함되어있다. 따라서 JRE 가 설치되어있다면 JVM 역시 설치되어있는것이다.

---

# JVM 구성 요소

- Class Loader 는 JRE 에 속하나 JVM 동작상 필요하므로 함께 설명
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4497fbef-65fb-4cdc-996d-f6dd80e6e0f0/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T090230Z&X-Amz-Expires=86400&X-Amz-Signature=6340e5ef2908547caa0691328a8c51062dc06a43a5e6ff08d561451a101c6523&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    [https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html](https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/02021582-a1c8-49ef-bfb7-a9b94f50261d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221115%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221115T090250Z&X-Amz-Expires=86400&X-Amz-Signature=0d459ccfb725df9422c59bb1f3e6d475ac54ac6aa2d6c6b548f6337752abe834&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    [https://velog.io/@host92/JVMJava-Virtual-Machine](https://velog.io/@host92/JVMJava-Virtual-Machine)
    

- **JVM 동작과정은 크게 4가지로 구성된다.**
    - Class Loader
    - Excution Engine
    - Runtime Data Area
    - Garbage Collection

---

# JVM 동작과정

[JVM 동작 과정 ](round1-1.md)

- JIT 컴파일러란 무엇이며 어떻게 동작하는지 포함

---

- 참고
    - 남궁성 - 자바의 정석
    - 바이트코드란
        - [http://www.tcpschool.com/java/java_intro_programming](http://www.tcpschool.com/java/java_intro_programming)
    - JRE 와 자바 런타임 환경
        - [https://www.itworld.co.kr/news/110768](https://www.itworld.co.kr/news/110768)
    - JDK / JRE
        - [https://www.itworld.co.kr/news/110817](https://www.itworld.co.kr/news/110817)
    - JDK 종류
        - [https://bonohubby.com/entry/JDK-종류-총-정리-Oracle-JDK-OpenJDK-Adpot-Corretto-Zulu?category=0](https://bonohubby.com/entry/JDK-%EC%A2%85%EB%A5%98-%EC%B4%9D-%EC%A0%95%EB%A6%AC-Oracle-JDK-OpenJDK-Adpot-Corretto-Zulu?category=0)
    - JDK 구현체 종류
        - [https://m.blog.naver.com/pcmola/222054565339](https://m.blog.naver.com/pcmola/222054565339)
    - JIT
        - [https://dicksonkho.com/software-road/brief-introduction-to-sdk-jre-jvm-jit/](https://dicksonkho.com/software-road/brief-introduction-to-sdk-jre-jvm-jit/)
    - JVM 이란
        - [https://velog.io/@host92/JVMJava-Virtual-Machine](https://velog.io/@host92/JVMJava-Virtual-Machine)
        - [https://d2.naver.com/helloworld/1230](https://d2.naver.com/helloworld/1230)
        - [https://ko.wikipedia.org/wiki/자바_가상_머신](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%EA%B0%80%EC%83%81_%EB%A8%B8%EC%8B%A0)
        - [https://coding-factory.tistory.com/827](https://coding-factory.tistory.com/827)
        - [https://www.itworld.co.kr/news/110837](https://www.itworld.co.kr/news/110837)
        - [https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html](https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)
    - Java SE 란
        - [https://doozi316.github.io/java/2020/07/01/WEB20/](https://doozi316.github.io/java/2020/07/01/WEB20/)
    - 어셈블러
