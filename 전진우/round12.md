# 12회차 - I / O

<aside>
➡️ 작성일 : 2022.11.23

</aside>

---

# I / O

- 입출력
- 컴퓨터 내부 또는 외부의 장치와 프로그램간의 데이터를 주고받는 것

---

# 스트림

- 입출력을 수행하기 위해 데이터를 전달하고자 할때 필요한 데이터를 운반하는데 사용되는 통로 개념
- 단방향 통신만 가능하다.
    - 이로 인해 하나의 스트림으로 입출력이 동시에 시행될 수 없다.
    - 각각 입력을 위한 스트림, 출력을 위한 스트림이 필요
- 스트림은 먼저 보낸 데이터를 먼저 받는다.
- 중간에 끊김없이 연속적으로 데이터를 주고받는다.
- 스트림을 사용해서 모든 작업을 마치고 난 후 close() 를 호출해 닫아주여야한다.
    - close() 를 호출하면 내부적으로 flush() 를 호출하여 스트림의 버퍼에 있는 모든 내용을 출력소스에 쓴뒤 닫는다.
        
        (flush() 는 버퍼가 있는 출력스트림의 경우에만 의마가 있음)
        
    - ByteArrayInputStream 과 같이 메모리를 사용하는 스트림, 표준 입출력스트림은 닫아주지 않아도 된다.
        
        (바이트배열의 경우 사용하는 자원이 메모리 밖에 ㅇ벗으므로 가비지컬렉터에 의해 자동으로 자원이 반환된다.)
        
    - 프로그램이 종료될 때 사용하고 닫지 않은 스트림을 JVM 이 자동으로 닫아주기는 한다.

---

# 스트림 분류

## **바이트 기반 스트림**

- 바이트 단위로 데이터를 전송 (바이트기반은 입출력 단위가 1 byte)
- InputStream / OutputStream
    - InputStream / OutputStream 는 바이트 기반 스트림의 조상
    
    ```java
    byte[] inSrc = {0,1,2,3,4,5,6,7,8,9};
    byte[] outSrc = null;
    byte[] temp = new byte[4];
    
    ByteArrayInputStream input = null;
    ByteArrayOutputStream output = null;
    
    input  = new ByteArrayInputStream(inSrc);
    output  = new ByteArrayOutputStream();
    
    try {
    	while(input.available() > 0) {
    		int len = input.read(temp); // 읽어온 데이터 갯수를 반환 
    		output.write(temp, 0, len); // 읽어온만큼 write 수행 
    	}
    } catch(IOException e) {
    	System.out.println("에러 발생");
    }
    
    outSrc = output.toByteArray(); 
    
    System.out.println("inSrc = " + Arrays.toString(inSrc));
    System.out.println("temp = " + Arrays.toString(temp));
    System.out.println("outSrc = " + Arrays.toString(outSrc));
    ```
    
    - 종류
        - ByteArrayInputStream / ByteArrayOutputStream
            - 입출력 대상 : 메모리 (byte 배열 )
        - FileInputStream / FileOutputStream
            - 입출력 대상 : 파일
        - PipedInputStream / PipedOutputStream
            - 쓰레드간 통신
            - 서로 다른 쓰레드에 존재하는 입력스트림과 출력스트림을 connect()를 통해 연결하여 쓰레드간의 입출력을 수행
        - AudioInputStream / AudioOutputStream
            - 입출력 대상 : 오디오장치
