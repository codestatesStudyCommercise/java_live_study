# 6주차 - 예외처리

<aside>
➡️ 작성일 : 2022.11.10

</aside>

---

# 프로그램 오류의 종류

- 에러가 발생하는 시점에 따라 분류
    1. 컴파일 에러 : 컴파일 시 발생하는 에러 
        - 주로 문법 오류로 부터 발생(Syntax Errors)
        - **“가장 좋은 에러는 컴파일 에러다"**
        - 상대적으로 발견이 쉽고 해결이 간단
    2. 런타임 에러 : 실행 시 발생하는 에러 
        - 프로그램이 실행되면서 JVM 에 의해 감지된다.
    3. 논리적 에러 : 실행은 되지만 의도와 다르게 동작하는 것
    
- 자바에서는 런타임 시 발생할 수 있는 프로그램 오류를 에러와 예외로 구분하였다.
    - 에러(Error)는 일단 발생하면 복구할수 없는 심각한 오류
        - OutOfMemoryError, StackOverflowError 등
    - 예외(Exception)는 발생하더라도 수습이 가능한 비교적 덜 심각한 오류
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c0723f85-3b89-47d8-a757-e4fc898257fd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221116%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221116T074050Z&X-Amz-Expires=86400&X-Amz-Signature=24e46b7b0f73a246c4e95381305035567f7365fe5566f4e56b056babf6948280&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    [https://simplesnippets.tech/exception-handling-in-java-part-1/](https://simplesnippets.tech/exception-handling-in-java-part-1/)
    

---

# Exception 클래스 (예외)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f09c78ce-6e3e-4b5b-a3af-972ccf6987fd/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221116%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221116T074107Z&X-Amz-Expires=86400&X-Amz-Signature=ad60a9cddb9a850501028a1610544c760d92c9cb2019bdc2d72b3e82bf45e97f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

[http://www.tcpschool.com/java/java_exception_class](http://www.tcpschool.com/java/java_exception_class)

- 자바에서 예외가 발생하면 예외 클래스로부터 객체를 생성하여 해당 인스턴스를 통해 예외처리를 수행한다.
- 예외클래스는 두 그룹으로 나뉘어진다.
    - Exception 클래스와 그 자손들 → Exception 클래스들이라고 부름
    - RuntimeException 클래스와 그 자손들 → RuntimeException 클래스들이라고 부름
- Exception 클래스들
    - 주로 외부의 영향으로 발생할 수 있는 것들
    - 사용자의 실수와 같은 외적인 요인에 의해 발생하는 예외
        - 존재하지않는 파일 이름 입력
        - 입력 실수
        - 잘못된 데이터 형식 입력
    - checked exception 이라고도 한다.
        - 컴파일러가 코드 실행 전에 예외 처리 코드 여부를 검사하기 때문
        - 해당 예외들을 발생시킬수 있는 코드들을 예외처리를 해주지 않을 경우 컴파일시 에러가 발생한다.
- RuntimeException 클래스들
    - 프로그래머의 실수로 발생하는 예외
        - 배열 범위 초과
        - null인 참조변수 호출
        - 클래스간 잘못된 형변환
        - 정수 나누기 0 시도
    - unchecked exception 이라고도 한다.
        - 컴파일러가 코드 실행 전에 예외 처리 코드 여부를 검사하지않기 때문
        - 해당 예외들은 컴파일러가 검사하지 않으므로 예외처리를 해주지 않는 상황이어도 컴파일이 정상 수행된다. (예외처리를 강제하지 않는다.)
            - RuntimeException 에 대해 예외처리가 강제된다면 예외처리 구문이 지나치게 많아지기때문

---

# 예외처리

- 프로그램 실행 시 발생할 수 있는 예기치 못한 예외의 발생에 대비한 코드를 작성하는 것
- 목적
    - 예외발생으로 인해 실행중인 프로그램의 갑작스런 비정상 종료를 막는것
    - 정상적인 실행상태를 유지할 수 있도록하는것
- 발생한 예외를 처리하지 못하면 프로그램은 비정상 종료되며
- 처리하지 못한 예외(uncaught exception)는 JVM의 예외처리기(UncaughtExceptionHandler) 가 받아서 예외의 원인을 화면에 출력한다.

## 방법 1. try - catch - finally

```java
try {
    // 예외가 발생할 가능성이 있는 코드를 삽입
} 
catch (ExceptionType1 e1) {
    // ExceptionType1 유형의 예외 발생 시 실행할 코드
} 
catch (ExceptionType2 e2) {
    // ExceptionType2 유형의 예외 발생 시 실행할 코드
} 
finally {
    // finally 블럭은 옵셔널
    // 예외 발생 여부와 상관없이 항상 실행
}
```

- try  블럭 실행
- catch 블럭은 try  블럭에서 발생한 예외에 따른 catch 블럭 실행
    - 처리하고자 하는 Exception 종류를 작성하면 내부적으로 instanceOf 를 통해 검사
    - 여러 catch 블럭을 작성 가능
        - 이경우 예외 발생시 catch 블럭에 작성된 Exception 종류 중 일치하는 catch 문 블럭만 실행되고 예외처리 코드가 종료되거나 finally 블럭으로 넘어간다.
        - catch 블럭은 위에서부터 순차적으로 검사를 진행하므로 상위 예외를 검사하는 로직이 하위 예외를 검사하는 로직보다 위에 있는 경우 컴파일 에러 발생
    - 발생한 예외와 catch 블럭에 작성된 Exception 이 일치하는 블럭을 찾지 못한다면 
    catch 블럭은 실행되지 않으며 예외는 처리되지 못한다.
- finally 블럭은  옵션, 포함하여 작성하였다면 예외 발생 여부에 관계없이 항상 실행
    - try 블럭에 return 문이 있는경우에도 finally 블럭이 먼저 실행된 후 return 이 수행된다.
- 주의
    - catch 블럭 내에 또다른 try-catch 블럭이 포함된 경우 같은 이름의 참조변수(모두 Exception e 를 사용하는 경우)를 사용해서는 안된다.

## 방법 2. 예외전가 - throws

```java
void method() throws Exception1, Exception2, ... ExceptionN {
		// 메서드 내용
}  

// ----------------------------------------------------

public static void main(String[] args) {
        try {
            someClass.method();
        } catch (Exception1 e) {
            System.out.println(e.getMessage());
        }
    }
```

- 특정 메서드 내에서 예외발생시 메서드를 호출한 메서드에게 예외를 전달하여 예외처리를 떠맡기는 것
- 메서드는 자신의 내부에서 발생할 수 있는 예외들을 throws 와 , 로 구분해 작성한다.
- 해당 메서드를 호출한 메서드는 throws 에 작성된 예외들을 보고 이에 대한 예외처리를 해주어야한다.
    - 해당 방식을 이용하여 발생할 수 있는 예외중 일부만 처리하여 
    메서드간의 예외처리를 분담하는 방식도 가능하다.
- 해당 방법은 일반적으로 RuntimeException 클래스들은 적지 않는다.
    - RuntimeException 들을 throws 를 통해 선언해준다고 해서 문제가 되진않는다.
    - 그러나 보통은 반드시 처리해주어야하는 예외들만 선언한다.
- 이 방식을 이용해 자신을 호출한 메서드에게 연속적으로 예외를 전달할 수 있으며 최종적으로 main 메서드에서도 예외가 처리되지 않으면 main 메서드가 종료되고 프로그램 전체가 종료된다.

---

# 예외 정보 확인

```java
try{
    throw new MyException("예외 발생 !!!!!!");
} catch (Exception e) {
    System.out.println( e.getMessage() );
    System.out.println( e.toString() );
    e.printStackTrace();
}
```

- `e.getMessage()`
    - 예외에 대한 기본적인 내용을 간단하게 출력해준다.
    - `예외 발생 !!!!!!`
- `e.toString()`
    - getMessage() 보다 더 자세한 예외 정보를 제공한다.
    - 발생한 예외가 어떤 예외에 해당하는지에 대한 정보
    - `ExceptionTest.ExceptionTest$MyException: 예외 발생 !!!!!!`
- `e.printStackTrace()`
    - 가장 자세한 예외 정보를 제공한다.
    - 어플리케이션 성능에 영향을 주고 다루기 어렵다는 이유로 
    성능을 중요시 한다면 비추천한다는 의견이 있음
        - System.err 로 출력된다.
    - `ExceptionTest.ExceptionTest$MyException: 예외 발생 !!!!!!
    at ExceptionTest.ExceptionTest.main(ExceptionTest.java:24)`

---

# 예외 발생시키기 - throw

```java
Exception e = new Exception("고의로 발생시키는 예외");

throw e; // 예외 발생

-------------------------------------------------------

throw new Exception("고의로 발생시키는 예외"); // 예외 발생
```

- `throw 예외인스턴스` 를 통해 의도적으로 예외를 발생 시킬 수 있다.

---

# 사용자 정의 예외 만들기

```java
class MyException extends RuntimeException {
        private final int ERROR_CODE;

        // 생성자를 통한 초기화
        MyException(String msg, int errCode) {
            super(msg);
            ERROR_CODE = errCode;
        }

        MyException(String msg) {
            this(msg, 100);
        }

        public int getERROR_CODE() {
            return ERROR_CODE;
        }
    }
```

- 프로그래머가 새로운 예외 클래스를 정의하여 사용 가능
    - 보통은 Exception 클래스 또는 RuntimeException 클래스로부터 상속받아 만든다.
    - 필요에 따라서 알맞은 예외 클래스 역시 선택 가능
    
    > 가능하면 새로운 예외 클래스를 만들기보다 기존의 예외 클래스를 활용하자
    > 
- 기존 예외클래스들은 Exception 클래스를 상속받아 checked exception 으로 작성하는 경우가 많았으나 Exception 클래스 는 checked exception 이므로 반드시 예외처리를 해주어야한다는 강제성으로 인해 코드가 지나치게 복잡해지므로 
예외처리를 강제하지 않는 unchecked exception 인 RuntimeException 을 통해 구현하는것이 추세이다.

---

# Exception Re-Throwing 예외 되던지기

- 하나의 예외에 대해 양쪽 모두에서 처리해줘야 할 작업이 있을때 사용한다.
    - 예외가 발생한 메서드
    - 이를 호출한 메서드
- 주의점 및 방법
    1. 예외가 발생할 메서드에서 try-catch 문을 통해 예외처리를 해줌과 동시에 
        - catch 문 안에서 다시 throw 를 통해 예외를 발생시켜야한다.
    2. 메서드 선언부에 throws 를 통해 발생할 예외를 지정해주어야한다. 
    
    ```java
    public static class ThrowExceptionTest{
    
        public void reThrowing() throws MyException{
            try {
                throw new MyException("첫번째 예외");
            } catch (MyException e) {
                System.out.println("첫번째 catch : e.getMessage() : " + e.getMessage());
                throw new MyException("두번째 예외"); // 예외 처리 후 다시 예외 발생 
            }
        }
    }
    
    public static void main(String[] args) {
    
        ThrowExceptionTest throwExceptionTest = new ThrowExceptionTest();
        try {
            throwExceptionTest.reThrowing(); // 예외 가능성 메서드 호출 
        } catch (MyException e) {
            System.out.println("두번째 catch : e.getMessage() : " + e.getMessage());
        }
    }
    ```
    

---

# Chained Exception 연결된 예외

- 하나의 예외가 다른 예외를 발생시킬수 있는 상황에서 사용
- initCause() 를 통한 예외의 원인인 예외를 등록
- 사용하는 경우
    1. 여러 예외를 하나의 큰 분류의 예외로 묶기 위해 다루기 위한 목적
    2. checked 예외를 unchecked 예외로 바꾸고 싶은 경우
    
    ## 전체 코드
    
    ```java
    // 설치 실패 예외
    static class InstallException extends RuntimeException {
        private final int ERROR_CODE;
    
        // 생성자를 통한 초기화
        InstallException(String msg, int errCode) {
            super(msg);
            ERROR_CODE = errCode;
        }
    
        InstallException(String msg) {
            this(msg, 100);
        }
    
        public int getERROR_CODE() {
            return ERROR_CODE;
        }
    }
    
    // 설치 공간 부족 예외
    static class NotEnoughSpaceException extends RuntimeException {
        private final int ERROR_CODE;
    
        // 생성자를 통한 초기화
        NotEnoughSpaceException(String msg, int errCode) {
            super(msg);
            ERROR_CODE = errCode;
        }
    
        NotEnoughSpaceException(String msg) {
            this(msg, 200);
        }
    
        public int getERROR_CODE() {
            return ERROR_CODE;
        }
    }
    
    // 설치작업 수행 메모리 부족 예외
    static class NotEnoughMemoryException extends RuntimeException {
        private final int ERROR_CODE;
    
        // 생성자를 통한 초기화
        NotEnoughMemoryException(String msg, int errCode) {
            super(msg);
            ERROR_CODE = errCode;
        }
    
        NotEnoughMemoryException(String msg) {
            this(msg, 300);
        }
    
        public int getERROR_CODE() {
            return ERROR_CODE;
        }
    }
    
    public static class ChainedExceptionTest{
    
        // 남은 설치 공간 확인
        private boolean checkRemainSpace(){
            return false;
        }
    
        // 남은 설치작업을 수행할 메모리 확인
        private boolean checkRemainMemory(){
            return false;
        }
    
        // 설치 시작
        private void startInstall() throws NotEnoughSpaceException, NotEnoughMemoryException{
            if (!checkRemainSpace()){
                throw new NotEnoughSpaceException("설치 공간 부족 !!!!");
            }
            if (!checkRemainMemory()){
                throw new NotEnoughMemoryException("설치작업을 수행할 메모리 부족 !!!!");
            }
        }
    
        // 파일 복사
        private void copyFiles(){};
    
        // 임시파일 삭제
        private void deleteTempFiles(){};
    
        // 설치과정 수행
        public void install() throws InstallException{
            try {
                startInstall(); // 예외 발생
                copyFiles();
            } catch (NotEnoughSpaceException se){
                InstallException ie = new InstallException("설치중 예외 발생");
                ie.initCause(se);
                throw ie;
            } catch (NotEnoughMemoryException me){
                InstallException ie = new InstallException("설치중 예외 발생");
                ie.initCause(me);
                throw ie;
            } finally {
                deleteTempFiles();
            }
        }
    }
    
    public static void main(String[] args) {
    
        // 테스트
        ChainedExceptionTest chainTest = new ChainedExceptionTest();
        try{
            chainTest.install();
        } catch (InstallException ie) {
            ie.printStackTrace();
        }
    }
    ```
    
    ## 결과
    
    ```java
    // 설치과정 수행
        public void install() throws InstallException{
            try {
                startInstall(); // 예외 발생
                copyFiles();
            } catch (NotEnoughSpaceException se){
                InstallException ie = new InstallException("설치중 예외 발생");
                ie.initCause(se);
                throw ie;
            } catch (NotEnoughMemoryException me){
                InstallException ie = new InstallException("설치중 예외 발생");
                ie.initCause(me);
                throw ie;
            } finally {
                deleteTempFiles();
            }
        }
    ```
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/16b681cb-c25a-48e7-92f3-51ae1a55ff35/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221116%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221116T074203Z&X-Amz-Expires=86400&X-Amz-Signature=af815ae4ecd7108bf3c32374a1a3ba505c7f69d5a867d54340f555deffa6a432&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    - `Throwable initCause(Throwable cause)`
        - 지정한 예외를 원인예외로 등록할 수 있다.
    - `Throwable getCause()`
        - 원인 예외를 반환한다.
    
    ---
    
    # try - with - resources
    
    - 사용한 후 반드시 사용한 자원을 반환해주어야하는 클래스들이 있다.
    - 주로 입출력(I/O) 관련 클래스들을 다룰때 유용하게 사용할 수 있다.
    
    ## finally 에서 예외가 발생한다면 ?
    
    - 기존의 try-catch-finally 구문에서는 finally 블럭 안에 자원을 반환하는 코드를 두어
    작업중 예외가 발생하더라도 자원이 반환되도록 구성하였다.
    - 이경우 finally 안에서 예외가 발생하면 ?
        
        ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/06e1c1af-fd68-47c3-824a-620aabf45089/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221116%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221116T074834Z&X-Amz-Expires=86400&X-Amz-Signature=ce3b838513ae6347744b72371a6c04d20ee30cdeae83a92d40b125426d1c9eff&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
        
        - DataInputStream 이 상속받고있는 상위클래스 FilterInputStream 의 close()
        - IOException 이 발생할 수 있다.
        - 이를 위해 finally 블럭 안에서도 예외처리를 해주어야한다.
        
        ```java
        FileInputStream fis;
        DataInputStream dis;
        try {
            fis = new FileInputStream("dataFile.dat");
            dis = new DataInputStream(fis);
            // 이하 생략
        } catch (IOException ie ){
            ie.printStackTrace();
        } finally {
            try {
                if (dis != null){
                    dis.close();
                }
            } catch (IOException ie){
                ie.printStackTrace();
            }
        }
        ```
        
        - **주의**
            - 이경우 코드가 복잡해지고 
            try 블럭과 finally 블럭 모두에서 예외가 발생하면 
            try 블럭의 예외가 무시된다.
        
        ## try - with - resources 사용
        
        ```java
        int score = 0;
        int sum = 0;
        
        // 괄호 안에 두문장 이상을 넣을 경우 세미콜론으로 구분
        try(FileInputStream fis = new FileInputStream("score.dat");
            DataInputStream dis = new DataInputStream(fis)) {
            // try 블럭 내 구문 수행
            while (true){
                score = dis.readInt();
                System.out.println(score);
                sum += score;
            }
        } catch (EOFException eof ){
            System.out.println("총 점수 합 : " + sum);
        } catch (IOException ie) {
            System.out.println("catch IOException");
            ie.printStackTrace();
        } finally {
            System.out.println("finally");
        }
        ```
        
        - try-with-resources 문의 괄호안에 객체를 생성하는 코드를 넣으면, 해당 객체는 따로 close()를 호출하지 않아도 try 블럭을 벗어나는 순간 자동으로 close() 가 호출된다.
            - 그 이후에서야 catch 블럭 또는 finally  블럭이 실행된다.
            - try 블럭 괄호 안에는 해당 괄호 안에서만 유효한 변수를 선언하는것도 가능하다.
        - 자동으로 cloase() 가 호출되기 위해선 닫아야하는 클래스가 
        AutoCloseable 인터페이스를 구현한것이어야한다.
            
            ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3ee3fa0e-2afb-4664-840e-241b6a465a87/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221116%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221116T074127Z&X-Amz-Expires=86400&X-Amz-Signature=431b3f946b4c0656b9faab51c4cfec0a9250d9329ea5a660b0ca9aaa9321af1c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
            
        - 적용
            
            ```java
            static class CloseableResource implements AutoCloseable {
            
                public void executeFirstException(boolean exception) throws FirstException{
                    System.out.println("executeException() 호출 !! 예외 throw 여부 : " + exception);
                    if (exception){
                        throw new FirstException("executeException() 에서 발생");
                    }
                }
            
                public void close() throws CloseException {
                    System.out.println("close() 호출 !!! 무조건 CloseException 발생 ");
                    throw new CloseException("close() 에서 발생");
                }
            
            }
            // 첫번째 예외
            static class FirstException extends Exception {
                    FirstException(String msg) {
                        super(msg);
                    }
            }
            // close() 호출시 발생하는 예외
            static class CloseException extends Exception {
                CloseException(String msg) {
                    super(msg);
                }
            }
            
            public static void main(String[] args) {
            	
                try (CloseableResource cr = new CloseableResource()) {
                    // 매개변수 boolean 값에 따라 예외 throw 여부 결정
                    cr.executeFirstException(true);
            
                } catch (FirstException fe) {
                    fe.printStackTrace();
                } catch (CloseException ce) {
                    ce.printStackTrace();
                }
                System.out.println();
                System.out.println("-".repeat(50));
                System.out.println();
            
            }
            ```
            
            - 첫번째 매서드executeFirstException()를 호출하고 매개변수 boolean 값에 따라 내부에서 예외를 호출한다.
            - 예외 발생 여부를 떠나 두 경우 모두 close() 를 자동으로 호출한다.
            - close() 는 내부에서 다른 예외를 발생시킨다.
            - executeFirstException(false) 지정 시
                
                ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/37dba977-b380-4359-b485-d33a6c92639d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221116%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221116T074929Z&X-Amz-Expires=86400&X-Amz-Signature=721e3c595a8c0daefc56713b9ffcf8bf45f6dff89901113a1df56dda3b321e25&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
                
                - executeFirstException() 내부에서 예외가 발생하지 않아 close() 내부의 예외만 발생한 경우
                - 일반적인 예외 발생 모습과 같다.
            - executeFirstException(true) 지정 시
                
                ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/af1b5b12-a771-43f8-83fa-dd25b94f0dc2/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221116%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221116T075512Z&X-Amz-Expires=86400&X-Amz-Signature=f30356d0a1b468710a94107e0b451405fa26360f0c1dc6f5bd15fc02916aad4d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
                
                - executeFirstException() 내부에서 예외가 발생한경우
                    - 예외가 발생하는곳은 해당 로직에서 2곳이다.
                        1. executeFirstException() 호출 시 executeFirstException() 메서드 내부 
                        2. 자동으로 호출되는 close() 내부 
                    - 하지만 두 예외가 동시에 발생할수는 없다.
                        - try-with-resources문에서는 실제 발생한 예외(try문 내부 로직에 의해 발생한 예외 )에 대한 내용을 출력하고 close() 에서 발생하는 예외는 억제된 예외(suppressed) 로 다룬다.
                            - 출력된 에러의 `Suppressed:` 머릿말 이후에 해당 정보가 출력된다.
                            - 억제된 예외에 대한 정보는 실제 발생한 예외에 저장된다.
                                
                                (위 예시에서는 FirstException에 CloseException 정보가 저장된다.) 
                                
                                - Throwable 에 정의된 메서드를 통해 억제된 예외를 다룰 수 있다.
                                    - `void addSuppressed(Throwable exception)` : 억제된 예외를 추가
                                    - `Throwable[] getSuppressed() :` 억제된 예외를 반환
                        - *** try-catch-finally 문이었다면 finally 에서 발생한 예외에 의해 try 블럭의 예외가 무시되는 결과를 가져온다.
                            - 먼저 발생한 예외가 무시되고 마지막으로 발생된 예외의 내용만 출력되는 꼴이다.
                    
                     
                    
    
    ---
    
    - 참고
        - 남궁성 - 자바의 정석