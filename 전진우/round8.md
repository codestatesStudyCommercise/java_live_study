# 8주차 - Enum

<aside>
➡️ 작성일 : 2022.11.10

</aside>

---

- 열거형 : enumerated type
- 서로 연관된 상수들의 집합
- **사용이유**
    - 상수명의 중복 방지
    - 타입 안정성 문제 해결
        - 의도하지 않은 타입의 객체가 저장되는것을 막고 저장된 
        객체를 꺼내올 시 
        원래의 타입과 다른 타입으로 잘못 형변환되어 발생할 수 있는 오류를 줄여준다는 뜻
        - 자실바열 거으형실  같 값 도같 도도타입입르다면파일컴파파에러 발생
        - 일반적인 상수의 값을 비교시 서로 의미가 다른 값임에도 상수값이 같으면 
        true 가 나올 수 있다. → 타입에 대한 안정성 문제
    - 재컴파일 불필요
        - 상수는 값이 바뀌면 해당 상수를 참조하는 모든 소스를 다시 컴파일 해야한다.
        - 열거형 상수는 기존의 소스를 다시 컴파일 하지 않아도 된다.
    - switch 문에서는 조건으로 사용자 정의 타입은 불가능한 반면 enum 은 가능
        - 가능 : char, byte, short, int, Character, Byte, Short, Integer, String, enum
        - case 문에 열거형 이름 없이 상수 이름만 적어야하는것에 유의
    

---

# 열거형 사용

```java
// 선언
enum Seasons { SPRING, SUMMER, FALL, WINTER}
enum Language { C, JAVA, PYTHON, JAVASCRIPT}

public class Main {
    public static void main(String[] args) {

        // 다양한 방식의 Enum 참조
        Seasons seasons1 = Seasons.SPRING;
        Seasons seasons2 = Seasons.valueOf("SPRING");
        Seasons seasons3 = Enum.valueOf(Seasons.class, "SPRING");

				System.out.println("Seasons.SPRING == Seasons.SPRING : " + (seasons1 == seasons2));
        // System.out.println("Seasons.SPRING > Seasons.SPRING : " + (seasons1 > seasons2)); : 대소비교 불가능
        System.out.println("Seasons.SPRING.compareTo(Seasons.SPRING) : " + (seasons1.compareTo(seasons2)));

        switch (seasons1) {
            // case 문에 열거형 이름 없이 상수 이름만 적어야하는것에 유의
            case SPRING:
                System.out.println("봄");
                break;
            case SUMMER:
                System.out.println("여름");
                break;
            case FALL:
                System.out.println("가을");
                break;
            case WINTER:
                System.out.println("겨울");
                break;
        }
    }
}
```

- **열거형은 각 상수 하나하나가 열거형 객체이다.**
    
    ```java
    // 다음과 같이 비유될 수 있다.
    class Seasons {
    		static final Seasons SPRING = new Seasons("SPRING");
    		static final Seasons SUMMER = new Seasons("SUMMER");
    		static final Seasons FALL = new Seasons("FALL");
    		static final Seasons WINTER = new Seasons("WINTER");
    
    		private String name;
    
    		private Seasons(String name) {
    				this.name = name;
    		}
    }
    ```
    
    - 이로 인해 열거형에 추상메서드 선언시 각 객체 모두에서 구현해주어야한다.
- switch 문 사용 가능
    - case 문에 열거형 이름 없이 상수 이름만 적어야하는것에 유의
- 열거형 상수간의 비교는 ‘==’ 를 사용할 수 있다.
    - 각 열거형 상수의 값은 각 객체의 주소이며 값이 변하지 않으므로 비교 가능
        - `static final Seasons SPRING = new Seasons(”SPRING”);` 처럼 비유될 수 있다.
    - equals( ) 가 아닌 == 비교가 가능하다는것은 성능이 좋다는 말이다.
- < , > 와 같은 비교 연산자는 불가능
    - `int compareTo()` 는 사용 가능

---

# 맴버를 가진 열거형

