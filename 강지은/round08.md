# **✅ 인터페이스 레퍼런스를 통해 구현체를 사용하는 방법**

인터페이스 레퍼런스를 통해 구현체를 사용한다는 의미

```java
interface Player {
   public void introduction(String name);
}
```

```java
public class MyPlayer implements Player {
   @Override
   public void introduction(String name) {
      System.out.println("Hello my name is "+name);
   }
}
```

```java
public class DevAndy {
   MyPlayer player = new MyPlayer();
   player.introduction("Andy");

   Player player02 = player;
   player02.introduction("Steve Jobs");
}
```

Hello my name is Andy

Hello my name is Steve Jobs

**인터페이스인 Player의 인스턴스 player02를 선언하면서 참조변수로 인터페이스 구현체인 MyPlayer의 인스턴스를 참조했다.**

**즉   인터페이스 레퍼런스를 통한 구현체  (player02)**는

**인터페이스 구현클래스(MyPlayer : player)**로 타입 변환이 가능하다는 뜻인듯

---

## **⏺ 인터페이스 상속을 통한 상,하위 인터페이스 존재시**

**→ 하위 인터페이스로 타입 변환하면 상,하위 구현 메소드 모두 사용 가능**

**→ 상위 인터페이스로 타입이 변환되면 상위 인터페이스에 선언된 메소드만 사용 가능**

### **또 다른 예제**

인터페이스 타입으로 객체를 생성할 수 있다.

해당 객체에 구현 클래스로 인스턴스화 할 수 없다.

![https://blog.kakaocdn.net/dn/BhZ4J/btrQK7WBW2n/SbcGkxK4jUxVpihQk5Mjkk/img.png](https://blog.kakaocdn.net/dn/BhZ4J/btrQK7WBW2n/SbcGkxK4jUxVpihQk5Mjkk/img.png)

study는 인터페이스타입이고, 객체 study를 생성했지만, 인스턴스화 된것은 아니기 때문에

say() 구현클래스 메서드 사용 불가한 듯

---

# **✅ 인터페이스 상속**

**인터페이스 사이에서도 상속을 쓸 수 있다.**

- **extends** 키워드 사용
- 하위 인터페이스는, **상위 인터페이스의 메서드를 모두 구현**해야한다.
- 인터페이스는 **다중 상속이 가능**하다
- **구현 코드의 상속이 아니기 때문에 타입 상속**이라고 한다.
- 

```java
public interface 하위인터페이스 extends 상위인터페이스1{

}
```

**하위 인터페이스를 구현하는 클래스는**

**하위인터페이스의 메소드 ~ 상위 인터페이스까지의 모든 추상 메소드에 대해**

**실제 메소드를 갖고 있어야 한다.**

**→ 구현 클래스로부터 객체 생성 후 다음과 같이 하위/상위 인터페이스 타입으로 변환이 가능함.**

```java
하위인터페이스 변수 = new 구현클래스(...);
상위인터페이스1 변수 = new 구현클래스(...);
상위인터페이스2 변수 = new  구현클래스(...);
```

## **✔ 빠른 이해 돕기**

### **(인터페이스 상속에 대하여)**

**stack overflow 중...**

<aside>
💡 **"A를 구현하지 않고 B를 구현하지 않으려면 B가 A를 확장하도록 만들 수 있습니다. "**

</aside>

**개가 아니어도 생명체가 되는 것은 가능**

**하지만, 생명체가 되지 않고 개가 되는것은 불가능함**

→ **짖을 수 있다면, 먹을수도 있지만, 먹을수 있다고 짖을 수 있는것은 아님**

<br>

위의 예시를 보면, 인터페이스 상속에 대해 다음 3가지를 생각해볼 수 있다. 

1) **interface는 형용사적(사물의 형태나 성질)인 의미를 갖고있는 것**임을 기억하자. 
즉 성질/특징으로 묶어줄 때 사용하고 구현체가 아니다.

**추상적인 특징을 이야기하는 메서드만 존재할 뿐이다.**

