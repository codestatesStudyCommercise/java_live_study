## **✅ 제네릭 (Generics)**
<br>

**다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시 타입체크를 해주는 기능**

<br>

- 자바5에서 추가
- 잘못된 타입이 사용될 수 있는 문제를 컴파일 과정에서 제거 가능
- 타입 변환을 제거함
- 상속이 가능하다.
- 기본 타입은 사용불가함.

<br>

### **⏺ 제네릭의 장점 (사용하는 이유 WHY)**

- **타입안전성을 제공**함
    - 타입안전성이란1) **의도하지 않은 타입의 객체를 저장하는 문제를 막음**2) 저장된 객체를 꺼낼 때 형변환되어 발생할 수 있는 오류를 줄임 → **타입변환이 발생하지 않게 도와줌**
    - **객체의 타입을 컴파일시 체크하기 때문이다.**
    - **컴파일 타임에 타입의 안정성을 보장받는것이 가능함.**
- 타입체크, 형변환을 생략할 수 있어서 **코드가 간결**해짐

---

<br>

## **✅ 제네릭 사용법**
<br>
### **⏺ 타입변수 < T >**

제네릭 타입 class<T> , interface<T>

클래스나 인터페이스 뒤에 <>부호를 붙히고, 사이에 타입파라미터가 위치한다.

- 일반적으로 타입변수는 대문자 알파벳 한글자로 표현하고, 반드시 T를 사용하지는 않는다.

  <br>
  
```java
public class 클래스명 <T> { }
public interface 인터페이스명 <T> { }
```
  
  <br>
  

**명명규칙 (가독성을 위함!)**

| 타입 | 의미 |
| --- | --- |
| T | Type |
| E | Element |
| N | Number |
| K | Key |
| V | Value |
| S, U, V … | 2nd, 3rd, 4th types |
  
<br><br>
  
### **⏺ 타입변수에 실제 타입 지정**

객체 생성시 실제 타입을 대입해 지정해준다.

  <br>
  
```java
ArrayList<Tv> tvList =new ArrayList<Tv> ();

public class ArrayList<E>extends AbstractList<E>{
  private transieont E[] elementData;
  public boolean add(E o){ /*생략*/ }
  public Eget(int index){ /*생략*/ }
}
```
  <br><br>
  

### **⏺ 멀티 타입**
<br>
  
**제네릭 타입이 두개 이상인 경우 컴마구분자(,) 로 나열해 사용**
  
<br>
  
```java
public class Product <T,M>{
  private T kind;
  private M model;

  public TgetKind() {returnthis.kind;}
  public MgetModel() {returnthis.model;}
  
  public void setKind(T kind){
    this.kind = kind;
  }
  public void setModel(M model){
    this.model = model;
  }
}
```
<br>
  
### **⏺ 제네릭 타입의 다형성**
<br>
  
**참조변수에 지정해주는 제네릭 타입과  생성자에 지정해주는 제네릭 타입이 일치해야한다.**

  <br>
  
```java
ArrayList<Tv>      list1 =new ArrayList<Tv>();  // 가능
ArrayList<Product> list2 =new ArrayList<Tv>();  // 에러

classProduct {}
classTvextendsProduct {}
```
  
<br>
  
**클래스 타입간 다형성 적용은 가능하다.**
  
<br>
```java
List <Tv> list1 =new ArrayList<Tv>();  // 가능
List <Tv> list2 =new LinkedList<Tv>();  // 가능
```
  
<br>
  
**Product의 자손 객체만 저장하고 싶다면, Product로 제네릭타입을 생성하고, 자손(Tv...) 객체를 저장하면 된다.**

  <br>
  
```java
ArrayList<Product> list =new ArrayList<Product>();
list.add(new Product());
list.add(new Tv());
```
<br>
  
**⏺ Iterator<E>**

**iterator에도 제네릭이 적용되어 있다.**

**제네릭이 도입되면서 이터레이터(반복자)를 적용해 해당 타입의 next()값을 가져올 수 있는것임 !**

```java
public interface Iterator<E>{
	boolean hasNext();
  E next();
	void remove();
} 
```

<br><br>
---
<br><br>
## **✅ 제네릭 주요개념 (바운디드 타입, 와일드카드)**