```java
// 열거형 상수의 값을 가지기 위해서는 맴버와 생성자가 필요하다.
enum Direction{ 
		EAST(1), SOUTH(5), WEST(-1), NORTH(10)
		
		// 정수를 저장할 맴버(인스턴스 변수) 추가
		// 상수이므로 final (제약은 없으나 상수라는 의미상 있는게 맞다.)
		private final int value; 

		// 생성자 
		// 열거형의 생성자는 제어자가 묵시적으로 private 이다.
		Direction(int value){
				this.value = value;
		}
		
		// getter 를 통해 값을 획득 		
		public int getValue(){
				return value;
		}
}

```

## 각 상수는 여러 값을 가질 수 있다.

```java
enum Coffees {
    // 끝에 세미콜론 유의
    AMERICANO(10, 150), CAPPUCCINO(110, 75), CAFFELATTE(180, 75), CAFFEMOCHA(290, 95);

    // 상수의 값을 담기위한 변수 선언 : private final
    private static final Coffees[] COFFEES_ARR = Coffees.values();
    private final int kcal;
    private final int caffeine;
    private static final int dailyMaxCaffeine = 400;

    // 생성자 : 열거형은 묵시적 private
    Coffees(int kcal, int caffeine) {
        this.kcal = kcal;
        this.caffeine = caffeine;
    }

    // 인스턴스 메서드 : 하루 권장섭취량 출력
    public void recommendDailyMax(){
        System.out.println("섭취한 커피 : " + this);
        System.out.println("섭취한 카페인 양 : " + this.caffeine + " mg");
        System.out.println("하루 권장 섭취량은 " + dailyMaxCaffeine + "mg 입니다.");
        System.out.println("권장 섭취량으로부터 " + (dailyMaxCaffeine - this.caffeine) + "mg 남았습니다.");
        System.out.println("***참고 " + this + " 칼로리 정보 : " + kcal + " kcal");
    }

    // static 변수 : 카페인이 가장 낮은 커피 return
    public static Coffees getLowestKcalCoffee(){
        int index = 0;
        int temp = COFFEES_ARR[0].kcal;
        for (int i = 0; i < COFFEES_ARR.length; i++) {
            if (temp > COFFEES_ARR[i].kcal){
                index = i;
                temp = COFFEES_ARR[i].kcal;
            }
        }
        return COFFEES_ARR[index];
    }

    // getter
    public int getKcal() {
        return kcal;
    }
    public int getCaffeine() {
        return caffeine;
    }
}

public class Main {
    public static void main(String[] args) {

        // Test2
        Coffees latte = Coffees.CAFFELATTE;
        // 인스턴스 메서드 출력 : 권장 섭취량 대비 섭취량 출력
        latte.recommendDailyMax();

        System.out.println();

        Coffees americano = Coffees.getLowestKcalCoffee(); // static 메서드 호출
        // 인스턴스 메서드 출력 : 권장 섭취량 대비 섭취량 출력
        americano.recommendDailyMax();
		}
}
```

- 열거형 상수가 값을 가지기 위해선 값을 저장할 필드와 생성자가 필요하다.
- 열거형의 생성자는 묵시적으로 private 이며 외부에서 호출할 수 없다.
- 열거형은 필드와 메서드를 가질 수 있다.
    - 필드는 상수라는 목적에 맞게 final 형으로 선언
        - 반드시 final 이라는 제약은 없지만 목적상 final 로 선언
    - 메서드는 static 메서드와 인스턴스 메서드 모두 선언가능

## 열거형은 추상메서드를 가질 수 있다.

