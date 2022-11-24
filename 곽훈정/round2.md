**스트림은 단일 방향으로 연속적으로 흘러가는 것을 말하는데, 물이 높은 곳에서 낮은 곳으로 흐르듯이 데이터는 출발지에서 나와 도착지로 들어간다는 개념이다.

# **InputStream(입력 스트림)과 OutputStream(출력 스트림)**
- 프로그램이 데이터를 입력 받을 때에는 입력 스트림. 출발지는 키보드, 파일, 네트워크상의 프로그램이 될 수 있다.
- 출력 스트림의 도착지는 모니터, 파일, 네트워크상의 프로그램이 될 수 있다.
- **프로그램을 기준**으로 데이터가 들어오면 입력스트림이고, 데이터가 나가면 출력스트림이다.
  - 프로그램이 네트워크상의 다른 프로그램과 데이터 교환을 하기 위해서는 양쪽 모두 입력 스트림과 출력 스트림이 각각 필요하다. (단방향이라는 특성 때문) 
- 자바의 기본적인 입출력(IO:Input/Output) API 는 java.io 패키지에서 제공하고 있다.

|java.io 패키지의 주요 클래스|설명|
|:-------------------------|:---|
|File|파일 시스템의 파일 정보를 얻기 위한 클래스|
|Console|콘솔로부터 문자를 입출력하기 위한 클래스|
|InputStream / OutputStream|바이트 단위 입출력을 위한 최상위 입출력 스트림 클래스|
FileInputStream / FileOutputStream  DataInputStream / DataOutputStrema  ObejctInputStrema / ObjectOutputStream  PrintStream  BufferedInputStream / BufferedOutputStream| 바이트 단위 입출력을 위한 하위 스트림 클래스|
|Reader / Writer | 문자 단위 입출력을 위한 최상위 스트림 클래스|
FileReade / FileWriter  InputStreamReader / OutputStreamWriter  PrintWriter  BufferdReader / BufferedWriter| 문자 단위 입출력을 위한 하위 스트림 클래스|

# **Byte와 Character 스트림**

# **표준 스트림 (System.in, System.out, System.err)**

# **파일 읽고, 쓰기, 수정**
