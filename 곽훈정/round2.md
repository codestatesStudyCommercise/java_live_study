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

---
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

---
## **OutputStrema**
- 바이트 기반 출력 스트림의 최상위 클래스로 추상 클래스이다.
- 모든 바이트 기반 출력 스트림 클래스는 이 클래스를 상속받아서 만들어진다.
![image](https://user-images.githubusercontent.com/77083074/203741744-a4863c3a-1276-44da-be3f-a74ed6350487.png)

### write(int b)메소드
- 매개 변수로 주어진 int 값에서 끝에 있는 1바이트만 출력 스트림으로 보낸다.
- 매개 변수가 int 타입이므로 4바이트 모두를 보내는 것으로 오해할 수 있다.
![image](https://user-images.githubusercontent.com/77083074/203743210-00825f0b-f796-4401-98e6-e7a2293e58e4.png)
```java
OutputStream os = new FileOutputStream(":/test.txt");
byte[] data = "ABC".getBytes();
for(int i=0; i<data.length; i++) {
  os.write(data[i]); // "A", "B", "C" 를 하나씩 풀력
  }
```
### write(byte[] b) 메소드
- 매개값으로 주어진 바이트 배열의 모든 바이트를 출력 스트림으로 보낸다.
![image](https://user-images.githubusercontent.com/77083074/203743761-a9aafdd3-9287-4260-9fc9-61b0cede3916.png)
```java
OutputStream os = new FileOutputStream("C:/test.txt");
byte[] data = "ABC".getBytes();
os.write(data); //"ABC" 모두 출력
```

### write(byte[] b, int off, int len) 메소드
- b[off] 부터 len 개의 바이트를 출력 스트림으로 보낸다.
![image](https://user-images.githubusercontent.com/77083074/203744063-d37c6c00-4af4-45ba-a397-3ebe4fb2b1db.png)
```java
OutputStream os = new FileOutputStream("C:/test.txt");
byte[] data = "ABC".getBytes();
os.write(data, 1, 2); // "BC" 만 출력
```

### flush()와 close() 메소드
- 출력 스트림은 내부에 작은 버퍼(buffer)가 있어서 데이터가 출력되기 전에 버퍼에 쌓여있다가 순서대로 출력된다.
- flush() 메소드는 버퍼에 잔류하고 있는 데이터를 모두 출력시키고 버퍼를 비우는 역할을 한다.
- 프로그램에서 더 이상 출력할 데이터가 없다면 flush() 메소드를 마지막으로 호출하여 버퍼에 잔류하는 모든 데이터가 출력되도록 해야 한다.
- OutputStream을 더 이상 사용하지 않을 경우 close() 메소드를 호출해서 OutputStream에서 사용했던 시스템 자원을 풀어준다.
```java
OutputStream os = new FileOutputStream("C:/test.txt");
byte[] data = "ABC".getBytes();
os.write(data);
os.flush();
os.close();
```


# **Byte와 Character 스트림**
스트림 클래스는 크게 두 종류로 구분된다. 
- 바이트(byte) 기반 스트림
  - 최상위 클래스 : InputStrema / OutputStream
  - 하위 클래스 : XXXInputStrema / XXXOutputStream   ex)FileInputStream / FileOutputStream
  - 그림, 멀티미디어, 문자 등 모든 종류의 데이터를 받고 보낼 수 있다.
- 문자(Character) 기반 스트림
  - 최상위 클래스 : Reader / Writer
  - 하위 클래스 : XXXReader / XXXWriter   ex)FileReader / FileWriter
  - 오직 문자만 받고 보낼 수 있도록 특화되어 있다.
  


# **표준 스트림 (System.in, System.out, System.err)**
- 자바는 콘솔로부터 데이터를 입력 받을 때 System.in 을 사용하고, 콘솔에 데이터를 출력할 때 System.out을 사용한다. 에러를 출력할 때에는 System.err를 사용한다.

## System.in
- InputStream 타입의 필드이므로 InpustStream 변수로 참조가 가능하다.
- 키보드로부터 어떤 키가 입력되었는지 확인하려면 read() 메소드로 한 바이트를 읽으면 된다. 리턴된 int 값에는 십진수 아스키 코드가 들어 있다.
- InputStream의 read() 메소드는 1바이트만 읽기 때문에 1바이트의 아스키 코드로 표현되는 숫자, 영어, 특수문자는 프로그램에서 잘 읽을 수 있지만, 한글과 같이 2바이트를 필요로 하는 유니코드는 read() 메소드로 읽을 수 없다.
  - read(byte[] b) 또는 read(byte[] b, int off, int len) 메소로 전체 입력된 내용을 바이트 배열로 받고, 이배열을 이용해서 String 객체를 생성하면 된다.
```java
        InputStream is = System.in;
        byte[] datas = new byte[100];

        System.out.println("이름: ");
        int nameBytes = is.read(datas);
        String name = new String(datas, 0, nameBytes-2); //끝에 2바이트는 Enter키에 해당하는 캐리지리턴(13)과 라인피드(10) 이므로 문자열에서 제외

        System.out.println("하고 싶은 말: ");
        int commentBytes = is.read(datas);
        String comment = new String(datas, 0, commentBytes - 2);

        System.out.println("입력한 이름: " + name);
        System.out.println("입력한 하고 싶은말: " + comment);
```
        
        
## System.out
- out은 PrintStream 타입의 필드이다. PrintStream이 OutputStream의 하위 클래스이므로 out 필드를 OutputStream 타입으로 변환해서 사용할 수 있다.
  - OutputStream os = System.out;
- OutputStream의 write(int b) 메소드는 1바이트만 보낼 수 있다. 2바이트로 표현되는 한글은 출력할 수 없다.
  - 한글을 바이트 배열로 얻은 다음 write(byte[] b) 또는 write(byte[] b, int off, int len) 메소드로 콘솔에 출력하면 된다.
```java
        OutputStream os = System.out;

        for (byte b = 48; b < 58; b++) {
            os.write(b); //아스키코드 48~57까지 출력 >> 0~9까지
        }
        os.write(10); //라인피드(10) 개행

        for (byte b = 97; b < 123; b++) {
            os.write(b); //아스키 코드 97~122까지 출력 >> a~z까지
        }
        os.write(10);

        String hangul = "가나다라마바사아자차카타파하";
        byte[] hangulBytes = hangul.getBytes();
        os.write(hangulBytes);

        os.flush();
```
     
        
# **파일 읽고, 쓰기, 수정**

## File클래스
- C:/Temp 디렉토리의 file.txt.파일을 객체로 생성하기
```java
  File file = new File("C:/Temp/file.txt"); 
```
  - 디렉토리 구분자는 윈도우에서는 / 또는 \ , 유닉스나 리눅스에서는 / 를 사용한다. 만약 \를 디렉토리 구분자로 사용한다면 이스케이프 문자(\\)로 기술해야 한다.
- File 객체를 생성했다고 해서 파일이나 디렉토리가 생성되지 않는다. 생성자 매개값으로 주어진 경로가 유효하지 않더라도 컴파일 에러나 예외가 발생하지 않는다. File 객체를 통해 해당 경로에 실제로 파일이나 디렉토리가 있는지 확ㅇ니하려면 exists() 메소드를 호출할 수 있다.
```java
boolean isExist = file.exists();
```
|메소드|설명|
|:---|:---|
createNewFile()|새로운 파일을 생성
mkdir()|새로운 디렉토리를 생성
mkdirs()|경로상에 없는 모든 디렉토리를 생성
delete()|파일 또는 디렉토리 삭제
canExecute()|실행할 수 있는 파일인지 여부
canRead()|읽을 수 있는 파일인지 여부
canWrite()|수정 및 저장할 수 있는 파일인지 여부
getName()|파일의 이름을 리턴
getParent()|부모 디렉토리를 리턴
getParentFile()|부모 디렉토리를 File 객체로 생성 후 리턴
getPath()|전체 경로를 리턴
isDirectiory()|디렉토리인지 여부
isFile()|파일인지 여부
isHidden()|숨김 파일인지 여부
lastModified()|마지막 수정 날짜 및 시간을 리턴
length()|파일 크기를 리턴
list()|디렉토리에 포함된 파일 및 서브디렉토리 목록 전부를 String 배열로 리턴
list(FilenameFilter filter)|디렉토리에 포함된 파일 및 서브디렉토리 목록 중에 FilenameFilter에 맞는 것만 String 배열로 리턴
listFiles()|디렉토리에 포함된 파일 및 서브 디렉토리 목록 전부를 File배열로 리턴
listFiles(FilenameFilter filter)|디렉토리에 포함된 파일 및 서브디록토리 목록 중에 FilenameFilter에 맞는 것만 File 배열로 리턴

## FileInputStream
- 파일로부터 바이트 단위로 읽어들일 때 사용하는 바이트 기반 입력 스트림. 바이트 단위로 읽기 때문에 그림, 오디오, 비디오, 텍스트 파일 등 모든 종류의 파일을 읽을 수 있다.
- FileInputStream은 InputStream의 하위 클래스이기 때문에 사용 방법이 InputStream과 동일하다.
  - 한 바이트를 읽기 위해서 read() 메소드를 사용하거나 읽은 바이트를 byte 배열에 저장하기 위해 read(byte[] b) 또는 read(byte[] b, int off, int len) 메소드를 사용한다.
```java
public class FileInputStreamExample {
    public static void main(String[] args) {
        try {
            FileInputStream fis = new FileInputStream(
                    "C:\\Users\\HunJeong\\IdeaProjects\\study\\src\\stream\\FileInputStreamExample.java");
            int data;
            while ((data = fis.read()) != -1) {
                System.out.write(data);
            }
            fis.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}// 콘솔에 그대로 출력 됨
```

## FileOutputStream
- 바이트 단위로 데이터를 파일에 저장할 때 사용하는 바이트 기반 출력 스트림. 모든 종류의 데이터를 파일로 저장할 수 있다.
  - 주의사항 : 파일이 이미 존재할 경우 데이터를 출력하면 파일을 덮어쓰게 된다. 기존의 파일 내용 끝에 데이터를 추가할 경우 FileOutputStream 생성자의 두 번째 매개값을 true로 준다.
- write() 메소드를 호출한 이후에 flush() 메소드로 출력 버퍼에 잔류하는 데이터를 완전히 ㅜㅊㄹ력하도록 하고, close() 메소드를 호출해서 파일을 닫아준다.
```java
 public static void main(String[] args) throws Exception {
        String originalFileName =
                "C:\\Temp\\IMG_2294.JPG";

        String targetFileName ="C:/Temp/IU.jpg";

        FileInputStream fis = new FileInputStream(originalFileName);
        FileOutputStream fos = new FileOutputStream(targetFileName);

        int readByteNo;
        byte[] readBytes = new byte[100];

        while ((readByteNo = fis.read(readBytes)) != -1) {
            fos.write(readBytes, 0, readByteNo);
        }

        fos.flush();
        fos.close();
        fis.close();

        System.out.println("복사 완료");
        
    }
```

## FileWriter
- 텍스트 데이터를 파일에 저장할 때 사용하는 문자 기반 스트림. 텍스트가 아닌 것들은 저장 할 수 없다. FileWriter를 생성하면 지정된 파일이 이미 존재할 경우 그 파일을 덮어쓰게 되므로, 기존의 파일 내용 끝에 추가할 경우에는 FileWriter 생성자 두 번째 매개값으로 true를 주면 된다.
```java
   public static void main(String[] args) throws Exception {
        File file = new File("C:/Temp/file.txt");
        FileWriter fw = new FileWriter(file, true);
        fw.write("FileWriter는 한글로된" + "\r\n");
        fw.write("문자열을 바로 출력할 수 있다." + "\r\n");
        fw.flush();
        fw.close();
        System.out.println("파일에 저장 되었습니다.");
    }
```


