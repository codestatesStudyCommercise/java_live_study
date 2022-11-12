#### 예외 처리(Exception Handling)
잠재적으로 발생할 수 있는 비정상 종료나 오류에 대비하여 정상 실행을 유지할 수 있도록 처리하는 코드 작성 과정

**자바에서 모든 예외는 Exception이라는 클래스를 상속**

> 자바의 예외 처리 방법 
 ``try`` - ``catch`` - ``finally``, ``throw`` , ``throws`` , 

## 🟡 try - catch - finally
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

#### 1) try
- try 블럭에 예외가 발생할 가능성이 있는 코드를 작성한다. 
- 만약 작성한 코드가 예외 없이 정상적으로 실행된다면, finally 블럭이 실행된다.

#### 2) catch
- 예외가 발생했을 때 처리하는 동작을 명시하는 블록이다.
	즉, 예외가 발생하는 경우 실행되는 코드이며 여러 종류의 예외를 처리할 수 있다.

- 모든 예외를 받을 수 있는 Exception 클래스 하나로 처리도 가능하다.

- catch 블럭이 여러 개인 경우, 일치하는 catch 블럭을 찾아 그 블럭만 실행이 되고 예외처리 코드가 종료되거나 finally 블럭으로 넘어간다.
만약 일치하는 블럭을 찾지 못하는 경우, 예외 처리는 되지 않는다.

- 보통 첫번째 catch블럭에 예외 메세지를 출력하고 로그를 남긴다.
```
printStackTrace() 메소드

ex) e1.printStackTrace() / e.printStackTrace(),,,
어느 부분에서 예외가 발생했는지 알려주는 추적 로그.
```
- catch 블럭이 여러 개인 경우, 상속관계에 있는 예외 중 부모가 위의 catch, 자식 예외 클래스가 아래의 catch에 놓일 수 없다.
ex)
```java
try{
	//...//
} catch (Exception e){
	//컴파일 오류 발생
} catch (IOException e){

}

```
 이 경우, Exception 클래스는 모든 예외 클래스들의 부모이기 때문에 IOException보다 위에서 처리할 경우, IOException이 발생할 경우, 첫번째 catch에서도 IOException 예외 처리가 가능하다. 때문에 IOException의 두번째 catch 블록에는 영원히 도달하지 않는다. 그러므로 IOException만을 따로 처리하고자 한다면 IOException을 Exception 위로 올려야 한다.
 즉, 범위가 더 좁은 예외를 처리하는 catch 블록을 먼저 명시하고, 범위가 더 넓은 예외를 처리하는 catch 블록은 나중에 명시해야만 정상적으로 해당 예외를 처리할 수 있습니다.

```java
IOException
I/O : Input / Output
java.io.IOException
```

- Java SE 7부터는 '|' 기호를 사용하여 하나의 catch 블록에서 여러 타입의 예외를 동시에 처리할 수 있다.
	ex) 
```java
try {

    this.db.commit();

} catch (IOException | SQLException e) {

    e.printStackTrace();

}
```
하지만 둘 이상의 예외 타입를 동시에 처리하는 catch 블록에서 매개변수로 전달받은 예외 객체는 묵시적으로 final 제어자를 가지게 된다.
때문에 catch 블록 내 해당 매개변수에는 어떠한 값도 대입할 수 없다.


#### 3) finally
- finally 블럭은 필수 옵션은 아니지만, 포함되는 경우에는 예외 발생 여부와 상관없이 항상 실행된다.
- 여기서는 임시 파일의 삭제 등의 뒷정리 코드가 작성된다.
```
finally 블록 보통 어떤 경우에 사용할까?
자원이나 DB에 커넥션 한 경우, 파일 닫기, 연결 닫기(close) 등과 같이 "정리" 코드를 넣는 데에 사용된다.
```

---
## 🟡 throws

예외를 호출한 곳으로 다시 예외 떠넘기는 방법
=> "예외를 여기서 처리하지 않고 나를 불러다가 쓰는 곳에 예외 처리를 전가하겠다."
=> 즉, 자신을 호출한 상위 메소드로 에러를 던지는 역할.
-> 코드 짜는 사람이 선언부만 보고 어떤 예외가 발생할 수 있는지 알 수 있다.