- **바이트 기반 보조 스트림**
    - 보조스트림자체적으로 입출력을 수행할 수 없음
    - 스트림을 먼저 생성한 후 이를 사용해서 보조 스트림을 생성함
    - 스트림의 기능을 향상시키거나 새로운 기능을 추가함
    - FilterInputStream / FilterOutputStream 는 
    InputStream/OutputStream 의 자손이면서 보조스트림의 조상
        
        (모든 보조스트림의 조상은 아님)
        
    - FilterInputStream / FilterOutputStream
        - **Buffered**InputStream / **Buffered**OutputStream
            - 스트림의 입출력 효율을 높이기 위해 버퍼를 사용하는 보조스트림
            - 버퍼(byte 배열)를 사용해서 한번에 여러 바이트를 입출력
            - 버퍼가 가득 차면 버퍼의 모든 내용을 출력소스에 출력하고, 버퍼를 비운뒤 다시 출력을 저장할 준비를 수행
                
                → 버퍼가 가득 찼을때 출력하므로 버퍼에 데이터가 남아있는 채로 프로그램이 종료될 수 있음 
                
                → 출력작업 후 close()(내부적으로 flush() 를 호출) 나 flush() 를 호출하여 버퍼에 있는 내용을 출력하도록 해야한다.
                
        - DataInputStream / DataOutputStream
            - 각 기본 자료형단위로 읽고 쓸수 있도록 하는 보조스트림
            - 각 기본 자료형 값을 16진수로 표현하여 저장
            - 여러 자료형으로 읽기, 쓰기를 진행할 수 있다.
                - 여러 자료형을 이용하여 쓰기를 수행한 경우 읽기 역시 쓰기에 사용된 순서대로 읽어와야 올바르게 읽어올 수 있다.
        - PushbackInputStream
        - SequenceInputStream
            - InputStream 을 직접 상속 받는다.
            - 어러 개의 입력 스트림을 연속적으로 연결해서 처리할 수 있도록 해주는 보조스트림
        - PrintStream
            - 데이터 스트림으로 다양한 형태로 출력 가능
            - 데이터를 적절한 문자로 출력하도록 문자 기반 스트림의 역할을 수행하는 보조 스트림
            - PrintWriter 가 더 다양한 언어의 문자를 처리하는데 적합
            - 표준 출력인 System.out , System. err  가 PrintStream 를 사용한다.
            - print(), println(), printf() 등 익숙한 메서드가 있다.
    
    ---
    

## 문자 기반 스트림

- 자바는 한문자를 의미하는 char 형이 2byte 이므로 
바이트 기반으로 문자를 처리하기에 어려워 문자기반의 스트림을 제공
- 문자 데이터를 다루는데 필요한 인코딩 정보 변환을 자동으로 처리해준다.
    - Reader : 특정 인코딩 → 유니코드
    - Writer : 유니코드 → 특정 인코딩
- 문자 데이터 입출력시 사용
- Reader / Writer
    - 종류
        - CharArrayReader / CharArrayWriter
            - 입출력 대상 : 메모리 (char 배열 )
        - FileReader / FileWriter
            - 입출력 대상 : 파일
        - PipedReader / PipedWriter
            - 쓰레드간 통신
            - 서로 다른 쓰레드에 존재하는 입력스트림과 출력스트림을 connect()를 통해 연결하여 쓰레드간의 입출력을 수행
        - StringReader / StringWriter
            - 입출력 대상 : 메모리 (String)
            - StringWriter 에 출력되는 데이터는 내부의 StringBuffer 에 저장
                - 메서드를 통해 버퍼에 저장된 데이터를 획득할 수 있다.
- **문자 기반 보조 스트림**
    - BufferedReader / BufferedWriter
        - 버퍼를 이용해 입출력의 효율을 높일 수 있도록 한 보조스트림
        - BufferedReader의 readLine() 을 통해 라인단위로 읽기 가능
        - BufferedWriter의 newLine() 을 통해 줄바꿈 가능
    - InputStreamReader / InputStreamWriter
        - 바이트 기반 스트림을 문자 기반 스트림으로 연결
        - 바이트 기반 스트림의 데이터를 지정된 인코딩의 문자 데이터로 변환하는 작업을 수행
    - FilterReader / FilterWriter
    - LineNumberReader
    - PrintWriter
    - PushbackReader

## RandomAccessFile

- 파일에 대한 입출력 모두를 수행할 수 있는 클래스
- InputStream 이나 OutputStream 으로부터 상속받지 않고 
DataInput 인터페이스와 DataOutput 인터페이스를 모두 구현
- 기본 자료형 단위로 데이터를 읽고 쓸 수있다.
- 내부적으로 파일 포인터를 사용
    - 입출력시 파일 포인터가 위치한 곳이 수행시작점이 된다.
    - 파일 포인터의 위치는 파일의 첫부분(0부터)이며 읽기나 쓰기 작업 수행시 해당 위치로 이동하게 된다.
    - 이를 이용해 파일을 순차적으로 읽기 쓰는것이 아닌 특정 위치 어디서나 읽기 쓰기가 가능하다.
    - 파일 포인터를 임의의 위치를 원하는 위치로 옮기고(seek()) 작업을 수행하면된다.
- 생성시 인자로 mode 를 입력받아 수행할 작업을 지정가능하다.
- 주의
    - 입력 작업 직후 바로 출력 작업 수행 시 
    입력작업이 수행되면서 옮겨진 파일 포인터를 원하는 위치로 옮기지 않고 작업하여
        
        출력이 제대로 이루어 지지않을 수 있음 
        
    

---

