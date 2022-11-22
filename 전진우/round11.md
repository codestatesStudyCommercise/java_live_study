# 11회차 - 람다

<aside>
➡️ 작성일 : 2022.11.20

</aside>

---

# Variable Capture : Lambda Capture

```java
static class LambdaTest {
    public static int MAX_NUM = 10000;
    public int value = 3;

    public void doTest(){
        int regionValue = 1000;
        LambdaTest lambdaTest1 = new LambdaTest();
        LambdaTest lambdaTest2 = new LambdaTest();

        Runnable r = () -> {
            System.out.println(regionValue); // 에러 발생 지점2
            lambdaTest1.value = 4; // 에러 발생 지점1
            LambdaTest.MAX_NUM = 90;
            System.out.println("lambdaTest.MAX_NUM = " + LambdaTest.MAX_NUM);
            //lambdaTest1 = lambdaTest2; // 시도 시 지점2 에러 발생
        };
        r.run();

        // regionValue = 20; // 시도시 지점1 에러 발생
        System.out.println(lambdaTest1.value);
    }
}

public static void main(String[] args) {
    LambdaTest lambdaTest = new LambdaTest();
    lambdaTest.doTest();
}
```

- 람다에서 접근 가능한 외부 변수
    - 지역변수 (stack 영역에 저장)
    - static 변수 (method 영역에 저장)
    - 인스턴스 변수 (heap 영역에 저장)
    - 이때, 지역변수는 수정이 불가능
- 람다 캡처링
    - {외부에서 정의된 변수: 자유변수 (free variable)}를 참조하는 변수를 
    람다식 내부에 저장하고 사용하는 동작
    - 제약사항
        - `local variables referenced from a lambda expression must be final or effectively final`
        - `람다 표현식에 사용되는 변수는 final 또는 유사 final이어야 합니다`
            
            → 값이 단 한번만 할당되는 지역변수만 캡처 가능하다는 의미 
            
        - 지역변수를 사용하려고 시도시 (람다식의 바디에서 캡처하려는 시도 시 ) 컴파일 에러 발생
- 람다캡처링 제약사항 이유
    - 람다 실행을 위해 람다는 새로운 스택을 생성
    - 실행되고 있던 메서드의 스택 데이터들을 람다의 스택으로 복사
        - 복사해서 들고오기에 값을 직접 참조가능 (call by value)
        - 그러나 수정은 다른 문제 → 지역변수 특성에 다른 제약사항 발생
        - 복사방식을 사용하므로 원본 지역변수의 할당이 해제 되어도 람다 내부에서 사용되는 데이터는 그대로 유지된다.
        - 원본 데이터가 변경 시 복사본 데이터는 원본이 변경되었는지 알 수 없음
        - 그러므로 복사본의 값이 변경되면 안된다 → 값이 한번만 할당되는 지역변수만 사용 가능
    - 이로 인해 람다 캡처링시 지역변수로 final 또는 유사 final 만 사용 가능하다는 제약사항이 존재하게 됨
        
        *** effectively final : 유사final
        
        - final 키워드는 선언되지 않았지만 값이 재할당 되지 않아 final 과 유사하게 동작하는것
    - 반면 static 변수와 인스턴스 변수는 사용이 가능한데
        
        이는 heap 이나 method 메모리 영역안에 있는 데이터를 
        call by reference 방식을 통해 주소를 통한 값을 참조하기 때문 
        

# 메소드 레퍼런스

- 람다표현식을 더 간단하게 표현하는 방법
    
    ```java
    Function<String, Integer> f = (String s) -> Integer.parseInt(s);
    
    Function<String, Integer> f = Integer::parseInt;
    ```
    
- 람다식이 하나의 메서드만 호출하는 경우 사용 가능
    
    ```java
    // 클래스명::메서드명
    BiFunction<String, String, Boolean> f1 = (s1, s2) -> s1.equals(s2);
    BiFunction<String, String, Boolean> f2 = String::equals;
    
    // 참조변수명::메서드명
    String str = new String();
    Function<String, Boolean> f3 = (x) -> str.equals(x);
    Function<String, Boolean> f4 = str::equals;
    ```
    
- 생성자의 메서드 참조
    
    ```java
    Supplier<LambdaTest> s1 = () -> new LambdaTest();
    Supplier<LambdaTest> s2 = LambdaTest::new;
    ```
    

---

- 참고
    - [https://yeon-kr.tistory.com/211](https://yeon-kr.tistory.com/211)
    - [https://cobbybb.tistory.com/19](https://cobbybb.tistory.com/19)
    - [https://bugoverdose.github.io/development/lambda-capturing-and-free-variable/](https://bugoverdose.github.io/development/lambda-capturing-and-free-variable/)
    - [https://futurecreator.github.io/2018/08/02/java-lambda-variable-scope/](https://futurecreator.github.io/2018/08/02/java-lambda-variable-scope/)
    - [https://velog.io/@ehdrms2034/JAVA-8-람다-표현식](https://velog.io/@ehdrms2034/JAVA-8-%EB%9E%8C%EB%8B%A4-%ED%91%9C%ED%98%84%EC%8B%9D)
    - 남궁성 - 자바의 정석