작성법
```java
반환타입 메서드명(매개변수, ...) throws 예외클래스1, 예외클래스2, ... {
	//...
}
```
=> 메서드 선언부 끝에 ``throws`` 키워드와 발생할 수 있는 예외들을 쉼표로 구분해서 나열하면 된다.

만약, 특정 메서드에서 모든 종류의 메서드가 발생할 가능성이 있는 경우!
```java
void ExampleMethod() throws Exception {
}
```
=> Exception 클래스는 모든 예외 클래스의 상위 클래스이므로 ``throws Exception`` 할 경우 Exception 하위의 모든 예외 클래스들이 포함된다.

- main() 메서드에도 throws 키워드를 사용해서 예외를 넘길 수 있는데, 이 경우에는 JVM이 최종적으로 예외의 내용을 콘솔에 출력하여 예외 처리를 수행한다.

> print() 출력 메서드 시리즈는 왜 예외 처리를 하지 않는가?
자바에서 print(), println(), printf() 메서드에만 자체적으로 예외처리를 해놨기 때문에 따로 예외 처리를 하지 않아도 된다.

---
### throwable 클래스

자바에서 Throwable 클래스는 모든 예외의 조상이 되는 Exception 클래스와 모든 오류의 조상이 되는 Error 클래스의 부모 클래스이다.
Throwable 타입과 이 클래스를 상속받은 서브 타입만이 JVM이나 throw 키워드에 의해 던져질 수 있다.

---
## 🟡 throw

**강제로 예외 발생시키기**

ex)
```java
Exception e = new Exception("오류메시지");

//...

throw e;
```
위의 예처럼 생성자에 전달된 문자열은 getMessage() 메소드를 사용하여 오류 메시지로 출력할 수 있다.

```java
try {
            throw new Exception(); // 강제로 Exception 객체를 생성
        } catch (Exception e) {
            System.out.println("예외를 강제로 발생했습니다.");
        }
```

> WHY?
예외를 한번더 처리하기 위함


---
## 🟡 사용자 정의 예외 처리 클래스

In Java, Exception 클래스를 상속받아 자신만의 새로운 예외 클래스를 정의하여 사용할 수 있다.
사용자 정의 예외 클래스에는 생성자뿐만 아니라 필드 및 메소드도 원하는 만큼 추가할 수 있다.
ex)
```java
class MyException extends RuntimeException {

    MyException(String errMsg) {

        super(errMsg);

    }

}
```
요즘에는 Exception 클래스가 아닌 예외 처리를 강제하지 않는 RuntimeException 클래스를 상속받아 작성하는 경우도 많다.

---
## 🟡 try-with-resources 문

	Java SE 7부터 사용 가능.
사용한 자원을 자동으로 해제해 주는 기능.

작성법
```java
try (파일을열거나자원을할당하는명령문) {

     ...

}
```
위와 같이 try 블록에 괄호(())를 추가하여 파일을 열거나 자원을 할당하는 명령문을 명시하면, 해당 try 블록이 끝나자마자 자동으로 파일을 닫거나 할당된 자원을 해제해 준다.

**java SE 7 이전** (문자열 한줄 읽어오는 코드)
```Java
static String readFile(String filePath) throws IOException {

    BufferedReader br = new BufferedReader(new FileReader(filePath));

    try {

        return br.readLine();

    } finally {

        if (br != null)

            br.close();

    }

}
```
**Java SE 7 이후**
```java
static String readFile(String filePath) throws IOException {

    try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {

        return br.readLine();

    }

}
```
Java SE 7 이전에는 finally 블록을 사용하여 사용한 파일을 닫아줘야 했지만,
Java SE 7 이후부터는 try-with-resources 문을 사용하여 자동으로 파일의 닫기를 수행할 수 있다.



---
cf)
https://reakwon.tistory.com/155
https://cheershennah.tistory.com/147
http://www.tcpschool.com/java/java_exception_class
http://www.tcpschool.com/java/java_exception_throw
https://bvc12.tistory.com/196