```java
// 상수들에 메서드구현에 대한 부분을 추가해야한다.
AMERICANO(10, 150){
        boolean isIncludeMilk(){
            System.out.println("추상메서드 구현 : private static 필드 사용 : " + dailyMaxCaffeine);
            // private 필드는 사용 불가
            // System.out.println("추상메서드 구현 : private final 필드 사용 : " + basicValuePrivate);
            System.out.println("추상메서드 구현 : protected final 필드 사용 : " + basicValueProtected);
            return false;}
    },
CAPPUCCINO(110, 75){
    boolean isIncludeMilk(){
        System.out.println("추상메서드 구현 : private static 필드 사용 : " + dailyMaxCaffeine);
        // private 필드는 사용 불가
        // System.out.println("추상메서드 구현 : private final 필드 사용 : " + basicValuePrivate);
        System.out.println("추상메서드 구현 : protected final 필드 사용 : " + basicValueProtected);
        return true;}
},
CAFFELATTE(180, 75){
    boolean isIncludeMilk(){
        System.out.println("추상메서드 구현 : private static 필드 사용 : " + dailyMaxCaffeine);
        // private 필드는 사용 불가
        // System.out.println("추상메서드 구현 : private final 필드 사용 : " + basicValuePrivate);
        System.out.println("추상메서드 구현 : protected final 필드 사용 : " + basicValueProtected);
        return true;}
},
CAFFEMOCHA(290, 95){
    boolean isIncludeMilk(){
        System.out.println("추상메서드 구현 : private static 필드 사용 : " + dailyMaxCaffeine);
        // private 필드는 사용 불가
        // System.out.println("추상메서드 구현 : private final 필드 사용 : " + basicValuePrivate);
        System.out.println("추상메서드 구현 : protected final 필드 사용 : " + basicValueProtected);
        return true;}
};

// ,,, 생략,,,,,,,,,,,,,,,,,,,,,,,,,,

// 추상메서드 선언 
abstract boolean isIncludeMilk();

// ,,, 생략,,,,,,,,,,,,,,,,,,,,,,,,,,

private final int basicValuePrivate = 99999;
protected final int basicValueProtected = 77777;
```

- 열거형에 추상메서드를 선언시 각 열거형 상수들은 추상메서드를 반드시 구현해야한다.
    - 열거형은 각 상수 하나하나가 열거형 객체이기때문
- **주의**
    - 각 상수 내부에서 열겨형의 필드를 사용하기 위해서는 protected 로 선언해야 각 상수에서 접근이 가능하다.
        - static 이 아닌 pirivate 는 불가능
        - static 필드는 접근 가능

---

# java.lang.Enum

- `String name()`
    - 열거형 상수의 이름을 문자열로 반환
- `int compareTo()`
    - 주어진 매개 값과 비교해서 순번 차이를 return
- `열거형 valueOf(String name)`
    - `static E valuesOf(String name)`
    - 지정된 열거형에서 name 과 일치하는 열거형 상수를 return
- `열거형배열 values()`
    - `static E values()`
    - 모든 열거형 상수들을 배열로 return
    - `Season[] allSeason = Season.values();`
- `int ordinal()`
    - 열거형 상수가 정의된 순서를 반환 (0부터 시작)
    - 그러나 이 값을 열거형 상수의 값으로는 사용하지 않는것이 좋다.
        
        → 필드를 선언해서 사용해라
        
    - 이 값은 내부적인 용도로만 사용되기 위한 것이다.
    - 단순히 열거된 순서다.
    - 이값을 활용하는 코드는 결코 좋은 코드가 아니다.

---

# EnumSet

