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
InputStream is = new FileInputStream("C:/test.jpg);
int readByte;
while ((readByte=is.read()) != -1) {...}
```
### read(byte[] b) 메소드
- 입력 스트림으로부터 매개값으로 주어진 바이트 배열의 길이만큼 바이트를 읽고 배열에 저장한다. 그리고 읽은 바이트 수를 리턴한다.
- 실제로 읽은 바이트 수가 배열의 길이보다 작을경우 읽은 수만큼만 리턴한다.
- ex) 입력 스트림에서 5개의 바이트가 들어온다면 아래와 같이 길이 3인 바이트 배열로 두번 읽을 수 있다.
![image](https://user-images.githubusercontent.com/77083074/203729265-1adc5220-598d-454d-8e43-8315f25d70d5.png)
- read() 메소드 처럼 마지막 바이트까지 루프를 돌며 읽을 수 있다.
```java
InputStream is = new FileInputStream("C:/test.jpg);
int readByteNo;
byte[] readBytes = new byte[100];
while ((readByteNo=is.read(readBytes)) != -1) {...}
```
- read() 메소드는 100번을 루핑해서 읽어들여야하는 반면 read(byte[] b) 메소드는 한번 읽을 때 매개값으로 주어진 바이트 배열 길이만큼 읽기 때문에 루핑 횟수가 현저히 줄어든다. => 많은 양의 바이트를 읽을 때는 read(byte[] b) 메소드가 유용.

### read(byte[] b, int off, int len) 메소드
- 입력 스트림으로부터 len개의 바이트만큼 읽고, 매개값으로 주어진 바이트 배열 b[off]부터 len개 까지 저장한다. 그리고 읽은 바이트 수인 len개를 리턴한다.(마찬가지로 읽은수만큼)
- ex) 입력 스트림에서 전체 5개의 바이트가 들어오고, 여기서 3개만 읽어 b[2], b[3], b[4]에 각각 저장한다면 아래와 같이 할 수 있다.
![image](https://user-images.githubusercontent.com/77083074/203731134-24ce3334-a235-4151-a67f-12004f63406e.png)
- read(byte[] b) 와의 차이점은 한 번에 읽어들이는 바이트 수를 len 매개값으로 조절할 수 있고, 배열에서 저장이 시작되는 인덱스를 지정할 수 있다는 점이다.
  - 만약 off =0, len = 배열의 길이  --> read(byte[] b)와 동일하다.

### close() 메소드
- InputStream을 더 이상 사용하지 않을 경우 close() 메소드를 호출해서 InputStream에서 사용했던 시스템 자원을 풀어준다.


# **Byte와 Character 스트림**
스트림 클래스는 크게 두 종류로 구분된다. 
- 바이트(byte) 기반 스트림
  - 그림, 멀티미디어, 문자 등 모든 종류의 데이터를 받고 보낼 수 있다.
- 문자(Character) 기반 스트림
  - 오직 문자만 받고 보낼 수 있도록 특화되어 있다.
  


# **표준 스트림 (System.in, System.out, System.err)**

# **파일 읽고, 쓰기, 수정**
