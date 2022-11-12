## 🟪 제네릭(Generic)
자바 5부터 사용 가능.
클래스나 메서드의 코드를 작성할 때, 타입을 정해두는 것이 아니라 추후에 지정할 수 있도록 일반화해두는 것.
= 작성한 클래스나 메서드의 코드가 특정 데이터 타입에 얽매이지 않도록 해둔 것.


> **제네릭 클래스 / 제네릭 인터페이스**
선언에 타입 매개변수(type-parameter)가 사용된 클래스 혹은 인터페이스
제네릭 클래스와 제네릭 인터페이스를 통틀어 제네릭 타입(generic type)이라고 한다.

### 🟡 WHY?
제네릭을 지원하기 전에는 컬렉션에서 객체를 꺼낼 때마다 형변환을 해야 했기 때문에 실수로 엉뚱한 타입의 객체를 작성하면 형변환 오류가 났다.
그러나 제네릭을 사용하면 컬렉션이 담을 수 있는 타입을 컴파일러에 알려주기 때문에 컴파일러는 알아서 형변환 코드를 추가할 수 있고, 엉뚱한 타입의 객체를 넣는 실수를 컴파일 과정에서 차단하여 더 안전하고 명확한 프로그램을 만들 수 있다.

### 🟡 사용법
```java
 class Ball<T> {
    private T item; //T를 임의의 타입으로 사용.

    public Ball(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }

    public void setItem(T item) {
        this.item = item;
    }
}
```
#### 👉🏻 Ball 클래스 인스턴스화 하기
```java
Ball<String> ball1 = new Ball<String>("축구공");
```
클래스를 인스턴스화할 때 클래스 이름 뒤에 <String>을 붙인다.
이 말은 "Ball 클래스 내의 T를 String으로 바꿔라"는 뜻입니다.
이렇게 인스턴스화하면 Ball 클래스 내의 T들이 String처럼 취급되어 실행된다.

> 위의 ``T`` : 타입 매개변수
  ``<T>`` : 타입 매개변수 선언, 클래스 이름 옆에 작성한다.
 타입 매개변수는 임의의 문자로 지정할 수 있다.
  T, K, V는 각각 Type, Key, Value의 첫 글자. 
  Element를 뜻하는 E, Number를 뜻하는 N, 그리고 Result를 뜻하는 R도 자주 사용된다.
  
  
#### 타입 매개변수 - 임의의 타입으로 사용
```java
class Ball<T> {
    private T item;

    ...
}
```

  
#### 👉🏻 여러 개의 타입 매개변수 사용
  
```java
class Ball<K, V> { ... }
```

  
---
### 🟡 주의할 점
#### 클래스 변수에는 타입 매개변수를 사용할 수 없다.
  클래스 변수는 모든 인스턴스가 공유하는 변수이다. 
  만약, 클래스 변수에 타입 매개변수를 사용한다면, 클래스 변수의 타입이 인스턴스마다 달라지게 될 것이다.
  때문에 static이 붙은 변수 또는 메서드에는 타입 매개변수를 사용할 수 없다.
#### 타입 매개변수에 치환될 타입으로 기본 타입을 지정할 수 없다.
  때문에 primitive type을 써야할 경우 래퍼 클래스로 써야 한다.
#### 제네릭 클래스의 타입 매개변수와 제네릭 메서드의 타입 매개변수는 별개이다.
   타입이 지정되는 시점이 다르기 때문이다.
  제네릭 클래스의 타입 매개변수는 클래스가 인스턴스화될 때 타입이 지정되지만, 제네릭 메서드의 타입 지정은 메서드가 호출될 때 이루어진다. 
  
  
---
## 🟪 제네릭 메서드
**  클래스 내부에 제네릭으로 선언된 특정 메서드.**
```java
class Ball {
		...
		public <T> void add(T element) {
				... //이 메서드 내부에서만 T 타입 매개변수 사용 가능
		}
}
```
  
### 🟡 특징
  
- 타입 매개변수 선언은 반환타입 앞에서 이루어지며, 해당 메서드 내에서만 해당 타입 매개변수를 사용할 수 있다.

- 메서드 타입 매개변수는 클래스 변수와 달리 static 메서드에서도 선언하여 사용할 수 있다.

- ``String 클래스``의 메서드는 제네릭 메서드를 정의하는 시점에 사용할 수 없다. ( ex : length() )
  제네릭 메서드를 정의하는 시점에서는 실제 어떤 타입이 입력 되는지 알 수 없기 때문이다.
- 그러나 최상위 클래스인 ``Object 클래스의 메서드``는 모든 클래스가 Object 클래스를 상속받기 때문에 사용이 가능하다. (ex: equals(), toString() )
  
---
### 🟡 배열 사용한 코드 with 제네릭
```java
import java.util.Arrays;
import java.util.EmptyStackException;

public class Generic<E>{
    private E[] elements;
    private int size = 0;
    private static final int DEFAULT_INITIAL_CAPACITY = 16;
    
    public Generic() {
        elements = new E[DEFAULT_INITIAL_CAPACITY];
    }
    
    public void push(E e) {
        ensureCapacity();
        elements[size++] = e;
    }
    
    public E pop() {
        if (size == 0)
            throw new EmptyStackException();
        E result = elements[--size];
        elements[size] = null; // 다 쓴 참조 해제하기
        return result;
    }
    
    public boolean isEmpty() {
        return size == 0;
    }
    private void ensureCapacity() {
        if (elements.length == size)
            elements = Arrays.copyOf(elements, 2 * size + 1);
    }
}

```
![](https://velog.velcdn.com/images/bokimy/post/6d93a71b-bd52-45cc-abeb-d6f3dbfd9029/image.png)
제네릭 배열은 컴파일 되지 않는다.
E와 같이 실체화 불가 타입으로는 배열을 생성할 수 없다. 

해결책
1) 제네릭 배열 생성을 금지하는 제약을 대놓고 우회하는 방법.
  => Object 배열 생성 후 제네릭 배열로 형변환하기.
  오류 대신 경고가 뜰 것임. 그러나 타입 안전하지는 않다.
```java
public Generic() {
	elements = (E()) new Object[DEFAULT_INITIAL_CAPACITY];
  }
```
2) elements 필드 타입을 E[] -> Object[] 로 바꾸기





---
cf)
이펙티브 자바 (조슈아 블로크)