### 

### **⏺ Bounded Type Parameters (제한된 제네릭 클래스)**
<br>
  
**💻 정수, 실수 관계없이 숫자만 사용하도록 제한**

  <br>
  
```java
public class GenericClass<T extends Number> {
  private T value;

  public GenericClass(T value) {
    this.value = value;
  }

  public TgetValue() {
    return value;
  }
}
```

→  String은 Number를 상속받은 객체가 아니라서 컴파일 에러 발생

![https://k.kakaocdn.net/dn/cs9ovT/btrQ2ThK3PY/aiXOFOnRATZzGh2cWv1l30/img.png](https://k.kakaocdn.net/dn/cs9ovT/btrQ2ThK3PY/aiXOFOnRATZzGh2cWv1l30/img.png)

  <br><br>
  
### **⏺ 와일드 카드 ( ? )**

**어떤 타입도 받을 수 있게 사용하는 것.**

- 제네릭 타입에 다형성을 적용하는 방법이다
- 의미하는 바를 명확히 하기 위한 목적이 있다.

  <br>
  
**상한제한(Upper Bound), 하한제한(Lower Bound), 제한 없음(Unbounded Wildcard) 존재**

  <br>
  
```java
<? extends T> // 상한 제한, T와 그 자손들 만 가능
<?super T>   // 하한 제한 ,T와 그 조상들만 가능
<T>           // 제한 없음   == <? extends Object>
```
<br><br>

- 와일드카드는 상한/하한 둘 다 지정할 수 없다.

<br>
### **1️⃣ 상한 제한 (Upper Bound Wildcard)**
<br>
- **상한 와일드카드를 사용해 변수에 대한 제한을 완화할 수 있다.**
- **ExampleList<Integer> , List<Double> 및 List<Number> 에서 작동하는 메서드를 작성하려고 한다고 가정**
- **List<Number> 는 List<? extends Number>보다 더 제한적이다**
- 왜(WHY)?
    - 전자가 Number 유형과 일치여부를 체크
    - 후자는 Number 유형 또는 그 하위 유형들과 일치여부 체크

<br>
sumOfList : 목록에 있는 숫자의 합계를 반환

```java
public static double sumOfList (List<? extends Number> list) {
  double s = 0.0;
  for (Number n : list){
    s += n.doubleValue();
    return s;
  }
```

<br>

<? extends Number> : Number과 Number의 하위 클래스인, Integer, Double모두 가능하다.

<br>

```java
List<Integer> li = Arrays.asList(1, 2, 3);
System.out.println("sum = " + sumOfList(li));
```

<br>


```java
List<Double> ld = Arrays.asList(1.2, 2.3, 3.5);
System.out.println("sum = " + sumOfList(ld));
```

### **2️⃣ 하한 제한 (Lower Bound Wildcard)**

**특정 유형 또는 해당 유형의 super유형 으로 제한한다.**

- **example** Integer 개체를 목록에 넣는 메서드를 작성한다고 가정
- 유연성을 최대화하려면 메서드가 List<Integer> , List<Number> 및 List<Object>에서 작동하게 해야함.
- 즉, Integer 값 을 보유할 수 있는 타입은 모두 작동할 수 있어야한다.
- **List<Integer> 라는 용어 는 List<? super Integer> 보다 더 제한적이다**
- 왜(WHY)?
    - 전자는 Integer 유형과 일치여부를 체크,
    - 후자는 Integer또는 Integer의 상위 유형들과  일치여부를 체크

```java
public static void addNumbers(List<? super Integer> list) {
for (int i = 1; i <= 10; i++) {
        list.add(i);
    }
}
```

### **3️⃣ 제한 없음(Unbounded Wildcard)**

**unbounded wildcard가 유용한 경**

- **Object 클래스 에서 제공하는 기능을 사용하여 구현할 수 있는 메서드를 작성**하는 경우
- 코드가 형식 매개변수에 의존하지 않는 제네릭 클래스의 메서드를 사용하는 경우.
    - ex : List.size, List.clear
- Class<?>는 ::: Class<T> 에 있는 대부분의 메서드가 T 에 의존하지 않을 때 자주 사용된다.

printList 메소드 :   **any type의 List를 출력하는 것**이 **목표**라고 하자.

근데 아래 코드는 **Object 인스턴스만 출력할 수 있다**. (**목표 달성 실패!**)

→  List<Integer>, List<String>, List<Double>은 불가능

**WHY ?** ::   **List<Object>의 subtype이 아니기 때문이다.**이런 경우에 **List<?>를 써야한다.**

```java
public static void printList(List<Object> list) {
	for (Object elem : list){
		System.out.println(elem + " ");
    System.out.println();
	}
}
```

```java
public static void printList(List<?> list) {
	for (Object elem: list){
		System.out.print(elem + " ");
    System.out.println();
	}
}
```

```java
List<Integer> li = Arrays.asList(1, 2, 3);
List<String>  ls = Arrays.asList("one", "two", "three");
printList(li);
printList(ls);
```

- **List<Object> 와 List<?> 는 같지 않다는 점에 유의할 것.**

<br><br>


### **⏺** **제네릭 타입의 형변환**

- 제네릭타입과 원시타입간의 형변환은 가능하다. (단, 경고가 발생한다.)
- 대입된 타입(파라미터화 된 타입)이 다른 제네릭 타입간의 형변환
    - **대입된 타입이 Object 일지라도 대입된 타입이 다르면 형변환이 불가능하다.**
    
    `Box<**Object**> objBox = null;
    Box<**String**> strBox = null;
    
    objBox = (Box<**Object**>) strBox; // 에러
    strBox = (Box<**String**>) objBox; // 에러
    
    Box<? **extends** **Object**> wBox = **new** Box<**String**>(); // OK`
    
    - Box 를 Box 으로 직접 형변환하는것은 불가능
    - 와일드카드가 포함된 제네릭 타입으로 형변환 하면 가능 (단, 확인되지않은 타입으로 형변환 한다는 경고 발생)
    - 마찬가지로 와일드카드가 사용된 제네릭 타입끼리도 형변환이 가능하다.

<br><br>

**💻 와일드 카드 예시**
<br>

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

<br>

- 우선 Juicer는 제네릭 클래스가 아니다. 또한 makeJuice()는 static 메서드이다.
- FruitBox 로 고정시 FruitBox 과 같은 다른 타입을 매개변수로 대입할 수 없다.
    - 타입이 맞지 않으므로
- 메서드 오버로딩을 통해 만들면 되지 않나 ?
    - 제네릭 타입이 다른것만으로는 오버로딩이 성립하지않는다
        - 제네릭 타입은 컴파일러가 컴파일 할때만 사용하고 제거해버린다.
- 이같은 상황에서 와일드 카드를 도입하여 사용한다.
    - 위의 예시에서 와일드 카드 도입시

<br>

```java
static Juice makeJuice ( FruitBox<? extends Fruit> box) { }
```

<br>

- FruitBox< 모든 종류 Fruit 및 그 이하 클래스> 를 수용 가능하게된다


<br><br>

---

<br><br>

## ✅ Erasure (**삭제, 소거)

제네릭을 사용하면 그 타입은 컴파일 후에 지워지게 된다.

**즉 컴파일 타임에만, 타입에 대한 제약 조건을 적용**하고,

**컴파일러가 타입변수를 실제 유형으로 바꿔버리기 때문에  런타임에는 타입에 대한 정보를 소거해 해당 타입 정보를 알 수 없다.**

<br>

```java
List<String> myList =new ArrayList<String>(); // 코딩 내용
ArrayList myList =new ArrayList(); // 디컴파일 결과

```

<br>

변수명은 동일하지만 제네릭 타입 파라미터는 제거되었다.

<br>

**→   타입 파라미터는 컴파일러에 의해 해석되는 부분이고 자바 가상 머신에서는 해석이 되지 않기 때문이다.** 그래서 제네릭은 런타임에 체크하는 것이 아니라 **컴파일 시에 정합성을 체크**하게 된다.

**→  자바 가상머신은 제네릭을 고려하지 않고 실행된다.  (제네릭이 제거된 기본 클래스형으로만 처리)**

**→  가상머신상에서 제네릭 코드를 제거하는 이유는**

**제네릭을 해석하기 위해 추가적인 자원 소모를 없애고,  빠르고 명확하게 동작하도록 하기 위해서 사용한다.**

<br>

### **⏺ 제네릭 타입 제거**

**1) T를  실제 타입 파라미터 / Object로 바꾼다.**

