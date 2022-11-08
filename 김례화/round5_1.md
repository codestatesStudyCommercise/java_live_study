> 오버로딩(Over loading) : 기존에 없는 새로운 메서드 추가 (new)
오버라이딩(Overriding) : 조상으로부터 상속받은 메서드 내용 변경 (change, modify) 
	= 부모 클래스로부터 상속받은 메서드를 자식 클래스에서 재정의

```java
                        class Parent {
                            void parentMethod() {}
                        }

                        class Child extends Parent {
                            void parentMethod() {} //오버라이딩
                            void parentMethod(int i) {} //오버로딩

                            void childMethod() {}
                            void childMethod(int i) {} //오버로딩
                        }
```
![](https://velog.velcdn.com/images/bokimy/post/b6e3c645-ce82-4ffc-9557-2a766d82a75d/image.png)

---
## 🟪 오버로딩 (Over loading)
	= " 메서드 오버로딩 "
    한 클래스 내에서 같은 이름의 메서드를 여러 개 정의하는 것
    
    overloading : 과적하다
메서드도 변수와 마찬가지로 같은 클래스 내에서 서로 구별되어야 하기 때문에 각기 다른 이름을 가져야 한다. 그러나 자바에서는 한 클래스 내에 사용하려던 이름과 같은 메서드가 존재한다 하더라도 매개변수의 갯수나 타입이 다르면, 같은 이름을 사용할 수 있다.

### 👉🏻 오버로딩의 조건 
> 1) 메서드의 이름이 같아야 한다.
2) 매개변수의 개수나 타입이 달라야 한다.

=> 조건을 만족하지 못할 시 메서드 중복 정의로 간주되어 컴파일 에러가 발생한다.
=> 오버로딩된 메서드는 매개변수에 의해서만 구별되므로 **반환 타입은 오버로딩을 구현하는 데에 아무런 영향을 주지 못한다.**

### 👉🏻 대표적인 예
> println() 메서드

우리는 지금까지 println()에 값만 지정해주면 자연스럽게 출력되기 때문에 크게 의문을 갖지 않았을 것이다.
그러나 **실제로는 println()을 호출할 때 매개변수로 지정하는 값의 타입에 따라 호출되는 println() 메서드가 달라진다.**
우리가 println을 어떤 타입이던 쉽게 쓸 수 있었던 이유는 
자바에서는 PrintStream 클래스에 어떤 종류의 매개변수를 지정하더라도 출력할 수 있도록 **10개의 오버로딩된 println() 메서드**를 정의해놨기 때문이다.

```java
                          void println()
                          void println(boolean x)
                          void println(char x)
                          void println(char[] x)
                          void println(double x)
                          void println(float x)
                          void println(int x)
                          void println(long x)
                          void println(Object x)
                          void println(String x)
```
=> 우리가 println() 메서드를 호출하면 매개변수로 넘어가는 값의 타입에 따라 오버로딩된 메서드들 중 하나가 실행되는 것이다.


### 👉🏻 예시

1) **오버로딩 ❌**
```java
int add(int a, int b) { return a + b; }
int add(int x, int y) { return x + y; }
```
매개변수의 이름만 다를 뿐 타입은 일치하기 때문에 사실상 같은 메서드이다.
컴파일 시 ``'add(int,int) is already defined'`` 라는 에러 메세지가 뜬다.

2) **오버로딩 ❌**
```java
int add(int a, int b) { return a+b; }
long add(int a, int b) {return (long)(a + b); }
```
리턴 타입만 다른 경우이다. 
매개변수의 타입과 개수가 일치하기 때문에 add(2,2)와 같이 호출하였을 때 어떤 메서드가 호출된 것인지 결정할 수 없다.
이 경우도 컴파일 시, ``'add(int,int) is already defined'`` 라는 에러 메세지가 뜬다.

3) **오버로딩 ⭕️**
```java
long add(int a, long b) {return a + b; }
long add(long a, int b) {return a + b; }
```
매개변수의 타입이 순서에 따라 달라지는 경우이다.
이 경우에는 호출 시에 매개변수 값에 따라 호출될 메서드가 구분되므로 중복 메서드 정의가 아닌, 오버로딩으로 간주한다.
ex) add(3, 3L) != add(3L, 3)
그러나 add(3,3)과 같이 호출하였을 경우에는 메서드를 결정할 수 없기 때문에 컴파일 에러가 발생한다.

4) **오버로딩 ⭕️**
```java
int add(int a, int b) { return a + b; }
long add(long a, long b) { return a + b; }
long add(int[] a) {    //배열의 모든 요소 합 리턴
	long result = 0;
    for(int i = 0; i < a.length; i++) {
    	result += a[i];
    }
    return result;
}
```
=> **같은 일을 하지만 매개변수를 달리 해야 할 경우, 매개변수를 다르게 하여 오버로딩을 한다.**

---
## 🟪 오버라이딩(Overriding)
	override : 덮어쓰다.
    조상 클래스로부터 상속받은 메서드의 내용을 변경하는 것.

#### 👉🏻 언제 쓰나?
상속받은 메서드를 그대로 사용하기도 하지만, 자손 클래스에 맞게 변경해야 하는 경우가 많은데 이럴 때 쓴다.

```java
class Point { //2차원 좌표 나타내기 위한 클래스 (인수2개필요)
	int x;
    int y;
    
    String getLocation() {
    	return "x :" + x + ",y: " + y;
    }
}
class Point3D extends Point { //3차원 좌표 표현하기 위한 클래스(인수3개필요)
	int z;
    
    String getLocation() { //오버라이딩
    	return "x :" + x + ",y: " + y + ",z: " + z;
    }
}
```
위의 예시는 자식 클래스는 3개의 값을 리턴해야 하는데 부모 클래스는 2개만 리턴하고 있으므로 자식 클래스에 맞춰 오버라이딩 하여 리턴한다.

### 👉🏻 오버라이딩 조건


> 자손 클래스에서 오버라이딩 하는 메서드는 조상 클래스의 메서드와
1) 이름이 일치해야 한다.
2) 매개변수가 일치해야 한다.
3) 반환 타입이 같아야 한다.

**오버라이딩은 메서드의 내용만을 새롭게 작성하는 것이므로 메서드의 선언부는 부모의 것과 완전히 일치해야 한다.**


➕
> 조상 클래스의 메서드를 자손 클래스에서 오버라이딩 할 때
1) 접근 제어자를 조상 클래스의 메서드보다 좁은 범위로 변경할 수 없다.
2) 예외는 조상 클래스의 메서드보다 많이 선언할 수 없다.
3) 인스턴스메서드를 static메서드로 혹은 그 반대로 변경할 수 없다.

---
cf) 
자바의 정석 - 남궁 성
이미지 출처)
https://hyoje420.tistory.com/14