2)  하위 인터페이스 : A,    상위인터페이스 : B 라고 했을 때

**인터페이스 상속은 A가 되면 당연히 B도 된다는 의미**

3) 객체의 상속에서도 IS-A 관계는 성립했다.

 이건 명제에 있어 필요조건과 충분 조건의 관계로 나타낼 수 있다.

 A → B가 참(True)일 때, **명제 B가 참이 되기 위해 명제 A가 참일 필요가 있음**  

즉 A는 B가 성립하기 위한 필요조건이다. 

대우도 true ((~B → ~A)) :

직접 인터페이스 상속을 사용하는 예를 생각해보자.

((under water))**<물에서 살지 않는> <물에서 사는>** 두 성질이 있고,

**<발로 걸어다니는> <날개로 하늘을 나는> <헤엄치는>** 세개의 성질이 있다고 가정하자

 **<발로 걸어다니는>**특징을 가졌다면, **<물에서 살지 않는>**게 자연스럽다.                ⭕

**<날개로 하늘을 나는>**특징을 가졌다면, **<물에서 살지 않는>**게 자연스럽다.             ⭕

그러나 **<물에서 살지 않는>**다고 해서 무조건 **<날개로 하늘을 나는>** 것은 아니다.    ❌

이걸 interface로 구현해보면,

```java
public class interface_extends{

    public static void main(String args[]){
      Person p = new Person("jieun",24);
        System.out.println(p.name);
        System.out.println(p.age);
        System.out.println(p.getClass()+ "는 "+ p.where()+"에 삽니다.");
        System.out.println(p.getClass()+"의 다리 개수는 : "+p.getNumberOfLeg());
    }
}

interface LiveInWater{
   String where();
}
interface NotLiveInWater{
   String where();
}

interface Swim extends LiveInWater{
   boolean isMammalia();
}
interface Walk extends NotLiveInWater{
   int getNumberOfLeg();

}
interface Fly extends NotLiveInWater{
   int getSpeed();
}

class Person implements Walk{
   String name;
    int age;

    Person(String name, int age){
        this.name = name;
        this.age = age;
    }

   @Override
   public String where(){
      return "Land";
   }
   @Override
   public int getNumberOfLeg(){
      return 2;
   }

}
```