# 표준 스트림 (System.in, System.out, System.err)

- 표준입출력 → 콘솔을 통한 입출력
- 자바의 표준입출력
    - System.in
    - System.out
    - System.err
- 자바 어플리케이션 실행과 동시에 자동 생성
- 타입으로 InputStream / PrintStream 을 사용하나 
인스턴스로는 BufferedInputStream / BufferedOutputStream 을 사용
- 입력
    - 콘솔입력은 버퍼를 가지고 있어 한번에 버퍼 크기만큼 입력이 가능
    - 버퍼를 가지므로 backspace 키 등 편집이 가능하다.
    - System.in.read() 호출시 
    Enter 키나 입력의 끝을 알리는 키(윈도우 : Ctrl + z / 유닉스 : Ctrl + d)를 누르기 전까지 입력을 기다리는 상태가 된다. (블락킹 상태)
    - Enter 입력 완료 시 입력된 데이터를 읽기 시작하고 모두 읽으면 다시 입력 대기 상태가 된다.
    - 입력의 끝을 알리는 키 입력시 -1 반환
    - Enter 입력 은 ‘\r’ 과 ‘\n’ 이 입력된것으로 간주되므로 데이터를 따로 처리시 주의
        
        → BufferedReader 를 함께 사용하면 readLine() 을 통해 라인단위로 데이터 입력처리가 가능 
        
- 지정한 입출력 대상으로 표준 입출력 대상 변경 가능
    - setIn(InputStream in)
    - setOut(PrintStream out)
    - setErr(PrintStream err)

---

# 스트림 / 버퍼 / 채널 기반의 I/O

## I / O

- I/O 는 스트림 기반
- 스트림은 입력과 출력 스트림으로 구분되어있어 데이터를 입력, 출력하기 위해서는 각각 따로 생성해서 구성해주어야함
- 특징
    - Stream 방식
    - Non-Buffer 방식
    - 비동기 지원 안함
    - Blocking 방식 사용

## 채널기반의 I/O - NIO

- JDK 1.4 부터 기존에 느린속도의 IO를 개선하고자 NIO(New IO)가 추가되었다
- NIO 는 채널 기반
    - 스트림과 달리 하나의 채널이 양방향으로 입출력이 가능
- 특징
    - Channel 방식
    - Buffer 방식
    - 비동기 지원
    - Blocking, Non-Blocking 방식 모두 사용

## Stream ↔ Channel

- 스트림
    - 입출력을 위해 각각 따로 스트림을 구성해주어야함
    - 단방향
- 채널
    - 하나의 채널을 통해 입출력이 가능
    - 양방향

## Buffer ↔ Non-Buffer

- 속도 및 데이터 처리의 유연함의 차이가 있다.
- Non-Buffer
    - 상대적으로 느리다.
    - 스트림 기반의 Java IO는 스트림으로 부터 한번에 여러 바이트를 읽는다.
    - 데이터는 어디에도 캐시되어있지 않다.
    - 스트림 속 데이터 내에서이동할 수 없다.
    - 이를 해결하기 위해 I/O 에서 Buffer 를 지원하는 보조 스트림을 연결해서 사용하기도 한다.
- Buffer
    - 입력과 출력을 버퍼를 통해 수행
    - 이미 처리된 buffer 로부터 데이터를 읽는다.
    - 필요시 버퍼 내부에서 이동 가능

## Blocking ↔ Non-Blocking

- Blocking
    - 쓰레드간 입출력이 필요한 경우 쓰레드를 블록킹 하여 처리함
    - 입력스트림에서 read() 를 호출하면 쓰레드가 블록킹(대기상태) 되고 출력스트림의 write() 를 호출하면 데이터를 출력 전까지 쓰레드가 블록킹이 된다.
        - IO 쓰레드가 블록킹 되는것은 다른 작업을 할 수 없고 블로킹을 빠져나오기 위해 인터럽트 할 수도 없다.
- Non-Blocking
    - NIO 는 Blocking과  Non-Blocking 특징을 모두 가지고있어 NIO Blocking은 쓰레드를 인터럽트함으로써 빠져나올 수 있다.
    - NIO의 Non-Blocking은 입출력 작업 준비가 완료된 채널만 선택해서 작업 쓰레드가 처리하므로 작업 쓰레드가 블로킹되지 않는다.

## 선택 기준

