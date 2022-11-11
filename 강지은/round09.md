<br><br>

# Exception과 Error의 차이는?

### **⏺ 에러 vs 예외**

**에러(Error) : 한번 발생하면, 복구하기 어려운 수준의 심각한 오류 (ex - StackOverflowError, OutOfMemoryError)**

**예외(Exception) : 잘못된 사용, 코딩으로인해 상대적으로 미약한 수준의 오류 (코드수정을 통해 수습이 가능)**

<br><br>

# 자바가 제공하는 예외 계층 구조

<br>

![image](https://user-images.githubusercontent.com/48430781/201230530-5976e211-1100-4583-8c13-d116a3d74b8f.png)

<br>

### ✔ Throwable 클래스

**모든 예외와 에러 클래스들의 조상이 되는 클래스 (Object의 자식)**

<br>

**예외나 에러에 대한 정보를 확인할 수 있는 메소드를 가지고 있음**

<br>

- **getMessage()** : 해당 throwable 객체에 대한 자세한 내용을 반환
- **printStackTrace()** : 예외나 에러가 발생 할 때까지의 이력을 출력
- **toString()** : 해당 throwable 객체의 간단한 내용을 반환

<br>

**Throwable 밑에 Error와 Exception이 있는데,** 

**에러는 시스템 레벨의 심각한 에러,  Exception은 개발자가 로직을 추가해 처리할 수 있다.**

<br><br>

---

<br><br>

# **RuntimeException과 RE가 아닌 것의 차이**

 **RuntimeException을 상속**하지 않고 꼭 처리해야 하는 **Checked Exception**
명시적으로 처리하지 않아도 되는 **Unchecked Exception**    

<br>

![image](https://user-images.githubusercontent.com/48430781/201230600-5c5af534-5b76-4729-a8b9-1507512c8ad6.png)

<br>

### ⏺ RuntimeException (UncheckedException)

**런타임 시에 예외를 발생**

<br>

실행 전에는 컴파일 에러를 발생시키지 않는다.

예외처리를 강제하지는 않지만 해당 내용이 런타임 시에 예외를 발생시킬 수 있음을 인지하면 예외를 처리해주는 것이 좋음

→  **NullPointerException, IndexOutOfBoundsException, ArithmeticException** 등 로직을 짜면서 발생가능한 exception

<br>

ArithmeticException

0으로 정수를 나누는 경우에 발생,  컴파일 에러는 발생 x

```java
package com.livestudy.ninth;
public class RuntimeExceptionTest {
    public static void main(String[] args) throws IOException {

        System.out.println(3/0);    //컴파일 에러 발생 X
    }
}
```

<br>

런타임시 에러 발생 확인 

즉 **ArithmeticException은 UncheckedException이다.**

![image](https://user-images.githubusercontent.com/48430781/201230720-4f36020d-9847-42e6-90ff-8e6bf1d814bd.png)

<br><br>

- 트랜잭션을 Rollback한다.
- 트랜잭션 적용시 전파방식과 롤백 규칙등을 적절히 사용해 효율적인 애플리케이션을 구현할 수 있다.
- 나중에 볼만한 자료 [https://cheese10yun.github.io/checked-exception/](https://cheese10yun.github.io/checked-exception/)

<br><br>

### ⏺ 그 외

RuntimeException이 아닌 Exception (CheckedException)

- 컴파일 단계에서 확인 가능함. → 실행하기 전에 예외를 반드시 처리해야함.
- 예외가 발생하면 Roll-back 하지 않고 예외를 던져준다.

→ IOException, SQLException

ex) BufferedReader 

데이터를 모두 읽은 이후에는 해당 객체를 종료해줘야 하는데, close() 하면, 컴파일 에러가 남. →  **IOException이 CheckedException**이기 때문

**내용 그대로 Stream으로 뭘 써야 하는데 이게 닫혀 버렸기 때문에 발생함.**

```java
package com.livestudy.ninth;

import java.io.BufferedReader;
import java.io.InputStreamReader;

public class RuntimeExceptionTest {
    public static void main(String[] args) {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        br.close();     //컴파일 에러 발생 (IOException)
    }
}
```
<br>

![image](https://user-images.githubusercontent.com/48430781/201230768-5248b9b0-9902-4305-af33-d666dc144afe.png)
            
<br><br>

# **커스텀한 예외 만들기**

Exception 클래스를 상속받아 사용자가 직접 예외를 커스텀해서 사용할 수 있다. 

<br>

1) 일반적으로 Exception 클래스를 상속 (필요에 따라 예외클래스 선택)

2) 생성자를 통해 어떤 값이 들어왔을 때 필드-에러코드를 설정하는 식

3) public 으로 에러코드값을 리턴하도록 설정해줬다.

<br>

CustonException <br>
- message만 파라미터로 들어오면, ERR_CODE 는 200
- int ERR_CODE까지 파라미터로 들어오면 ERR_CODE 는 100
- 커스텀 예외 클래스의 생성자를 확인하면, super(message)라는 메소드를 확인할 수 있음.
- 이는 위에서 **Throwable 클래스의 getMessage()를 통해 메세지를 처리함**
<br><br>

```java
public class CustomException extends Exception {
    private final int ERR_CODE;

    //에러 메세지(커스텀)
    public CustomException(String message) {
        this(message, 200);
    }

    // 에러 메세지(커스텀), 에러 코드(커스텀)
    public CustomException(String message, int ERR_CODE) {
        super(message);
        this.ERR_CODE = ERR_CODE;
    }

    // 에러코드 리턴
    public int getErrorCode() {
        return ERR_CODE;
    }
}
```

<br><br>

Main 

- main(), checkAge()

<br><br>

```java

public class Main {
    public static void main(String[] args){

        try{
            checkAge(1300);
            //checkAge(2022);
        }catch (CustomException e){

            e.printStackTrace(); //예외/에러 발생할 때까지의 이력을 출력

            System.out.println("ERR_MSG : "+ e.getMessage()); // 자세한 내용 반환
            System.out.println("ERR_CODE : "+ e.getErrorCode());
        }

    }
    private static void checkAge(int birthYear) throws CustomException{
        final int YEAR = 2021;

        if (YEAR - birthYear < 0 ){
            throw new CustomException("Too big birth year");
        }
        if(birthYear < 1800){
            throw new CustomException("maybe wrong birth year", 100);
        }
    }
}
```

<br><br>


1) main에서 try-catch를 통해 어떤 사람이 태어난 년도를 확인한다. <br>
2) checkAge에서 유효성 검증을 해주는 코드를 작성, 유효범위에 어긋나면 <br>

