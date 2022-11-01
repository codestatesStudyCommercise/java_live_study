# JVM 동작 과정

<aside>
➡️ 작성일 : 2022.10.30

</aside>

---

# 1. Class Loader

> 클래스 로더는 자바 바이트코드를 JVM 으로 동적으로 로드하는 JRE 의 일부이다.
> 

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c7fb608d-384c-4c0e-b83c-32066cfcd147/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T133654Z&X-Amz-Expires=86400&X-Amz-Signature=77eef4300bbecfc7bd2b28bced3656b57246787433222ea35a8d01dc0575fa1e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

[https://coding-factory.tistory.com/827](https://coding-factory.tistory.com/827)

- **JVM은 RAM에 상주** 합니다 . 실행하는 동안 클래스 로더 하위 시스템을 사용하여 클래스 파일을 RAM으로 가져옵니다.
- 자바어플리케이션은 클래스 파일(바이트코드)을 동적으로 읽어와 실행하는 특징을 가지고 있다.
- 이 특징은 JVM 이 동작하다가 클래스 파일을 참조하는 순간(프로그램에 의해 호출 될 때) 동적으로 class 파일을 읽어서 메모리에 로드되면서 JVM 에 링크되는 방식으로 동작되기 때문이다.
    
    (즉 컴파일 타임에 모든 class파일을 loading 하는 것이 아닌 runtime 에 동적으로 loading 된다.)
    
- 해당 동작 과정중 클래스 로더는 동적으로 클래스파일(바이트코드)들을 운영체제로 부터 할당받은 메모리(Runtime Data Area 의 Method Area)에 로딩시키는 역할을 담당한다.
- **클래스로더는 4가지 주요 원칙을 따르며 3가지 유형의 클래스 로더가 있다.**
    - [https://blog.hexabrain.net/397](https://blog.hexabrain.net/397)
    - 원칙
        - Visibility Principle (가시성 원칙)
            - 자식 클래스 로더는 부모 클래스 로더가 로드한 클래스를 볼 수  있지만 
            부모 클래스 로더는 자식 클래스 로더가 로드한 클래스를 볼 수 없다.
        - Uniqueness Principle  (유일성 원칙)
            - 부모클래스가 로드한 클래스를 자식 클래스 로더가 다시 로드하지 않아야한다.
            - 이미 로딩한 클래스를 다시 로드하지 않아야한다.
            - 클래스가 한번만 로드될 수 있도록 보장
        - Delegation Hierarchy Principle (위임 계층 원칙)
            - 참고 : class path 클래스 패스
                
                > 시스템의 모든 폴더를 JVM이 검사하도록 하는 것은 비현실적이므로 JVM에 찾아볼 파일 경로를 제공해야 합니다.
                클래스 패스는 JVM이 프로그램을 실행할 때, 클래스 파일을 찾는 데 기준이 되는 파일 경로를 말합니다.
                > 
            - JVM 은 클래스 로딩 요청을 받을 클래스 로더를 선택하기 위해 위임계층을 따른다.
            - 계층 구조로 인해 가시성, 유일성 원칙을 충족 가능
                
                ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f0f9239a-e78c-4b09-aaf9-a59c87707ee1/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T133825Z&X-Amz-Expires=86400&X-Amz-Signature=c174b29396aa267e2b3cba4039f64d766659cd3e7b1faee90cd7745d18374e67&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
                
                [https://blog.hexabrain.net/397](https://blog.hexabrain.net/397)
                
            - 가장 아래 있는 애플리케이션 클래스 로더가 자신이 받은 클래스 로딩 요청을 부모인 확장 클래스 로더에게 위임하고 
            확장 클래스 로더는 부모인 부트스트랩 클래스 로더에게 위임한다.
            - 이후 요청한 클래스가 부트스트랩 클래스 패스에 있으면 해당 클래스를 로드합니다. 
            없으면 요청을 자식 클래스로더에게 위임
            - 만약 애플리케이션 클래스 패스까지 클래스 로드에 실패하면 
            런타임 예외인 java.lang.ClassNotFoundException 발생
            
        - No Unloading Principle (언로딩 금지 원칙)
            - 클래스로더는 클래스를 로드할 순 있지만 언로드 할 순 없다.
            - 현재 클래스 로더를 제거하고 새로운 클래스 로더를 만들 수 있다.
    - 종류
        - Bootstrap Class Loader (부트스트랩) (부모)
            - 가장 필수가 되는 Library class 들을 load 한다.
            - 부트스트랩 클래스패스
                - %JAVA_HOME%/jre/lib)
            - 자바에서 기본적으로 제공하는 API 등과 같은 표준 JDK 클래스들을 부트스트랩 클래스패스에 있는 rt.jar에서 로드한다.
                
                > 이 클래스로더는 C/C++와 같은 네이티브 언어로 구현되며 자바에서 모든 클래스로더의 부모 역할을 합니다.
                > 
        - Extention Class Loader (확장)
            - 자바 9 이후부터는 확장 메커니즘이 제거되어 플랫폼 클래스 로더로 명칭이 변경 (계층은 유지)
            - 확장 클래스 패스
                - $JAVAHOME/jre/lib/ext 또는
                - 환경변수 java.ext.dirs 에 지정된 경로
            - 클래스 로드 요청을 부트스트랩 클래스 로더에 위임
            - 부트스트랩 클래스 로더가 로드에 실패하면 확장 클래스 패스의 확장 디렉토리에서 클래스를 로드
                
                > 이 클래스로더는 sun.misc.Launcher$ExtClassLoader 클래스로 자바에 구현되어 있습니다.
                > 
        - Application Class Loader (어플리케이션) (자식)
            - 시스템 클래스 로더 라고도 한다.
            - 개발자가 작성한 클래스 파일을 load
            - CLASSPATH 환경변수, 명령행 인수 -classpath 나 -cp 로 지정된 경로에서 클래스를 로드한다.
                
                > 이 클래스 로더는 sun.misc.Launcher$AppClassLoader 클래스로 자바에 구현되어 있습니다.
                > 
- **동작**
    - 클래스 파일은 클래스 로더의 3단계를 거쳐 JVM 에서 사용될 수 있게 된다.
    - 처음으로 클래스를 참조할 때 클래스 파일(.class)을 로드하고, 링크하고, 초기화 한다.
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/5448c1f5-5dc9-4d36-8892-d789019c0b78/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T133710Z&X-Amz-Expires=86400&X-Amz-Signature=0e92275b5cef82653769814e25c105328c328e14383ff14390be0398ea7c1f41&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
        
        [https://javatutorial.net/jvm-explained/](https://javatutorial.net/jvm-explained/)
        
    - 각각의 단계는 다음과 같다.
        - 1. Loading
            - class 파일을 JVM의 메모리에 올려주는 과정
                
                > 이 컴포넌트는 하드웨어 시스템에서 JVM 메모리로 .class 파일의 로드를 처리하고 
                바이너리(이진) 데이터(
                완전 수식 클래스명(fully qualified class-name), 
                직접 부모 클래스명(immediate parent class-name), 메서드, 변수, 생성자 등에 관한 정보 등
                )를 Method Area 에 저장합니다. 
                로드된 .class 파일마다 JVM은 즉시 java.lang.class 타입의 개체를 heap 메모리 상에 만듭니다. 개발자가 클래스를 여러 번 호출해도 하나의 클래스 객체만 생성된다는 것을 기억하세요. [ps://www.javacodegeeks.com/2018/04/jvm-architecture-jvm-class-loader-and-runtime-data-areas.html](https://www.javacodegeeks.com/2018/04/jvm-architecture-jvm-class-loader-and-runtime-data-areas.html)
                > 
        - 2. Linking
            - 로드된  클래스나 인터페이스, 그 직계 부모클래스나 인터페이스, 필요한 경우 요소 타입(배열 타입인 경우)를 
            검증하고, 준비하고, 해석하는 과정을 거친다.
            - 2-1. Verification (검증)
                - 클래스 파일(바이트코드)이 올바른지 검증 하여 .class 파일의 정확성을 보장
                    - 자바언어명세서를 따르고 있는지
                    - JVM 규격에 따라 검증된 컴파일러에서 .class 파일이 생성되는지 등
                - 내부적으로 바이트코드 검증기가 해당 과정을 담당
                    - 검증이 실패하면 런타임에러(java.lang.VerifyError) 를 발생
            - 2-2. Preparation (준비)
                - 클래스(바이트코드)와 인터페이스 등에 필요한 static field 메모리 할당 및 기본값으로 초기화 (기본값 ≠ 초기값)
                - JVM 에서 쓰이는 자료구조나 정적 기억영역을 위해 메모리를 할당
                    - 메모리가 부족하면 java.lang.OutOfMemoryError가 발생
                - 해당 단계에서 정적 필드가 생성되고 기본값으로 초기화 된다. (단, 값은 초기화 단계에서 할당하므로 초기화 블록이나 초기화 코드는 해당 단계에서실행하지 않는다.)
                    - ***자료형에 따른 기본값
                        - [https://blog.hexabrain.net/397](https://blog.hexabrain.net/397)
                        
                        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2845873c-ef7c-4532-9b37-80b659e0ef9a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T134045Z&X-Amz-Expires=86400&X-Amz-Signature=1b2237a3c5523035c0631d288c7b61eabad46608991379551e10ae19d0240b42&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
                        
            - 2-3. Resolution (분석)
                - 클래스가 참조하는 객체의 실제 메모리 주소값을 대입하는 단계
                - Symbolic Reference 값을 Method Area 의 Direct Reference 값으로 변환
                    
                    > 런타임 상수풀(run-time constant pool)에 있는 
                    심볼릭 참조(symbolic reference)를
                    직접참조(direct reference)로 대체하는 과정입니다.
                    > 
                - 해당 단계에서 JVM 구현에 따라 클래스를 검증할 때
                - 해당 단계는 JVM의 구현에 따라 선택적으로 진행 될 수 있다.
                    - 한번에 해석할 수도 있고 (eager resolution)
                    당장 심볼릭 참조를 직접 참조로 바꿀 필요가 없다면 
                    뒤로 밀려날 수도 있다.(lazy resolution)
        - 3. Initialization
            - 클래스 파일을 읽고 이를 이용해
                - static 변수 등을 초기화
                - 클래스와 인터페이스의 값들을 지정한 값으로 초기화
            - 멀티 쓰레드로 동작하기 때문에 동시성 고려
                
                > JVM은 다중 스레드이므로 클래스 또는 인터페이스의 초기화는 적절한 동기화와 함께 매우 신중하게 일어나야 다른 스레드가 동시에 동일한 클래스 또는 인터페이스를 초기화하려고 시도하는 것을 방지할 수 있습니다
                (즉, **스레드로부터 안전한** 상태로 만들기 )
                > 
    - 해당 과정이 끝났을때 
    JVM 에서 클래스 파일을 구동시킬 준비가 완료된다.

---

# 2. Runtime Data Area

- JVM 이 프로그램을 수행하기 위해 OS 로 부터 할당받는 메모리 영역
    
    > WAS의 성능에 문제가 발생했을때 대부분 이 영역들이 원인이 된다.
    (Memory Leak 혹은 GC)
    > 
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1c33fe49-ebfa-4ab3-af7f-b95755f2c889/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T134118Z&X-Amz-Expires=86400&X-Amz-Signature=8359b4867826c49773bdbaebbf7498b03d7122491e0516da3173e610858fbbfe&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    [https://www.programcreek.com/2013/04/jvm-run-time-data-areas/](https://www.programcreek.com/2013/04/jvm-run-time-data-areas/)
    
- 5가지 로 구분
    - 3가지 영역은 Thread 별로 생성되며 
    (JVM stack / PC Register / Native Method stack )
    - 2가지 영역은 모든 Thread 가 공유한다.
        
        ( Method Area / Heap)
        
- Method Area
    - JVM 에 하나만 존재, JVM 구동 시에 해당 영역이 생성되고 JVM 이 종료시에 해제
    - Class Loader가 적재한 클래스(또는 인터페이스)에 대한 메타데이터 정보가 저장된다
    - 인스턴스 생성을 위한 객체 구조, 생성자, 필드 등이 저장된다.
        
        인스턴스 생성에 필요한 정보도 존재하기 때문에 JVM 의 모든 Thread 들이 Method Area 를 공유 
        
    - JVM이 읽어 들인 
    각각의 클래스와 인터페이스에 대한 런타임 상수 풀(Runtime Constant Pool), 
    필드와 메서드 코드, Static 변수, 메서드의 바이트코드 등을 보관한다.
        - 참고할만한 글
            
            > *** **[Runtime constant pool](https://wellbell.tistory.com/161#Runtime%--constant%--pool)**
            Method area 내부에 존재하는 영역으로, 각 클래스와 인터페이스의 상수뿐만 아니라, 메서드와 필드에 대한 모든 레퍼런스까지 담고 있는 테이블이다. 즉, 상수 자료형을 저장하여 참조하고 중복을 막는 역할을 수행한다.
            [https://wellbell.tistory.com/161](https://wellbell.tistory.com/161)
            > 
            - [https://jithub.tistory.com/40](https://jithub.tistory.com/40)
            - [https://8iggy.tistory.com/229](https://8iggy.tistory.com/229)
            
- Heap
    - Java 로 구성된 인스턴스, 배열 등을 동적으로 저장
    - Garbage Collection 의 대상이 되는 영역
    - Heap 영역이 가진 데이터는 모든 Java Stack 영역에서 참조되어 Thread 간 공유 
    (동기화 문제 가능성)
    - Heap 영역이 모두 차게 되면 OutOfMemoryException 발생
- JVM Stack
    - Java 의 메소드가 호출될 때 사용되는 메모리 공간
    - Thread의 Method가 호출될 때 수행 정보(메소드 호출 주소, 매개 변수, 지역 변수,연산 스택)가 
    Frame 이라는 단위로 JVM stack에 저장된다.
    - Method 호출이 종료될 때 stack에서 제거된다.
- PC Register
    - Thread 별로 동시에 동작할 수 있도록 최근 실행중인 명령어 메모리 주소를 저장하는 공간
    - 주의 : CPU 내의 기억장치인 레지스터와는 다르게 동작한다.
        
        (Register Base 가 아닌 Stack Base 로 작동 )
        
        - 참고할만한 글
            - Register base 와 Stack base
                - [https://blog.naver.com/kbh3983/221292870568](https://blog.naver.com/kbh3983/221292870568)
- Native Method Stack
    - 시스템 자원을 사용하거나 Java 로 구성된 코드만 사용될 수 없는 경우,
    다른 프로그래밍 언어로 작성된 메소드를 호출 시 사용되는 영역

---

# 3. Execution Engine

- JVM 은 Method Area 의 바이트 코드를 
Execution Engine 에 제공하여 정의된 내용대로 바이트 코드를 실행시킨다.
- execution engine 은 바이트코드를 기계어로 변환시켜 명령어 단위로 읽어서 실행하는데 
두가지 방식을 혼합하여 사용한다.
- 구성 요소
    - Execution Engine 은 세가지 요소로 구성
        - Interpreter
        - JIT Compiler
        - Garbage Collection
        
- **Interpreter**
    - 참고 : 컴파일러와 인터프리터
        - [https://coding-factory.tistory.com/303](https://coding-factory.tistory.com/303)
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/05998ce7-f567-4b69-bb59-edffaf83a645/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T134150Z&X-Amz-Expires=86400&X-Amz-Signature=e86212d80de88cfc05f307904962851ab914e05bf22781f62f397328e28f7b70&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    [https://www.javatpoint.com/java-interpreter](https://www.javatpoint.com/java-interpreter)
    
    - 바이트 코드를 읽고 운영체제가 실행할 수 있도록 기계어로 번역하는 역할을 수행
    - 바이트 코드를 한줄씩 해석, 실행하는 방식
    - 이러한 방식으로 인하여 속도가 느림 + 중복된 코드여도 해석하여 성능이 저하
        
        > JVM 인터프리터는 런타임(runtime) 중에 바이트 코드를 한 라인씩 읽고 실행합니다. 
        여기에서 속도가 문제가 발생합니다. 
        바이트 코드 역시 기계어로 변환되어야 하기 때문에 C, C++ 처럼 미리 컴파일을 통해 기계어로 변경되는 언어에 비해 속도가 느려집니다. 
        반복문 같은 경우 컴파일 언어와 다르게 인터프리터는 코드 각 줄을 매번 읽고, 번역해야 합니다.
        [https://junhyunny.github.io/information/java/jvm-execution-engine/](https://junhyunny.github.io/information/java/jvm-execution-engine/)
        > 
    
- **JIT Compiler**
    - **Just-In-Time Compiler**
    - 프로그램을 실제 실행하는 시점에 기계어로 번역하는 컴파일러
    - 인터프리터의 속도 문제를 해결하기 위해 도입
    - 인터프리터 방식으로 진행하다가 
    코드 전체에서 반복되어 호출되는 메소드는 JIT 컴파일러가 기계어로 변환(컴파일)하여 캐싱한다.
    - 이후 인터프리터 방식으로 번역을 진행하다가 중복된 부분을 만나면 캐싱된 기계어 코드를 재사용
    - 나중에 동일한 부분이 호출된다면 캐싱해둔 코드를 사용하므로 실행 속도 향상
    - 선행 작업들로 인해 초기 실행속도는 다소 느릴 수 있으나 기계어로 반복변환작업이 줄어 일반적으로 빠른 속도 결과를 보인다.
    - 모든 코드를 JIT 컴파일러 방식으로 실행하지 않고, 
    인터프리터 방식을 사용하다가 일정 사용 기준을 넘어서면 JIT 컴파일러 방식으로 실행
    
    - 동작과정
        - 모든 코드를 JIT 컴파일러 방식으로 실행하지 않고, 인터프리터 방식을 사용
            - 한번만 수행되는 메서드들은 인터프리터 방식이 더 빠르기 때문
        - JVM 은 호출되는 메서드 각각에 대해 호출마다 호출 횟수를 누적
        - 호출 횟수가 특정치를 초과할 때(컴파일 임계치를 넘어설 떄) JIT 컴파일러 방식으로 실행
        - *** 컴파일 임계치
            - 다음 두 값의 합
            - method entry counter (JVM 내에 있는 메서드가 호출된 횟수 )
            - back-edge loop counter (메서드가 루프를 빠져나오기까지 회전한 횟수)
        - 컴파일 임계치를 확인하고 메서드가 컴파일 될 자격이 있는지 결정
        - 자격이 있다면 메서드는 컴파일되기 위해 큐에서 대기
        - 이후 컴파일 쓰레드에 의해 컴파일 진행
        
        > [https://hyeinisfree.tistory.com/26](https://hyeinisfree.tistory.com/26)
        아주 오랫동안 돌아가는 루프 문의 카운터가 임계치를 넘어가면 해당 루프는 컴파일 대상이 된다. 
        JVM은 루프를 위한 코드의 컴파일이 끝나면 루프가 다시 반복될 때는 코드를 컴파일된 코드로 교체하고 더 빠르게 실행된다. 
        이 교체 과정을 "스택 상의 교체(on-stack replacement, ORS)"라고 부른다.
        > 
    
    - 종류
        - [https://nopainnocode.tistory.com/15](https://nopainnocode.tistory.com/15)
        - JIT 컴파일러는 두 가지 형태로 나뉜다.
        - 두 컴파일러의 차이는 컴파일 있어서의 적극성이다.
            - 1. 클라이언트 컴파일러 : 컴파일하는 시기가 빠르다.
            - 2. 서버 컴파일러 : 컴파일하는 시기가 느리다.
            - 3. 티어드 컴파일 : 두 가지 컴파일러를 모두 사용.

---

# 4. Garbage Collection

- 자바의 메모리 관리 방법 중의 하나로 
JVM Heap 영역에서 동적으로 할당했던 메모리 영역 중 필요없게 된 메모리 영역을 주기적으로 삭제하는 프로세스
- Java 의 Heap 영역에서 참조되고 있지 않는 객체들의 메모리를 할당, 해제하는 과정
- 장점
    - 개발자가 메모리관리를 직접 해주지 않아도 되므로 개발에 온전히 집중할 수 있다.
- 단점
    - 개발자가 메모리가 언제 해제되는지 정확하게 알 수 없다.
    - 가비지컬렉션이 동작하는 동안에는 다른 동작을 멈추기 때문에 오버헤드가 발생한다.
- 명시적으로 불필요한 데이터는 null 로 선언
- System.gc() 메소드로 GC 를 할 수 있으나 프로그램의 성능에 큰 영향을 미침
- GC 과정에서 중요한 개념은 Reachability, Stop-the-world
- 영역에 따라 Minor GC, Major GC 로 나뉨
- 동작
    - **heap 영역**
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/59e55f51-311f-4add-af05-45d537e97aab/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221031%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221031T134217Z&X-Amz-Expires=86400&X-Amz-Signature=2d5ad54286dd7e7e3b2fe0f1f9d5afc28b8d2b397c14ddb587a01b48f885e20a&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
        
        [https://www.waitingforcode.com/off-heap/on-heap-off-heap-storage/read](https://www.waitingforcode.com/off-heap/on-heap-off-heap-storage/read)
        
        - JVM 의 가비지컬렉터는 처음 설계될 때 Week Generational Hypothesis 를 전제로 설계
            - 대부분의 객체는 금방 접근 불가능한 상태가 된다.
            - 오래된 객체에서 새로운 객체로의 참조는 아주 드물게 존재한다.
        - 즉 객체는 대부분 일회성이며, 메모리에 오랫동안 남아있는 경우는 드물다.
        - 따라서 객체의 생존기간에 따라 물리적은 Heap 영역을 나누었다.
            - Young generation
                - Young generation 영역은 다시 Eden, 두군데의 Survivor 영역으로 나누어 관리한다.
                - 새롭게 생성된 객체가 할당(Allocation)되는 영역 (대부분 Eden 영역 이후 survivor 로 이동 )
                - 대부분의 객체가 금방 Unreachable 상태가 되기 때문에 많은 객체가 Young 영역에 생성되었다 사라진다.
                - Young 영역에 대한 가비지 컬렉션을 Minor GC 라고 한다.
                - Minor GC 는 상대적으로 빈번하게 발생하지만 짧게 끝난다.
                - 가비지컬렉션의 동작이 Old Generation 까지 스캔해서 가비지를 찾지 않도록 해서 더욱짧은 Stop-the-world 시간 안에 메모리를 회수 할 수 있도록 했다.
            - Old generation
                - Young영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
                - Young 영역보다 크게 할당되며 영역의 크기가 큰 만큼 가비지는 적게 발생한다.
                    - Old 영역이 Young 영역보다 크게 할당되는 이유는 Young 영역의 수명이 짧은 객체들은 큰 공간을 필요로 하지 않으며 
                    큰 객체들은 Young 영역이 아니라 바로 Old 영역에 할당되기 때문이다.
                - Old 영역에 대한 가비지 컬렉션을 Major GC 또는 Full GC 라고 한다.
                - Old generation 영역에 있는 개체가 Young generation 영역의 객체를 참조한다면 카드테이블에 참조여부를 기록
                    
                    (Old 영역의 card table 이 존재)
                    
                    - Minor GC 를 수행할 때 Old Generation 객체 전체를 스캔하는 대신 카드 테이블에 있는 참조 정보들만 확인해서 
                    Young generation 으로의 참조가 있는 Old Generation 영역만 스캔해서 가비지 여부를 판별
                    - Old Generation 에서 Young Generation 으로의 참조가 발생하면 Write Barrier 를 이용해 Card Table 에서 해당 영역에 참조가 있었다고 표시한다.
                    - 카드테이블
                        - [https://intrepidgeeks.com/tutorial/jvm-card-table](https://intrepidgeeks.com/tutorial/jvm-card-table)
                - ~~Perm~~
                    - Java8 부터 제가됨
    - **stop-the-world**
        - GC 를 실행하기 위해 JVM 이 애플리케이션 실행을 멈추는 것
        - stop-the-world 가 발생하면 GC 를 실행하는 쓰레드를 제외한 
        나머지 쓰레드는 모두 작업을 멈춘다.
        - GC 작업을 완료한 이후에 중단했던 작업을 다시 시작한다.
        - stop-the-world 시간을 줄이는것이 GC 튜닝
        - 어떤 GC 알고리즘을 사용해도 stop-the-world 는 발생한다.
    - **Reachability**
        - GC 에서 객체가 Garbage 인지 판별하는 개념
        - 유효한 참조의 최초 셋을 Root set 이라고 함
        - Heap 영역 내부의 객체들은 Method Area, java stack, Natice Stack 에서 참조되면 reachable 로 판정
    - **GC 알고리즘**
        - GC 기본알고리즘
        - 발생 시점에 따른 GC
        - 여러가지 GC 방식

---

- 참고
    - Garbage Collection
        - [https://mangkyu.tistory.com/118](https://mangkyu.tistory.com/118)
        - [https://hbase.tistory.com/209](https://hbase.tistory.com/209)
    - runtime data area
        - [https://jithub.tistory.com/40](https://jithub.tistory.com/40)
        - [https://tecoble.techcourse.co.kr/post/2021-08-09-jvm-memory/](https://tecoble.techcourse.co.kr/post/2021-08-09-jvm-memory/)
    - excution engine
        - [https://junhyunny.github.io/information/java/jvm-execution-engine/](https://junhyunny.github.io/information/java/jvm-execution-engine/)
    - class loader
        - [https://medium.com/platform-engineer/understanding-jvm-architecture-22c0ddf09722](https://medium.com/platform-engineer/understanding-jvm-architecture-22c0ddf09722)
        - [https://wonit.tistory.com/590](https://wonit.tistory.com/590)
        - [https://tecoble.techcourse.co.kr/post/2021-07-15-jvm-classloader/](https://tecoble.techcourse.co.kr/post/2021-07-15-jvm-classloader/)
        - [https://coding-factory.tistory.com/828](https://coding-factory.tistory.com/828)
        - [https://connie.tistory.com/10](https://connie.tistory.com/10)
        - [https://keichee.tistory.com/105](https://keichee.tistory.com/105)
        - [https://blog.hexabrain.net/397](https://blog.hexabrain.net/397)
    - JIT 컴파일러
        - [https://hyeinisfree.tistory.com/26](https://hyeinisfree.tistory.com/26)
        - [https://dkswnkk.tistory.com/416](https://dkswnkk.tistory.com/416)
        - [https://coding-factory.tistory.com/827](https://coding-factory.tistory.com/827)
        - [https://beststar-1.tistory.com/3#JIT_컴파일러](https://beststar-1.tistory.com/3#JIT_%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC)
        - [https://nopainnocode.tistory.com/15](https://nopainnocode.tistory.com/15)
