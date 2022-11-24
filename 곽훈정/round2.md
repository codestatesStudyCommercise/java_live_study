**스트림은 단일 방향으로 연속적으로 흘러가는 것을 말하는데, 물이 높은 곳에서 낮은 곳으로 흐르듯이 데이터는 출발지에서 나와 도착지로 들어간다는 개념이다.**

# **InputStream(입력 스트림)과 OutputStream(출력 스트림)**
- 프로그램이 데이터를 입력 받을 때에는 입력 스트림. 출발지는 키보드, 파일, 네트워크상의 프로그램이 될 수 있다.
- 출력 스트림의 도착지는 모니터, 파일, 네트워크상의 프로그램이 될 수 있다.
- **프로그램을 기준**으로 데이터가 들어오면 입력스트림이고, 데이터가 나가면 출력스트림이다.
  - 프로그램이 네트워크상의 다른 프로그램과 데이터 교환을 하기 위해서는 양쪽 모두 입력 스트림과 출력 스트림이 각각 필요하다. (단방향이라는 특성 때문) 
- 자바의 기본적인 입출력(IO:Input/Output) API 는 java.io 패키지에서 제공하고 있다.

|java.io 패키지의 주요 클래스|설명|
|:---|:---|
|File|파일 시스템의 파일 정보를 얻기 위한 클래스|
|Console|콘솔로부터 문자를 입출력하기 위한 클래스|
|InputStream / OutputStream|바이트 단위 입출력을 위한 최상위 입출력 스트림 클래스|
FileInputStream / FileOutputStream</br>    DataInputStream / DataOutputStrema</br>    ObejctInputStrema / ObjectOutputStream</br>    PrintStream</br>    BufferedInputStream / BufferedOutputStream| 바이트 단위 입출력을 위한 하위 스트림 클래스|
|Reader / Writer | 문자 단위 입출력을 위한 최상위 스트림 클래스|
FileReade / FileWriter</br>  InputStreamReader / OutputStreamWriter</br>  PrintWriter</br>  BufferdReader / BufferedWriter| 문자 단위 입출력을 위한 하위 스트림 클래스|

## **InputStream**
- 바이트 기반 입력 스트림의 최상위 클래스로 추상 클래스이다.
- 모든 바이트 기반 입력 스트림은 이 클래스를 상속받아서 만들어진다.

![image](https://user-images.githubusercontent.com/77083074/203725929-4c7d1059-cf63-4591-b084-c51b6ae0f44f.png)

### read() 메소드
- 입력 스트림으로부터 1바이트를 읽고 4바이트 int 타입으로 리턴한다. 따라서 리턴된 4바이트 중 끝의 1바이트에만 데이터가 들어 있다. 
  - ex) 입력 스트림에서 5개의 바이트가 들어온다면 아래 그림과 같이 read() 메소드로 1바이트씩 5번 읽을 수 있다.
![image](https://user-images.githubusercontent.com/77083074/203727118-98d6c68e-7ae4-4298-b16d-1477dfcfe80a.png)
- 더 이상 읽을 수 없다면 -1 을 리턴하는데, 이것을 이용하여 읽을 수 있는 마지막 바이트까지 루프를 돌며 한 바이트씩 읽을 수 있다.
```java
InputStream is = new FileInputStream("C:test.jpg);
int readByte;
while ((readByte=is.read()) != -1) {...}
```



# **Byte와 Character 스트림**
스트림 클래스는 크게 두 종류로 구분된다. 
- 바이트(byte) 기반 스트림
  - 그림, 멀티미디어, 문자 등 모든 종류의 데이터를 받고 보낼 수 있다.
- 문자(Character) 기반 스트림
  - 오직 문자만 받고 보낼 수 있도록 특화되어 있다.
  


# **표준 스트림 (System.in, System.out, System.err)**

# **파일 읽고, 쓰기, 수정**
