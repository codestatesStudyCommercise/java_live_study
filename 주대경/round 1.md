# JVM

- 자바 가상 머신(Java Virtual Machine)
- 자바 바이트코드를 실행할 수 있는 런타임 환경을 제공하는 주체.
  - JVM 덕에 Java는 플랫폼 독립적(Platform Independent, Write Once Run Anywhere)
    ![study.drawio-3.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b36b4ecc-4b89-44ce-918a-51a07b17c3bd/study.drawio-3.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T112310Z&X-Amz-Expires=86400&X-Amz-Signature=8260f597e6cc619af9eab7dc4d4cc4f8862ea5c41113898714ba7b69de8d754d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22study.drawio-3.png%22&x-id=GetObject)
  - 프로그램 메모리 최적화 및 관리.

# javac

터미널에 `javac 파일명.java` 입력.

# java

`java 파일명.class` 입력으로 실행

# Bytecode

고급 언어로 작성된 소스코드를 특정 하드웨어가 아닌 가상 컴퓨터(VM)위에서 돌아가는 어플리케이션을 위해 컴파일한 중간 코드, 혹은 의사 코드.

# JIT Compiler

JIT 컴파일러(Just-In-Time) : 실행 시점에서 인터프리트 방식으로 기계어 코드를 생성하면서 그 코드를 캐싱하여, 같은 함수가 여러 번 불릴 때 매번 기계어 코드를 생성하는 것을 방지.

기본적으로 사용 가능하며 메소드가 호출될 때 활성화.

해당 메소드의 바이트코드를 원시 기계 코드로 컴파일하여 "적시에" 컴파일하여 실행.

메소드가 컴파일되면 JVM은 해당 메소드의 컴파일된 코드를 해석하는 대신 직접 호출.

# JVM 구성 요소

![study.drawio.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/df528c75-36a0-4ea3-a87e-3999ec563ffa/study.drawio.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T112338Z&X-Amz-Expires=86400&X-Amz-Signature=1cd0679d610986e4cc77c19decd62325511cd5c0781489ba37c6ed1555fcc986&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22study.drawio.png%22&x-id=GetObject)

## 클래스로더

클래스 파일을 적재하는 JVM의 하위 시스템. 자바 어플리케이션을 처음 실행하면 클래스 파일이 클래스로더에 의해 적재됨.

1. 로드 : 클래스 파일을 가져와 JVM 메모리 영역에 적재
2. 검증 : 코드가 Java, JVM 명세에 맞는지 검증
3. 준비 : 클래스가 필요로 하는 메모리 할당(필드, 메서드, 인터페이스 등등)
4. 분석 : 클래스의 [상수 풀](https://blog.breakingthat.com/2018/12/21/java-constant-pool%EA%B3%BC-string-pool/) 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경.
5. 초기화 : 클래스 변수 초기화.

## 메모리 영역

- Class(Method) : 상수 풀, 필드(멤버 변수) 및 메서드 데이터, 메서드 코드와 같은 클래스별 구조를 저장.
- Heap : 객체가 할당되는 데이터 영역.
- Stack : 프레임을 저장. 로컬 변수와 부분 결과를 보유하고 메서드 호출 및 반환에 역할.
  각 스레드에는 스레드와 동시에 생성된 전용 JVM 스택이 존재.
  메서드가 호출될 때마다 새 프레임이 생성됩니다. 메서드 호출이 완료되면 프레임이 삭제.
- PC Register : 현재 실행 중인 Java 가상 시스템 명령의 주소가 존재.
- Native Method Stack : 응용 프로그램에 사용되는 모든 기본 메서드가 포함.

## 실행 엔진

- 인터프리터 : JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 실행.
- JIT 컴파일러(Just-In-Time) : 실행 시점에서 인터프리트 방식으로 기계어 코드를 생성하면서 그 코드를 캐싱하여, 같은 함수가 여러 번 불릴 때 매번 기계어 코드를 생성하는 것을 방지.
- GC(Garbage Collecter) :

## 자바 네이티브 인터페이스

- C, C++ 어셈블리와 같은 다른 언어로 작성된 다른 응용 프로그램과 통신할 수 있는 인터페이스를 제공하는 프레임워크.

## 네이티브 메서드 라이브러리

- 네이티브 라이브러리는 "네이티브" 코드를 포함하는 라이브러리.
- 특정 하드웨어 아키텍처 또는 운영 체제용으로 컴파일된 코드.
- 프로젝트에 이러한 네이티브 라이브러리를 포함하면 애플리케이션의 플랫폼 독립성이 깨질 수 있음.

![study.drawio-4.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/75ce91c3-7a89-41f1-ab5f-579abe47fe92/study.drawio-4.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T112409Z&X-Amz-Expires=86400&X-Amz-Signature=ad63f2484161dd6665d925ee414daef11b171140bad736551df09ad3ed8109b3&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22study.drawio-4.png%22&x-id=GetObject)

# JDK vs JRE

## JDK

Java Development Kit

자바 어플리케이션 개발을 하는데 있어서 필요한 필요한 도구 모음

## JRE

Java Runtime Evironment

자바 어플리케이션 실행을 위한 환경과 그에 필요한 파일들
