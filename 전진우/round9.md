# 9주차 - 제네릭

<aside>
➡️ 작성일 : 2022.11.11

</aside>

---

# 용어 정리

```java
class Box<T> {}

Box<String> b = new Box<String>();
```

- `Box<T>` : 제네릭 클래스 - T의 Box 또는 T Box 라고 읽는다.
- `T` : 타입변수 , 타입매개변수 ( T 는 타입문자 )
- `Box`  : 원시타입 ( raw type)
- 제네릭 타입 호출
    - 타입 매개변수에 타입을 지정하는 것
- 파라미터화된 타입
    - 예시에서 지정된 타입 String
    - 매개변수화 된 타입
    - parameterized type

# 제네릭 사용 이유

- 타입 안정성 제공
    - 의도하지 않은 타입의 객체가 저장되는것을 막고 
    저장된 객체를 꺼내올 시 
    원래의 타입과 다른 타입으로 잘못 형변환되어 발생할 수 있는 오류를 줄여준다는 뜻
    - 객체의 타입을 컴파일시 체크하기 때문
    - **즉 컴파일 타임에 타입의 안정성을 보장받는것이 가능**
- 타입 체크와 형변환을 생략 가능

# 타입매개변수

- \<T> 에서 T 를 타입매개변수라 한다.
- \<T> 와 같은 형태로 내부에서 사용할 타입 매개변수를 선언할 수 있다.
- 자주 사용하는 표기
    - 기호의 종류만 다를 뿐 모두 임의의 참조형 타입을 의미
    - T : Type
    - E : Element
    - K : Key
    - V : Value
    - N : Number
    - R : Result

---

# 제네릭 클래스

```java
interface Plant { ... }
class Flower implements Plant { ... }
class Rose extends Flower implements Plant { ... }

// 특정 타입만 지정가능하도록 제한 
class Basket<T extends Flower & Plant> {
    private T item;
	
		public T getItem() {
        return item;
    }

    public void setItem(T item) {
        this.item = item;
    }

		// 에러 : static 메서드 안에서 T 사용 불가능
		static int compare(T t1, T t2){...} 
}

public static void main(String[] args) {

		// 인스턴스화 
		Basket<Flower> flowerBasket = new Basket<>();
		Basket<Rose> roseBasket = new Basket<>();
}
```

- 클래스의 타입 매개변수는 클래스가 인스턴스화 될때 타입이 확정된다.
- **주의**
    - static 맴버(필드, 메서드 )는 제네릭 클래스의 타입변수 T 를 사용할 수 없다.
        - 모든 인스턴스에 대해 동일하게 동작해야하므로 사용 불가
        - 반면 T 는 인스턴스 변수로 간주된다.
    - 제네릭 타입의 배열을 생성하는것은 불가능
        - 참조변수를 제네릭 배열타입으로 선언하는것은 가능
        - new 를 통해 배열을 생성하는것은 불가능
            - new 의 연산과정에서 컴파일 시점에 타입 T 가 정확이 무엇인지 알아야하나 모르기때문
    - 같은 이유로 instanceOf 역시 피연산자로 T 사용 불가능

## ****Bounded Type Parameters****

```java
// bounded type parameters 미사용 
public static <T> int countGreaterThan(T[] anArray, T elem) {
    int count = 0;
    for (T e : anArray)
        if (e > elem)  // compiler error
            ++count;
    return count;
}

// bounded type parameters 사용시
public static <T extends Comparable<T>> int countGreaterThan(T[] anArray, T elem) {
    int count = 0;
    for (T e : anArray)
        if (e.compareTo(elem) > 0)
            ++count;
    return count;
}
```

- 타입 매개변수 T 에 지정할 수 있는 타입의 종류를 제한하는 방법
- 특정 타입만 받도록 지정 가능 ( == 바운디드 타입 매개변수 == 경계 타입 매개변수)
    - extends 키워드를 사용하여 특정 타입의 자손들만 대입가능하게 설정 가능
    - 인터페이스나 클래스 관계없이 extends 를 사용
    - 여러 개를 사용시 & 사용
        - **여러 타입을 제한하고 싶을때 & 사용시 클래스가 인터페이스보다 앞쪽에 위치해야한다.**