**2)** 타입 안전성 보존을 위해 필요시 **type casting**을 넣는다.

- 확장된 제네릭 타입에서 다형성 보존을 위해 **3) bridge method**를 생성한다.

1-1 ) 컴파일러가 <E>는 **unbouned**이기 때문에 **E를 Object로 바꿔준다.**

```java
public class Stack<E> {
private E[] stackContent;

public Stack(int capacity) {
this.stackContent = (E[])new Object[capacity];
    }

public void push(E data) {
        // ..
    }

public E pop() {
        // ..
    }
}

```

```java
public class Stack {
	private Object[] stackContent;

	public Stack(int capacity) {
		this.stackContent = (Object[])new Object[capacity];
	}

	public void push(Object data) {
        // ..
	}

	public Object pop() {
        // ..
  }
}

```

1-2) 만약 **bound** 되었다면

**제네릭 타입의 경계(bound)를 제거**한다.

**첫번째로 바운드된 클래스 (예제 코드에선 Comparable이다.) 로 바꾼다.**

```java
public class BoundStack<E extends Comparable<E>> {
	private E[] stackContent;

	public BoundStack(int capacity) {
		this.stackContent = (E[])new Object[capacity];
  }

	public void push(E data) {
        // ..
  }

	public E pop() {
	       // ..
  }
}

```