- enum 클래스와 함께 동작하는 특수한 Set 컬렉션이다.
- java.util.EnumSet
    
    ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/1e2605f0-2d5e-4c85-98ba-7f9172c98e1b/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221111%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221111T143436Z&X-Amz-Expires=86400&X-Amz-Signature=1987d9d4b17c475765c2fadfbb11ac3169293a0cdd330b549501c7973fc299a6&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
    
    [https://www.baeldung.com/java-enumset](https://www.baeldung.com/java-enumset)
    
- enum 클래스와 함께 동작하는 특수한 Set 컬렉션이다.
    - Set 인터페이스를 구현하고 AbstractSet 을 상속한다.
- 컬렉션 Set 의 특징을 가진다.
    - 데이터를 중복 저장할 수 없다.
    - 저장 순서가 보장되지 않는다.
- AbstractSet 및 AbstractCollection이 Set 및 Collection 인터페이스의 거의 모든 메서드에 대한 구현을 제공하지만 EnumSet은 대부분을 재정의한다.
- 내부적으로 비트벡터로 구현되어있다.
    - 메모리를 적게 효율적으로 사용한다.
    - ***비트벡터란
        - 중복되지 않는 정수 집합을 비트로 나타내는 방식이다.
        - 최소의 저장공만만으로 정수집합을 표현 가능
        - 0~7 의 범위의 정수를 담고자 한다면 1바이트만 있으면 표현 가능
        - [https://cjh5414.github.io/bit-vector/](https://cjh5414.github.io/bit-vector/)
        - [https://velog.io/@jimmy48/비트-벡터Beat-Vector](https://velog.io/@jimmy48/%EB%B9%84%ED%8A%B8-%EB%B2%A1%ED%84%B0Beat-Vector)
        
    
    ---
    

## EnumSet 사용시 고려사항

- 열거형 값만 포함할 수 있으며, 모든 값은 동일한 열거형에 속해야한다.
- null 을 추가할 수 없다.
- 쓰레드에 안전하지 않다.
    - 필요시 외부에서 동기화해주어야한다.
- 요소는 열거형에서 선언된 순서에 따라 저장된다.
- iterator 를 사용한 복제에서, 
fail-safe 하므로 컬렉션을 반복하면서 컬렉션이 수정될 때 *ConcurrentModificationException* 이 발생하지 않음
    - *** fail-safe iterator 와 fail-fast iterator 란
        - [https://www.baeldung.com/java-fail-safe-vs-fail-fast-iterator](https://www.baeldung.com/java-fail-safe-vs-fail-fast-iterator)
        
    
    ---
    

# 종류

- JDK 에서 2가지 EnumSet 구현체를 제공
    - EnumSet의 팩토리 메서드는 enum 요소의 수에 따라 다른 인스턴스를 생성한다.
        - 이때 컬렉션에 저장될 요수의 수가 아니라 열거형 클래스의 크기만을 고려한다.
            
            ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a2532a89-908d-4ac0-91d8-c2c715d592af/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221111%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221111T143514Z&X-Amz-Expires=86400&X-Amz-Signature=f106c88b2c421218c420bf1932cd33e34ef421aa603249b352ad4f0a375521cc&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
            
            < java.util.EnumSet > 
            
    - **RegularEnumSet**
        - 비트벡터를 표현하기 위해 하나의 long 을 사용
        - long 의 각 비트는 enum 값을 나타낸다.
            - long 은 64비트 해당 구현은 최대 64개의 요소를 저장 가능
        - 열거형의 i 번째 값은 i번째 비트에 저장되므로 값이 있는지 여부를 쉽게 파악 가능
    - **JumboEnumSet**
        - long 배열을 비트 벡터로 사용
            - 64개 이상의 원소를 저장 가능
        - RegularEnumSet 와 비슷하게 동작하지만 저장된 배열 인덱스를 찾기위해 추가 연산을 수행한다.
    - *** 참고 : EnumSet 이 생성자를 사용하는 이유
        - [https://siyoon210.tistory.com/152](https://siyoon210.tistory.com/152)
    - *** 정적 팩토리 메서드란
        - [https://tecoble.techcourse.co.kr/post/2020-05-26-static-factory-method/](https://tecoble.techcourse.co.kr/post/2020-05-26-static-factory-method/)

---

## EnumSet 사용 이유

> 열거형 값을 Set 에 저장할 때 다른 Set 구현체보다 항상 우선시 되어야한다.
> 

> 이펙티브 자바, 비트 필드 대신 EnumSet을 사용하라
> 
> 
> 열거할 수 있는 타입을 한데 모아 집합 형태로 사용한다고 해도 비트 필드를 사용할 이유는 없다. 
> 
> EnumSet 클래스가 비트 필드 수준의 명료함과 성능을 제공하고 열거 타입의 장점까지 선사하기 때문이다. 
> 
> EnumSet의 유일한 단점이라면 불변 EnumSet을 만들 수 없다는 것이다. 
> 
> 그래도 향후 릴리스에서 수정되리라 본다. 그때까지는 Collections.unmodifiableSet으로 EnumSet을 감쌀 수 있다.
> 

- 비트벡터의 특성으로 매우 작은 메모리를 효율적으로 사용한다.
- EnumSet 의 모든 메서드는 산술 비트 연산을 사용하여 구현되므로 연산이 매우 빠르게 처리된다.
- 다른 Set 구현체에 비해 상대적인 장점
    - HashSet 과 같이 다른 Set 구현체에 비해 데이터가 예상 가능한 순서대로 저장하여
        
        각 계산을 하는데 하나의 비트만이 검사하면 되므로 더 빠르다.
        
    - 또한 HashSet 처럼 데이터를 저장할 버킷을 찾는데 hashcode 를 계산할 필요가 없다.

## 사용

```java
// 생성
EnumSet<Coffees> coffees1 = EnumSet.noneOf(Coffees.class);
EnumSet<Coffees> coffees2 = EnumSet.allOf(Coffees.class);
EnumSet<Coffees> coffees3 = EnumSet.of(Coffees.CAFFELATTE, Coffees.AMERICANO);

// 복사
EnumSet<Coffees> coffees4 = EnumSet.copyOf(coffees3);

// 조회
Iterator<Coffees> iterator = coffees2.iterator();
while (iterator.hasNext()){
    System.out.println(iterator.next());
}
System.out.println();

// 특정 값 제외
EnumSet<Coffees> complCoffees = EnumSet.complementOf(coffees3);
System.out.println(complCoffees);
iterator = complCoffees.iterator();
while (iterator.hasNext()){
    System.out.println(iterator.next());
}
System.out.println();

// 추가
coffees4.add(Coffees.CAPPUCCINO);
iterator = coffees4.iterator();
while (iterator.hasNext()){
    System.out.println(iterator.next());
}
System.out.println();

// 포함 확인
System.out.println("카푸치노 포함여부 : " + coffees4.contains(Coffees.CAPPUCCINO));
System.out.println();

// 삭제
coffees4.remove(Coffees.CAPPUCCINO);
System.out.println("카푸치노 포함여부 : " + coffees4.contains(Coffees.CAPPUCCINO));
System.out.println();
```

- [https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/EnumSet.html](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/EnumSet.html)
- 컬렉션 프레임워크의 맴버이므로 iterator 를 생성해 조회가능
- Set의 기능을 일부 사용 가능
- `noneOf()`
    - 지정된 요소 유형으로 빈 열거형 집합을 만든다.
- `allOf()`
    - 지정된 요소 유형의 모든 요소를 포함하는 열거형 집합을 만든다.
- `of()`
    - 들어갈 요소를 직접 입력하여 EnumSet을 생성할 수 있다.
- `copyOf()`
    - 다른 EnumSet의 모든 요소를 복사하여 EnumSet을 만들 수 있다.
- `complementOf()`
    - 원하는 요소를 제거하고 EnumSet을 생성할 수 있다.
- `add()`
    - EnumSet 에 들어갈 요소를 추가할 수 있다.
- `contains()`
    - 특정 요소가 포함됬는지 확인
- `remove()`
    - 특정 요소를 제거

---

- 참고
    - 남궁성 - 자바의 정석
    - [https://www.baeldung.com/java-enumset](https://www.baeldung.com/java-enumset)
    - [https://scshim.tistory.com/253](https://scshim.tistory.com/253)
    - [https://ryumodrn.tistory.com/95](https://ryumodrn.tistory.com/95)
    - [https://velog.io/@jimmy48/비트-벡터Beat-Vector](https://velog.io/@jimmy48/%EB%B9%84%ED%8A%B8-%EB%B2%A1%ED%84%B0Beat-Vector)
    - [https://siyoon210.tistory.com/152](https://siyoon210.tistory.com/152)
    - [https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/EnumSet.html](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/EnumSet.html)