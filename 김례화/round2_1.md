
[Java] Array vs ArrayList
ArrayList
Java
array
리스트
배열
코딩
태그를 입력하세요

H1

H2

H3

H4







    👉🏻 배열 추가 : **grow()**
    ```java
            cars.grow();
    ```
    
    
- ArrayList에서의 정렬 
    java.util 패키지 Collections 클래스의 sort() 메서드를 사용하면 배열 내 요소들이 자동으로 정렬된다.
    ```java
      import java.util.Collections;
        //...
          ArrayList<String> cars = new ArrayList<String>();
          cars.add("Volvo");
          cars.add("BMW");
          cars.add("Ford");
          cars.add("Mazda");
          Collections.sort(cars);  // Sort cars
        //...
        
    //출력 결과
    //BMW
    //Ford
    //Mazda
    //Volvo
    ```
    
### 🟪 내부 동작
In Heap
   
   ![](https://velog.velcdn.com/images/bokimy/post/ab6c96a0-d486-4c38-b773-1e97624f2d6b/image.png)
​
#### 원리
element를 add() 하려고 할 때, capacity가 elementData(기존 배열)의 길이와 같아지면 일반적으로 ``기존의 용량 + 기존의 용량/2`` 즉, ``1.5배`` 만큼 크기가 늘어난 배열에 기존 elementData를 copy한다. 
**즉,**
grow() 메서드로 용량을 늘린 뒤, 추가하려는 element를 할당하면 클라이언트 입장에서는 자동으로 사이즈를 늘려주면서 element가 추가된 것으로 보인다.
**실제로는,**
가지고 있던 용량이 꽉 찼을 때, 용량을 늘린 새로운 배열을 copy하는 것이다.
기존의 배열은 삭제된다.
​
​
### 🟪 메모리 영역
    Object를 가리키는 변수(주소값)만 Stack에 쌓이고, Object 자체는 Heap에 할당되어 참조하는 형태

나가기
임시저장수정하기
[Java] Array vs ArrayList
ArrayList
자바 컬렉션 프레임워크의 일종.
클래스.
발전된 형태의 배열.
일반적으로 배열을 선언하면 배열의 인덱스를 다 채워서 더이상 못채우거나 인덱스를 못채울 수 있는데 이런 경우 메모리가 낭비되는 현상이 일어난다.
-> 이러한 문제를 해결하기 위해 나옴.
java.util 패키지에 존재.
원할 때마다 element를 추가,제거할 수 있다.
👉🏻 항목 추가 : add()
  ArrayList<String> cars = new ArrayList<String>();
      cars.add("Volvo");
👉🏻 항목 엑세스 : get()
		cars.get(0); //0번째 인덱스에 접근
👉🏻 항목 변경 : set()
		cars.set(0, "Opel"); // 0번째 인덱스 "Opel"로 변경
👉🏻 항목 제거 : remove()
		cars.remove(0); //0번째 인덱스 제거
👉🏻 배열 크기 : size()
		cars.size();
👉🏻 배열 추가 : grow()
		cars.grow();
ArrayList에서의 정렬
java.util 패키지 Collections 클래스의 sort() 메서드를 사용하면 배열 내 요소들이 자동으로 정렬된다.
  import java.util.Collections;
  	//...
      ArrayList<String> cars = new ArrayList<String>();
      cars.add("Volvo");
      cars.add("BMW");
      cars.add("Ford");
      cars.add("Mazda");
      Collections.sort(cars);  // Sort cars
  	//...
    
//출력 결과
//BMW
//Ford
//Mazda
//Volvo
🟪 내부 동작
In Heap



원리
element를 add() 하려고 할 때, capacity가 elementData(기존 배열)의 길이와 같아지면 일반적으로 기존의 용량 + 기존의 용량/2 즉, 1.5배 만큼 크기가 늘어난 배열에 기존 elementData를 copy한다.
즉,
grow() 메서드로 용량을 늘린 뒤, 추가하려는 element를 할당하면 클라이언트 입장에서는 자동으로 사이즈를 늘려주면서 element가 추가된 것으로 보인다.
실제로는,
가지고 있던 용량이 꽉 찼을 때, 용량을 늘린 새로운 배열을 copy하는 것이다.
기존의 배열은 삭제된다.

🟪 메모리 영역
Object를 가리키는 변수(주소값)만 Stack에 쌓이고, Object 자체는 Heap에 할당되어 참조하는 형태
ex)

public class Main {

    public static void main(String[] args) {
    	//...
        List<String> skills = new ArrayList<>();
        skills.add("java");
        skills.add("js");
        skills.add("c++");
		//...
        test(skills);

    }
}
1) ArrayList skills가 값이 채워지지 않고 생성만 됐을 때

List<String> skills = new ArrayList<>();


ArrayList Skills의 list가 생성만 된 상태

2) 값 add()

skills.add("java");
skills.add("js");
skills.add("c++");


차이점


Array
배열
크기가 고정되어있다.
primitive type(int,byte,char etc.)과 object를 모두 담을 수 있다.
제네릭을 사용할 수 없다.
길이에 대한 배열 : length 변수 사용.
element들을 할당하기 위해 assignment(할당)연산자 써야 한다.
자바 내장 배열
ArrayList
발전된 형태의 배열
사이즈가 동적인 배열.
Object element만 담을 수 있다.
primitive type을 사용하려면 래퍼 클래스가 필요하다.
jvm은 Autoboxing을 통해 ArrayList에 Object만 저장되도록 한다.
cf)
Autoboxing
내부적으로 primitive type을 타입에 상응하는 Object로 변환시켜주는 것 
ex: int -> Integer

Wrapper Class (래퍼 클래스)
객체가 기본 데이터 유형을 래핑하거나 포함하는 클래스.
타입 안정성을 보장해주는 제네릭을 사용할 수 있다.
길이에 대한 배열 : size() 메서드 사용.
element들을 할당하기 위해 add() 메서드를 통해 element를 삽입한다.
java.util 패키지에서 import 해야 사용 가능.
cf)

클래스 간의 관계


1) AbstractList
: 이 클래스는 클래스를 확장하고 get() 및 size() 메서드 만 구현하면 되는 수정 불가능한 목록을 구현하는 데 사용.
2) CopyOnWriteArrayList
: 이 클래스는 목록 인터페이스를 구현. 모든 수정(추가, 설정, 제거 등)이 목록의 새 복사본을 만들어 구현, ArrayList 의 향상된 버전.
3) AbstractSequentialList
: 이 클래스는 Collection 인터페이스 와 AbstractCollection 클래스를 구현. 이 클래스는 AbstractList 클래스를 확장하고 get() 및 size() 메서드만 구현하면 되는 수정 불가능한 목록을 구현하는 데 사용.

cf)


이미지 출처