- 예시에서 위의 경우는 매개변수로 받는 elem 이 비교가 가능한대상인지 확정되지 않아 컴파일 에러가 발생하게 된다.
    - **컴파일 타임에 에러가 난다는것 역시 중요한 점이다. : 타입을 지정하여 컴파일 타임에 타입의 안정성을 보장**
- 이를 아래의 경우로 변경하여 경계타입매개변수를 `<T extends Comparable<T>>` 와 같이 지정하여 비교가 가능한 타입만 받도록 제한하여 해결할 수 있다.

---

# 제네릭 메서드

```java
// 1 : 여기에서 선언한 타입 매개변수 T와 
class Basket<T> {                        
		...
		// 2 : 여기에서 선언한 타입 매개변수 T는 서로 다른 것입니다.
		public <T> void add(T element) { 
	
				...
		}

		// static 메서드에도 선언 가능
		static <T> int setPrice(T element) {
				...
		}

		// 메서드 정의 시점에서 사용 불가능한 경우 
		public <T> void print(T item) {
        System.out.println(item.length()); // 불가 : 정의하는 시점에서 item이 String 인지 알 수 없으므로 
				System.out.println(item.equals("Kim coding")); // 가능 : Object 의 메서드는 활용 가능 
    }
}

```

- 선언부에 제네릭 타입이 선언된 메서드
- 타입 매개변수 선언은 반환타입 앞에 작성된다.
    - 해당 메서드 내에서만 선언한 타입 매개변수 사용 가능
- 제네릭 메서드는 제네릭 클래스가 아닌 클래스에도 정의 될 수 있다.
- **제네릭 메서드의 타입 매개변수는 제네릭 클래스의 타입 매개변수와 다른것이다.**
    - 클래스의 타입매개변수는 클래스가 인스턴스화 될때 타입이 확정된다.
    - 반면 제네릭 메서드의 타입 지정은 메서드가 호출될 때 이루어진다.

---

# 제네릭 타입의 형변환

- 제네릭타입과 원시타입간의 형변환은 가능하다. (단, 경고가 발생한다.)
- 대입된 타입(파라미터화 된 타입)이 다른 제네릭 타입간의 형변환
    - **대입된 타입이 Object 일지라도 대입된 타입이 다르면 형변환이 불가능하다.**
    
    ```java
    Box<Object> objBox = null;
    Box<String> strBox = null;
    
    objBox = (Box<Object>) strBox; // 에러
    strBox = (Box<String>) objBox; // 에러
    
    Box<? extends Object> wBox = new Box<String>(); // OK
    ```
    
    - Box\<String> 를 Box\<Object> 으로 직접 형변환하는것은 불가능
    - 와일드카드가 포함된 제네릭 타입으로 형변환 하면 가능 (단, 확인되지않은 타입으로 형변환 한다는 경고 발생)
    - 마찬가지로 와일드카드가 사용된 제네릭 타입끼리도 형변환이 가능하다.

## List 와 List\<Object> 의 차이

- 어떤 메서드에 파라미터로 List 나 List\<Object> 가 명시된 상황에서의 차이
- List 는 명확히 제네릭이 아님
    - raw type 이며 제네릭 이전의 사용과의 호환성으로 만들어졌음
    - 따라서 List\<String>,  List\<Boolean> 과 같은 모든 타입을 수용가능하다.
- List\<Object>는 Object 타입을 허용한다는 의사를 컴파일러에게 명확히 전달하는 꼴
    - List\<Object> 가 아니고는 수용이 불가능하다.

## **"List\<String>은 List의 하위 타입이지만, List\<Object>의 하위 타입은 아니다."**

- **List\<String> 와 List\<Object> 타입은 전혀 다른 파라미터화된 타입을 가지며
각각 하나의 독립된 타입이므로 서로를 관계가 없다.**
- 타입 매개변수가 일치하고 두 클래스가 상속관계에 있다면 상속이 가능하다.
    - Box\<Integer> → SteelBox\<Integer>

---

# 와일드카드

- 자바의 제네릭에서 와일드카드는 어떤 타입으로든 대체될 수 있는 타입파라미터를 의미
- 사용 형태
    - `<? extends T>`
        - 상한제한 (위로는 불가능, 아래로만 가능 )
        - 상위 타입 경계 와일드카드(Upper Bounded Wildcards)
        - T 와 T 를 상속받는 하위 클래스 타입만 타입 파라미터로 받을 수 있도록 지정
    - `<? super T>`
        - 하한제한 (위로만 가능 , 아래는 불가능 )
        - 하위 타입 경계 와일드카드(Lower Bounded Wildcards)
        - T 와 T의 상위 클래스만 타입 파라미터로 받도록 지정
    - `<?>`
        - 경계가 없는 와일드카드 (Unbounded Wildcards)
        - `<? extends Object>` 와 같다
        - 모든 클래스 타입을 타입 파라미터로 받을 수 있다는 의미