3) throw : 인위적으로 예외를 발생시킨다 — 여기에서 CustomException을 new연산자로 CustomException을 생성하고, 인자값을 전달한다. <br>

4) throws 키워드를 사용했기 때문에 해당 메소드의 호출 지점으로 예외가 던져진다. <br>

5) main()으로 던져진 CustomException은 catch 가 잡아서, e로 사용할 수 있다.<br>

6) CustomException은 Throwable을 상속받았기 때문에  Throwable메서드를사용할수있다. <br>

- getMessage(), printStackTrace(), toString()  <br><br>


![image](https://user-images.githubusercontent.com/48430781/201230845-e1114826-4346-47b8-a27d-ff6d402c8307.png)

<br><br>
---
<br><br>
 

### References

[https://www.nextree.co.kr/p3239/](https://www.nextree.co.kr/p3239/)

[https://velog.io/@zayson/백기선님과-함께하는-Live-Study-9주차-예외-처리](https://velog.io/@zayson/%EB%B0%B1%EA%B8%B0%EC%84%A0%EB%8B%98%EA%B3%BC-%ED%95%A8%EA%BB%98%ED%95%98%EB%8A%94-Live-Study-9%EC%A3%BC%EC%B0%A8-%EC%98%88%EC%99%B8-%EC%B2%98%EB%A6%AC)