- NIO 는 다수의 연결이나 파일들을 non-blocking 이나 비동기처리를 할 수 있어 많은 쓰레드 생성을 피하고 쓰레드를 효과적으로 재사용한다는 장점
    - 연결수가 많고 하나의 입출력 처리 작업이 오래 걸리지 않는  경우 사용
    - 쓰레드에서 입출력 처리가 오래 걸린다면 대기하는 작업의 수가 늘어나 장점 유실
- NIO 는 버퍼 할당 크기가 문제가 되고 모든 입출력 작업이 버퍼를 반드시 사용해야하므로 즉시 처리하는 I/O 보다 성능 저하가 있을 수 있음
    - 연결 클라이언트 수가 적고 전송되는 데이터가 대용량이면서 순차적으로 처리될 필요성이 있는 경우 I/O 로 구현하는것이 좋다.

---

# 실습 - stream 을 이용한 입출력

```java
String line = "";
ArrayList<String> list = new ArrayList<>();
StringBuilder sb = new StringBuilder();

try (InputStreamReader isr = new InputStreamReader(System.in);
     BufferedReader br = new BufferedReader(isr)) {

    System.out.println("사용중인 OS 인코딩 정보 : " + isr.getEncoding());

    do {
        System.out.print("문장을 입력하세요. 마치시려면 q 를 입력하세요 >>> ");
        line = br.readLine();
        if (!line.equals("q")) {
            list.add(line);
            System.out.println("입력 내용 : " + line);
        }
    }while (!line.equalsIgnoreCase("q"));

    for (String str : list) {
        sb.append("[");
        sb.append(str);
        sb.append("]");
    }
    System.out.println(sb);
    System.out.println("프로그램을 종료합니다.");

} catch (IOException e) {
    e.printStackTrace();
}
```

# 실습 - 파일 읽고 쓰기 수정

```java
public static void writeFileText(File file) {
  try (InputStreamReader isr = new InputStreamReader(System.in);
       BufferedReader br = new BufferedReader(isr);
       FileWriter output = new FileWriter(file, true);
       BufferedWriter bw = new BufferedWriter(output)) {

      System.out.println("[입력하는 메세지를 " + file.getName() +  " 파일에 저장합니다.]");
      System.out.print(">>> ");
      bw.newLine();
      bw.newLine();
      bw.write(br.readLine());

  }catch (IOException e) {
      e.printStackTrace();
  }
}

public static void readFileText(File file) {
  try (FileReader output = new FileReader(file);
       BufferedReader bw = new BufferedReader(output)) {

      String line;

      System.out.println("파일 내용 출력 : " + file.getName());
      while ((line = bw.readLine()) != null){
          System.out.println(line);
      }
  }catch (IOException e) {
      e.printStackTrace();
  }
}

public static void makeNewFile(File file) {
  System.out.println("새로운 파일을 생성합니다.");
  writeFileText(file);
}

public static void main(String[] args) {
  File dir = new File("/Users/username/someDirName");
  String targetName = "file_write_test.txt";
  File target = new File(dir, targetName);;

  if (dir.exists()){
      if (dir.isDirectory()){
          System.out.println("디렉터리 이름 : " + dir.getName());
          System.out.println();
          // 디렉토리의 포함 파일과 디렉토리 목록 반환
          File[] files = dir.listFiles();
          if (files != null && files.length != 0){
              boolean isTargetExist = false;
              for (File file : files) {
                  String fileName = file.getName();
                  if (fileName.equals(targetName)) {
                      isTargetExist = true;
                  }
                  System.out.println("\t" + fileName);
              }
              if (isTargetExist) {
                  writeFileText(target); // 파일 쓰기
                  System.out.println();
                  readFileText(target);
              } else {
                  makeNewFile(target); // 새로운 파일 생성 후 쓰기
                  System.out.println();
                  readFileText(target);
              }
          } else {
              System.out.println("디렉터리가 비었습니다.");
              makeNewFile(target); // 새로운 파일 생성 후 쓰기
              System.out.println();
              readFileText(target);
          }
      } else {
          System.out.println("파일 이름 : " + dir.getName());
      }
  } else {
      System.out.println("파일 또는 디렉터리가 존재하지 않습니다.");
  }
}
```

---

- 참고
    - 남궁성 - 자바의 정석
    - [https://adrian0220.tistory.com/144](https://adrian0220.tistory.com/144)
    - [https://brunch.co.kr/@myner/47](https://brunch.co.kr/@myner/47)
    - [https://jeong-pro.tistory.com/145](https://jeong-pro.tistory.com/145)
    - [https://velog.io/@jihoson94/BIO-vs-NIO](https://velog.io/@jihoson94/BIO-vs-NIO)