- **주의**
    - **제네릭 클래스와 달리 와일드카드에는 & 를 사용할 수 없다.**

## 와일드카드 활용 예시

```java
// 와일드 카드 사용 이전 코드 
// 과일박스를 넣으면 주스를 만들어 반환하는 Juicer
class Juicer {
		... 
		// 타입매개변수 대신 특정 타입을 지정해준 상황 
		static Juice makeJuice ( FruitBox<Fruit> box) {
				String temp = "";
				for (Fruit f : box.getList()) {
						temp += f + "";
				}
				return new Juice(temp);
		}
}
```

- 우선 Juicer는 제네릭 클래스가 아니다. 또한 makeJuice()는 static 메서드이다.
- FruitBox\<Fruit> 로 고정시 FruitBox\<Apple> 과 같은 다른 타입을 매개변수로 대입할 수 없다.
    - 타입이 맞지 않으므로
- 메서드 오버로딩을 통해 만들면 되지 않나 ?
    - 제네릭 타입이 다른것만으로는 오버로딩이 성립하지않는다
        - 제네릭 타입은 컴파일러가 컴파일 할때만 사용하고 제거해버린다.
- 이같은 상황에서 와일드 카드를 도입하여 사용한다.
    - 위의 예시에서 와일드 카드 도입시
        
        ```java
        static Juice makeJuice ( FruitBox<? extends Fruit> box) {
        ```
        
        - FruitBox\< 모든 종류 Fruit 및 그 이하 클래스> 를 수용 가능하게된다.

> **제네릭**
> 
> 
> : 지금은 이 타입을 모르지만, 이 타입이 정해지면 그 타입 특성에 맞게 사용하겠다.
> 
> **와일드 카드**
> 
> : 지금도 이 타입을 모르고, 앞으로도 모를 것이다. + 데이터타입보다는 데이터로 무엇을 할지에 관심
> 

---

# Type Erasure : 제네릭 타입의 제거

- 컴파일러는 제네릭 타입을 이용해서 소스 파일을 체크하고 필요한곳에 형변환을 넣어준 뒤 제네릭 타입을 제거한다.
- 제네릭 타입은 컴파일 타임에만 사용되며 컴파일 된 파일에는 제네릭 타입에 대한 정보가 없다.
- 제네릭이 도입되기 이전의 소스코드와의 호환성을 위해서 이러한 방식을 유지한다.
- 이러한 방식으로 인해 제네릭이 다른것만으로는 오버로딩이 불가능한 이유가 된다.

1. 제네릭 타입의 경계(bound)를 제거한다.
    - 제네릭 타입이 bounded type 을 사용한 경우 ( \<T extends Fruit> 과 같은 경우) 라면 T는 Fruit 으로 치환된다.
    - \<T> 의 경우 Object 로 치환된다.
    - 이후 class 선언에서 제네릭 선언이 제거된다.
2. 제네릭 타입을 제거한 후 타입이 일치하지 않으면 형변환을 추가한다. 
    
    ```java
    T get(int i) {
    		return list.get(i); // list 의 get() 은 Object 형을 반환
    }
    
    ----------------------------------
    
    Fruit get(int i) {
    		return (Fruit) list.get(i); 
    }
    ```
    
    - List의 get() 의 경우 Object 타입을 반환하므로 형변환이 필요하다.
    - 따라서 형변환을 추가해준다.
    - 와일드 카드 가 포함된 경우 역시 적절한 형변환과정을 추가한다.

---

- 참고
    - 남궁성 - 자바의 정석
    - [https://docs.oracle.com/javase/tutorial/java/generics/bounded.html](https://docs.oracle.com/javase/tutorial/java/generics/bounded.html)
    - [https://vvshinevv.tistory.com/54](https://vvshinevv.tistory.com/54)
    - [https://devfunny.tistory.com/563](https://devfunny.tistory.com/563)
    - [https://blog.hexabrain.net/379](https://blog.hexabrain.net/379)