![https://blog.kakaocdn.net/dn/c0mwiA/btrQJvoGuOa/iKobc24q1FHNUKRt1JaCuk/img.png](https://blog.kakaocdn.net/dn/c0mwiA/btrQJvoGuOa/iKobc24q1FHNUKRt1JaCuk/img.png)

만약 하위인터페이스나 상위 인터페이스의 추상메서드가 구현이 한개라도 안되면 다음과 같은 에러가 난다.

. compiler.java:8: error: cannot find symbol        System.out.println(p.getClass()+ "? "+ p.where()+"? ?

??.");                                                ^  symbol:   method where()  location: variable p of type Personcompiler.java:32: error: Person is not abstract and does not override abstract method where() in NotLiveInWaterclass Person implements Walk{^2 errors

// Person은 추상이 아니며 NotLiveInWater의 추상 메서드 where()를 재정의하지 않습니다.

---

## **⏺ 왜 인터페이스가 인터페이스를 상속하는 구조를 사용할 까? (WHY)**

### **Q. 둘의 차이는 무엇일까? 실제로 코드상에선 아무런 차이가 없어보인다.**

```java
interface A{
    public void method1();
}
interface B extends A{
    public void method2();
}
class C implements B{
    @Override public void method1(){}
    @Override public void method2(){}
}
```

```java
interface A{
    public void method1();
}
interface B{
    public void method2();
}
class C implements A, B{
    @Override public void method1(){}
    @Override public void method2(){}
}
```

### **A.  한 가지 큰 차이점이 있다.**

첫 번째 예시는  인터페이스 B가 A를 extends (확장) 하기 때문에

앞으로 B를 구현하는 모든 클래스는 A를 자동으로 구현한다.

→ 컴파일러에게   "A가 된다는 것" 은  B가 된다는 뜻으로 알려주는것.    **" 모든 B는 A이다** !"

그런데 아래 코드를 보자.

```
class C implements B {
    ... you implement all of the methods you need...
    ...blah...
    ...blah...
}
A myNewA = new C();
```

두 번째 예에서는 A와 B의 관계가 없어서   위의 코드가 동작하지 않는다.

C가 B를 구현했는데, A 참조변수에 C인스턴스를 할당하려고 하면,

모든 B는 A이다! 라고 컴파일러에게 말하지 않았기 때문이다.

### **추가이해를 돕는 예제**

**1번코드**

```java
class ChevyVolt implements Vehicle, Drivable {}
class FordEscort implements Vehicle, Drivable {}
class ToyotaPrius implements Vehicle, Drivable {}
```

**2번코드**

```java
class ChevyVolt implements Vehicle {}
class FordEscort implements Vehicle {}
class ToyotaPrius implements Vehicle {}
```

```java
interface Vehicle extends Drivable {}
```

위의 예제를 A, B, C에 대입하면

Drivable  ==  A

Vehicle   ==  B

class ChevyVolt     == C

class FordEscort    == C

class ToyotaPrius   == C

```java
A myNewA = new C();//여기에 대입하면, (상속 없이는 안되는 코드 )
Drivable  Toyota  = new ToyotaPrius();// 가 불가능하게된다.//Vehicle   Toyota  = new ToyotaPrius();  얘는 가능함  ..
```

(Vehicle) 탈것이라면 당연히 (Drivable)운전할 수있다는 참인 명제를

**1번코드**처럼 

상속 관계를 안 넣어주고, 둘다 구현 클래스에 implement해주면 

자동차는 탈것을 구현했지만  운전할수있다는 성질로 묶어줄 수 없어지는 것...

참인 명제에서 오류가 생긴다. 

---

# **✅ 인터페이스 다중 상속**

```java
public interface 하위인터페이스 extends 상위인터페이스1, 상위인터페이스2 {...}
```

상위 인터페이스에 있는 메서드 중

메서드명/파라미터 형식이 같지만 리턴타입이 다른 메서드가 있다면,

**둘중 어떤 것을 상속받느냐에 따라 규칙이 달라져 다중 상속이 불가능하다.**

![https://blog.kakaocdn.net/dn/ct9ZJ2/btrQK0pEcJX/Mf3CX3I7221kthz7ttpYUK/img.png](https://blog.kakaocdn.net/dn/ct9ZJ2/btrQK0pEcJX/Mf3CX3I7221kthz7ttpYUK/img.png)

## **⏺ 두개 인터페이스를 구현시, 메소드 시그니쳐가 같은 케이스에서는 어떻게 해야하는지?**

**중복되는 인터페이스의 추상 메소드를 재정의** 하여 사용할수 있음

> 보니까 default만 문제가 생기는 것 같음

default 메서드는 인터페이스에 구현되고, 구현클래스에서 오버라이딩이 가능한(필수x) 유일한 메서드라서...!

>>  기본 메서드는 어차피 구현클래스에서 오버라이딩을 필수로 해줘야 하기 때문에 메서드 시그니처가 같아도 오버라이딩된 메서드만 호출해 사용하는 것 같다.
> 

### **예제**

→    preJoin 메소드를 재정의 하지 않으면 컴파일 에러가 발생

→  **".super.메소드"  사용**

```java
public interface JoinMember {

    default void preJoin(){
        System.out.println("pre member");
    }
}
```

```java
public interface JoinGroup {

     default void preJoin(){
        System.out.println("pre group");
    }
}
```

```java
public class Member implements JoinMember, JoinGroup{

    @Override
    public void preJoin() {
        JoinMember.super.preJoin();
        JoinGroup.super.preJoin();
    }
}
```

**+ static 메소드면 어떻게 할까?**

**애초에 override가 안되기 때문에**

인터페이스이름.preJoin(); 으로 사용할 수 밖에 없음.
