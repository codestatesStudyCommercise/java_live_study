
![](https://velog.velcdn.com/images/bokimy/post/ec9d29f5-f053-4b4c-b38f-fa6b0d4d58fe/image.jpeg)

## 🟡 체크 예외(checked Exception)
- 분홍색은 체크 예외이다. 
- RuntimeException을 상속하지 않는 예외들을 말하는데, 체크 예외가 발생할 수 있는 메소드를 사용할 경우, 복구가 가능한 예외들이기 때문에 반드시 예외를 처리하는 코드를 작성해야 한다. 
- catch문으로 예외를 잡거나, throws로 예외를 자신을 호출한 클래스로 던지는 방법으로 해결해야 하며, 해결하지 않으면 컴파일 시 체크 예외가 발생한다. 
- 체크 예외는 Java 컴파일러와 JVM이 규칙을 준수하는지 확인하기 때문에 Exception이 호출된다.
- 대표적인 Exception - IOException, SQLException

 

## 🟡 언체크 예외(unchecked Exception)
- 하늘색은 언체크 예외이다. 
- RuntimeException을 상속한 예외들을 말한다.
- 언체크 예외라고 불리는 이유는 명시적으로 예외처리를 강제하지 않기 때문이다. 
- 언체크 예외는 따로 catch문으로 예외를 잡거나, throws로 선언하지 않아도 된다. 프로그램에 오류가 있을 때 발생하도록 의도된 것이다.
- 대표적인 Exception - NullPointerException, IllegalArgumentException

### 👉🏻 IOException : 입출력 예외처리
- EOFException
	입력의 도중에 예상외의 파일의 종료, 또는 예상외의 스트림의 종료가 있던 것을 나타내는 시그널.
이 예외는 주로 데이터 입력 스트림의 종료를 알리기 위해서 사용된다. 다만, 다른 많은 입력 조작에서는 스트림이 종료했을 때에 예외를 Throw 하지 않고 특정의 값을 리턴한다.
- MalformedURLException
	무효인 서식의 URL가 발생한 것을 나타내기 위해서 발생한다.

### 👉🏻 Runtime Exception
- NullPointerException
	객체가 필요한 경우임에도 어플리케이션이 null을 사용하려고 하면 발생된다.



---
cf) 이미지 출처)
https://reference-m1.tistory.com/246
http://cris.joongbu.ac.kr/course/java/api/java/io/IOException.html