```java
public class BoundStack {
	private Comparable [] stackContent;

	publicBoundStack(int capacity) {
		this.stackContent = (Comparable[])new Object[capacity];
  }

	public void push(Comparable data) {
        // ..
  }

	public Comparable pop() {
        // ..
  }
}

```

2)  제네릭 타입을 제거한 후 **타입이 일치하지 않으면 형변환을** **추가**한다.

- List의 get() 의 경우 Object 타입을 반환하므로 형변환이 필요하다.
- 따라서 형변환을 추가해준다.
- 와일드 카드 가 포함된 경우 역시 적절한 형변환과정을 추가한다.

```java
T get(int i) {
  return list.get(i); // list 의 get() 은 Object 형을 반환
}

----------------------------------

Fruit get(int i) {
  return (Fruit) list.get(i);
}

```

**3) 브릿지 메서드**

- 매개변수화된 클래스를 확장하거나, 메소드 서명이 약간 다르거나,모호할 수 있는 매개변수화된 인터페이스를 구현하는 클래스 또는 인터페이스를 컴파일하는 동안Java 컴파일러에 의해 생성된 합성 메소드
- 메서드의 매개변수나 리턴타입을 소거하기 위해서 만들어지는 메서드

```java
public class SomeList extends ArrayList<String> {
  @Override
public booleanadd(String e) {
      //...
  }
}
void Test() {
  ArrayList<String> list =new SomeList();
  list.add("string");
}

```

- ArrayList의 타입소거된 add() 메서드를 호출할 경우 SomeList에는 add(Object e) 메서드가 존재하지 않기 때문에 이를 위해 브릿지 메서드를 생성한다.

<br> <br>

### **+ 다이아몬드 연산자 (자바 7)**

<br>

객체 선언부에 <> 를 기술하면 **변수 선언 시에 사용한 제네릭 타입이 그대로 적용 됨**

```java
Map<String, List<String>> myMap =new HashMap<>();

```

<br>

**다이아몬드 연산자는 오직 객체를 생성하는 부분에서만 사용할 수 있다.**

**아래는 컴파일러가 제네릭의 타입을 추정할 때 변수에 선언해 놓은 파라미터를 바탕으로 추정하기 때문에 컴파일 에러 발생**

```java
Map<> myMap =new HashMap<String, List<String>>(); // 컴파일 에러 발생
```

<br>

(자바 10) 변수를 선언 시 특정 클래스 지정안하고, 타입추론 가능하게 **var** 사용가능

```java
var myMap =new HashMap<String, List<String>>();

```
