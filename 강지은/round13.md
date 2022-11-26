

## 스트림 (Stream) / 버퍼 (Buffer) / 채널 (Channel) 기반의 I/O

## **✅**  I/O  input & output

![image](https://user-images.githubusercontent.com/48430781/204076998-dbf43da8-1a07-438f-8359-b193663f42ee.png)

- 자바의 I/O API는 모두 [java.io](http://java.io) 패키지에서 제공된다.

<br><br>

## **✅  스트림 (Stream)**

데이터를 운반하는데 사용되는 연결통로

자바에선 데이터를 전달하기 위해 두 대상을 연결하고 데이터를 전송하는게 필요한데 이 역할을 하는 것이 스트림(Stream)이다.

- Stream.of()하는 이 스트림과는 다른 스트림이다.

<br>

## **⏺**  스트림의 특징

스트림은 연속적인 데이터의 흐름을 물에 비유해 붙혀진 이름

>> 물과 유사한 특징을 갖고 있다. 

<br>

- **바이트 단위**의 데이터 전송

<br>

- **FIFO**

<br>

- **단방향통신**
    - 하나의 스트림으로 입출력이 동시에 처리될 수 없다.
    - 입출력을 동시에 처리하려면 inputStream, outputStream이 둘다 필요함.

![image](https://user-images.githubusercontent.com/48430781/204077009-25ba9828-1a4c-4a5a-994d-af98c11b4f71.png)

<br>

- **순차적 접근**
    - 먼저 보낸 데이터를 먼저 받는다.
    - 특정 위치의 데이터를 무작위로 Read/Write 원칙적으로 불가능

<br>

- **연속적으로 데이터를 주고 받는다.**
    - (모두 전송 될 때까지 쓰레드는 지연상태(블로킹) 유지)
    - **처리 속도가 떨어질 수 있다**는 (단점)
    - 이를 보완하기 위해 나온 것이 버퍼와 채널을 사용하는 NIO(New IO)
     
<br><br>

## **✅**  InputStream과 OutputStream

InputStream, OutputStream은 추상클래스

이 클래스를 상속받는 여러가지 입출력 클래스가 있다. 

<br>

![image](https://user-images.githubusercontent.com/48430781/204077015-2c9eddba-06b4-45ea-b5da-a810c1c8041f.png)
[https://stackoverflow.com/questions/46953036/inputstream-outputstream-for-standard-stream-java](https://stackoverflow.com/questions/46953036/inputstream-outputstream-for-standard-stream-java)

<br>

### ⏺ 종류

<br>

| 입력스트림 | 출력스트림 | 입출력 대상 종류 |
| --- | --- | --- |
| FileInputStream | FileOutputStream | 파일 |
| ByteArrayInputStream | ByteArrayOutputStream | 메모리 (byte배열) |
| PipeInputStream | PipeOutputStream | 프로세스간 통신 |
| AudioInputStream | AudioOutputStream | 오디오 장치 |

<br>

### **⏺ 메서드**

<br>

| InputStream | OutputStream |
| --- | --- |
| abstract int read() | abstract int write() |
| int read(byte[] b) | void write(byte[] b) |
| int read(byte[] b, int off, int len) | void write(byte[] b, int off, int len) |
- read()의 반환타입이 byte가 아닌 이유는 반환값의 범위가 0~255, -1 이기 때문
    - byte : 128 ~ 127
    - int :  2,147,483,648 ~ 2,147,483,647

<br><br>

## **✅**  Byte와 Character 스트림

스트림 클래스는 크게 두 종류로 나뉨

<br>

![image](https://user-images.githubusercontent.com/48430781/204077021-cf8db652-64a3-46ff-bb48-88ea1eea8053.png)
 
<br>

### **⏺** 바이트(byte)기반 스트림

- 모든 종류의 스트림을 받는다  -1byte
- 원시바이트를 그대로 주고받는다.

- InputStream, OutputStream이 최상위 추상클래스 
→  접미사로 사용
- 예를 들어 그림, 멀티미디어, 텍스트등의 
파일을 바이트단위로 읽을 때  FileInputStream , FileOutputStream 사용

<br>

### **⏺** 문자(character) 기반 스트림

문자단위로 입출력을 한다. -2byte

문자를 받고 보낼 수 있도록 **특화**되어 있음

→ 코딩테스트!!!

<br>

- Reader, Writer — 최상위 추상 클래스

<br>

![image](https://user-images.githubusercontent.com/48430781/204077028-f27dfb56-3eac-4f93-aeff-9422caf592d0.png)

<br>

- FileReader, BufferedReader, InputStreamReader
- FileWriter, BufferedWriter, PrintWriter, OutputStreamWriter

<br><br>

## **✅**  표준 스트림

자바에서 미리 정의한 표준 입출력 클래스

콘솔화면에 입출력됨 → 콘솔 입출력이라고 하기도 함.

<br>

java.lang.* 

- System.in : 표준 입력용 스트림
- System.out : 표준 출력용 스트림
- System.err : 표준 오류 출력 스트림

<br>

⏺왜 [System.in](http://System.in) 일까?  in은 무엇일까?

System 클래스에 존재한   InputStream 타입의 정적 필드!!! 

<br>

![image](https://user-images.githubusercontent.com/48430781/204077037-800073ca-ab1f-4fae-a34f-b1589fbd3c6f.png)

<br>

![image](https://user-images.githubusercontent.com/48430781/204077042-aef17a88-146e-4c57-8100-04a249162abf.png)

<br>

물론 InputStream inputstream = System.in을 사용해서 

inputstream.read()를 사용할 수도 있다. —>  (   내용보충필요   ) 

<br>

| 메서드 | 설명 |
| --- | --- |
| System.in.read() | 키보드로 입력된 값을 읽어들임, 더 이상 읽어들일 수 없으면 return -1  |
| System.out.write() | ( )안에 입력된 값을 화면(콘솔)에 출력
컴퓨터가 숫자로 저장된 것 → 사람이 읽을 수 있는 문자로 디코딩 후 출력 |
| System.out.flush() | 남아있는 데이터를 모두 출력시킴
→ 출력은 버퍼에 일정 용량 이상이 쌓여야 가능함 (입출력 성능 향상을 위해)  얘를 사용하면  버퍼를 비워서 바로 출력할 수 있다. |

<br><br>

## **✅  버퍼(Buffer)**

데이터를 전송할때 두 장치간 속도차이가 날수밖에 없을 텐데. 이 차이를 줄여주는 역할의 중간저장소 

<br>

![image](https://user-images.githubusercontent.com/48430781/204077051-4b4b2e6c-264d-4820-85ae-2808fc9e387d.png)

<br>

- I/O에서 버퍼는 보조스트림이다.
    
    단순히 보조만 하는, 파일을 직접 읽거나 쓸 수 없는 스트림
    
- 보조스트림은 파일에 접근할 수없으므로 스트림을 먼저 생성하고, 이를 이용해 보조 스트림을 생성해야한다.

<br>

우리가 코딩테스트에서 사용하는 입출력 방식도 해당 방식을 사용하면 빠른 입출력이 가능하다.

<br>

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
//버퍼(보조스트림)변수 =        보조스트림생성 (스트림생성(시스템 콘솔 입력))
```
<br>

Scanner 와는 무슨 차이가 있을까? 

```java
Scanner sc = new Scanner(System.in);
```

<br>

Scanner

- 기본적으로 공백을 delimiter로 삼는다
- 정규표현식 사용, 입력값 분할, 토큰화 파싱 과정(다른자료형으로 변환)  
→ 퍼포먼스 속도가 낮다.

<br>

![image](https://user-images.githubusercontent.com/48430781/204077063-7934f755-7500-4194-a15c-1e75775d97db.png)

<br>

![image](https://user-images.githubusercontent.com/48430781/204077068-25dc7cda-1298-42bc-8c5b-57d9809b2f86.png)

<br>

스캐너가 편하다고 생각할 수도 있지만, 그냥 스트림버퍼 쓰는걸 습관화하자!
<br>
InputStream 

![image](https://user-images.githubusercontent.com/48430781/204077073-431b90f0-9978-4001-bef3-8865842090bf.png)

![image](https://user-images.githubusercontent.com/48430781/204077077-7fb4aa37-68ac-470c-9ea9-b91b54f6a854.png)

<br><br>

## **✅**  파일 읽고 쓰기

<br>

가장 효율적인 방법

- FileReader + BufferedReader
- FileWriter + BufferedWriter

<br>

### **⏺ 왜 ((굳이)) 두가지를 함께 사용하는게 효율적일까?**

<br>

- BufferedReader와 FileReader는 작동방식에서 차이가 있다.
    - Reader는 입력 소스에서 문자를 읽고, BufferedReader는 문자 스트림에 버퍼를 추가해 버퍼에서 문자를 읽는다.
    - 일단 BufferedReader는 FileReader 보다 빠르고 효율적으로 작동
        - 버퍼 : 일정량의 데이터를 일시적으로 저장하는 데 사용되는 장치 메모리 저장소의 작은 부분
        - 일반적으로 버퍼는 장치의 RAM을 사용하여 임시 데이터를 저장해서 버퍼에서 데이터에 액세스하는 것이 하드 드라이브에서 동일한 양의 데이터에 액세스하는 것보다 훨씬 빠르다.

<br>

- BufferedReader를 이용하면, 버퍼 메모리를 사용하기 때문에
readline()메서드를 통해 한 번에 전체 라인을 읽을 수 있다.
또 FileReader처럼 매번 하드 드라이브에 액세스할 필요가 없어서 더 빠르다.

<br>

- 그러나 하드드라이브에 액세스 하는건 Reader만 됨.
- BufferedReader는 보조스트림이라  얘만 이용해서 파일을 읽을수는 없다 (하드 드라이브에 대해 액세스 권한이 없다)

<br>

- 만약 Reader로만 하드드라이브에 접근하면, 
    1)  **항상 한 문자씩 읽어들이는 특징**에 의해 
    2)  하드드라이브에 엄청나게 많이 접근해야함. (비효율)

<br>

- 그래서 좀더 효율적인 BufferedReader를 사용하되,  권한이 있는 Reader(FileReader)를 제공해 읽어들이는게 효율적이고 빠른것이다!

<br>


### ⏺  try-catch

<br>

파일 입출력 코드에선 **try-catch문**이 필요하다. 

1) 파일 경로명이 틀리면 FileNotFoundException

2) 읽기, 쓰기, 닫기 중 입출력 오류 발생시 read(), write(), close()메서드가 IOException예외 발생

<br>

### ⏺  close()는 반드시 하자.

아까 입출력 성능 향상을 위해 버퍼에 일정 용량 이상이 쌓여야 가능하다고 했다. 

그래서 바로바로 flush()되지 않는다. 

<br>

stream을 다 사용한 이후 close하지 않으면, 다음과 같은 문제가 생길수있다. 

- **InputStream** - open file이나 socket과 같은 OS resource들 차지
- **OutputStream -** close()를 해주지 않으면 file에 쓰려고 했던 data들이 stream에 남아있는 경우가 발생

<br>


---

<br>

### ⏺ FileWriter + BufferedWriter

<br>

```java
package inputOutput.practice;

import java.io.*;
import java.io.File;

public class Main {
    public static void main(String[] args) throws IOException {

        BufferedReader br= new BufferedReader(new InputStreamReader(System.in));

        File file = new File("11월24일_나의_하루.txt");
        if(!file.exists()){
            file.createNewFile();
        }

        FileWriter fw = new FileWriter(file); //얘만 써도 되긴 하지만 느려요!
        BufferedWriter bw = new BufferedWriter(fw); //이렇게 부착해줍니다 ㅎㅎ
				//BufferedWriter bw = new BufferedWriter(new FileWriter(file)); 
				
        String line;
        for (int i=0;i<10;i++) {
            line = br.readLine();
            bw.write(line); //"\r\n"을써야한다는데 개행이 안된다.. 귀찮다.. 내가 왜 그래야하지..? 써도안되잖아 그냥 newLine쓴다 휴
            bw.newLine();
        }

        bw.close();
        br.close();
        //?

    }
}
```

<br>

![image](https://user-images.githubusercontent.com/48430781/204077188-b7af9294-5626-411d-8d9f-09b31228e009.png)

<br>

### **⏺ InputStream, OutputStream :: 파일 복사 붙혀넣기**

```java
package inputOutput.practice;

import java.io.*;
import java.io.File;

public class Main {
    public static void main(String[] args) throws IOException {

				//출처 : 프로그래머스 자바 중급 강의
        //좋은예제!
        //끝난줄알았지? 인풋,아웃풋스트림도 쓰고 잘거다
        //인풋아웃풋은 읽고 쓰는게 역할이 확실하다는 걸 기억하자!
        

        FileInputStream fis = null;
        FileOutputStream fos = null;

        try{
            fis = new FileInputStream("11월24일_나의_하루.txt");
            fos = new FileOutputStream("copy.txt");
            
            int readData = -1; // 바이트형식으로 읽어내기 때문에 정수로 나온다
            while((readData = fis.read()) != -1){ // -1은 읽을 내용이 더 이상 없다는 의미
                fos.write(readData); // FileOutputStream의 write()함수를 이용해서 읽어온 내용을 copy.txt에 쓴다
            }
        }
        catch(Exception e){
            System.out.println(e);
        }
        finally{
            try{
                fis.close();
                fos.close();
            }
            catch(Exception e){
                System.out.println(e);
            }
        }
    }
}
```

![Screen Shot 2022-11-25 at 3.17.00 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c065ed0-7ea0-491f-bd62-00c8f54698f7/Screen_Shot_2022-11-25_at_3.17.00_AM.png)


<br><br>

## **✅  채널(Channel)**

스트림의 단점을 극복

- 양방향으로 접근이 가능하다
- 비동기적으로 닫고 중단 가능

![image](https://user-images.githubusercontent.com/48430781/204077207-2aaae065-803a-4684-9065-349e64414be1.png)

<br>


| 종류 | 설명 |
| --- | --- |
| FileChannel | 파일 입출력 채널 |
| Pipe.SinkChannel | 파이프에 데이터를 출력하는 채널 |
| Pipe.SourceChannel | 파이프로 부터 데이터를 입력받는 채널 |
| ServerSocketChannel | 클라이언트의 연결 요청을 처리하는 서버 소켓 채널 |
| SocketChannel | 소켓과 연결된 채널 |
| DatagramChannel | DatagramSocket과 연결된 채널 |

<br><br>

## **✅  NIO  ( New Input/Output )**

기존 I/O의 단점인 속도를 개선

채널 기반의 입출력 방식을 사용해 양방향 입출력이 가능하다.

| 구분 | IO | NIO |
| --- | --- | --- |
| 입출력 방식 | 스트림(Stream)방식 | 채널(Channel)방식 |
| 버퍼 방식 | 넌버퍼 | 버퍼 |
| 비동기 방식 | 지원 안 함 | 지원 |
| 블로킹/넌블로킹 방식 | 블로킹 방식만 지원 | 블로킹/넌 블로킹 모두 지원 |

<br>

![image](https://user-images.githubusercontent.com/48430781/204077237-3012cf43-7ffb-41cb-92a0-85ee8df2c142.png)

<br>

나중에 시간이 나면 더더더 추가하자.


<br>


---

 <br>

### References

[https://www.geeksforgeeks.org/difference-between-bufferedreader-and-filereader-in-java/](https://www.geeksforgeeks.org/difference-between-bufferedreader-and-filereader-in-java/)

[https://logical-code.tistory.com/147](https://logical-code.tistory.com/147)

[https://blog.naver.com/swoh1227/222244309304](https://blog.naver.com/swoh1227/222244309304)

[https://blog.naver.com/swoh1227/222237603565](https://blog.naver.com/swoh1227/222237603565)

[https://wookcode.tistory.com/25](https://wookcode.tistory.com/25)

나중에 다시 읽고 또 읽자

[https://st-lab.tistory.com/41](https://st-lab.tistory.com/41)

[https://blog.naver.com/swoh1227/222244309304](https://blog.naver.com/swoh1227/222244309304)
