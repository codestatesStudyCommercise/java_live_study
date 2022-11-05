---
<br>

# 클래스패스 (classpath)

<br><br>

## ✅ 클래스패스
<br>
(.class) 클래스를 찾기 위한 경로
<br>

JVM이 프로그램을 실행 할 때 바이트코드로 된 파일(.class)을 찾는데 경로를 의미함.

Java runtime(java or jre)으로 .classs 파일에 포함된 명령어를 실행하기 위해 먼저 이 파일을 찾아야한다. 

<br>

### **⏺** classpath를 지정하는 방법

- 환경변수 CLATHPATH를 사용
- java runtime에 `-classpath` 옵션 사영

<br><br>

## **✅ CLASSPATH 환경변수**

운영체제에 지정하는 변수

- 자바 가상머신과 같은 애플리케이션들이 환경변수 값을 참고해서 동작한다.
- 자바는 클래스 패스로 환경변수 CLASSPATH를 사용함
- 환경변수 CLASSPATH 사용 → 실행할 때 classpath옵션을 사용하지 않아도 됨.
- 운영체제 변경시 클래스 패스가 사라지기 떄문에 이식성 면에서 불리할 수 있다.

<br>

### **⏺** classpath를 <환경변수를 통해> 지정하는 이유 (WHY)

프로젝트는 굉장히 복잡한 구조로 여러 경로가 존재하고, 많은 클래스파일을 사용하다보면, 매번 컴파일 할때마다 클래스패스를 명시하는게 번거로운 일이 된다. 

이러한 이유로 운영체제 상에서 CLASSPATH 환경변수로서 설정한다. 

<br>

**Windows → 시스템설정 > 환경변수**

<br>

![image](https://user-images.githubusercontent.com/48430781/200132918-0c25210e-4261-45fd-b41f-228be5f076ed.png)

<br>

![image](https://user-images.githubusercontent.com/48430781/200132940-69cc52ce-c79d-4565-8951-ee3545a53c16.png)

<br><br>


**IDE의 자동 클래스 패스 설정**

최근엔 운영체제 상의 환경변수로 CLASSPATH를 설정하는 것을 지양, IDE나 빌드 도구를 이용해 설정한다. 


<br><br>

---

<br><br>

## **✅** classpath 옵션

환경변수를 통하지 않고, 컴파일 할 떄 -classpath 옵션을 사용해 설정하는 방법이 있다.

<br>

### **⏺** 컴파일 할 때 option을 이용해 지정하는 이유 (WHY)
다른 클래스(Hello) 에 의존하는 클래스(app)의 파일을 컴파일 하기 위해, 컴파일 명령어와 함께 -classpath 옵션을 지정해서 Hello.class의 경로를 알려주기 위함이다. 

<br>

### **⏺** classpath 옵션 사용방법

```java
javac -classpath classpath경로 파일이름

javac -cp classpath경로 파일이름
```
<br>

### 💻 실습  (우분트 리눅스)

다음 그림과 같은 구조인 두개의 파일을 만들었다.

- App.java는  Hello.java에 종속적이다.

![image](https://user-images.githubusercontent.com/48430781/200132833-e0442551-5b80-4ae9-9c8c-8d7ad009d5e2.png)

```java
//Hello.java
public class Hello {
	public static void hello() {
		System.out.println("Hello World!");
	}
}
```
<br>

```java
//App.java

public class App {
	public static void main(String[] args) {
		Hello.hello();
	}
}
```
<br><br>

**만약 같은 파일 내에 App.java와 [Hello.java](http://Hello.java)를 만들경우 Hello.class까지 자동적으로 만들어져서, classpath를 지정해줄 필요가 없다.** 
<br>
![image](https://user-images.githubusercontent.com/48430781/200132851-e567ab8a-fa62-4d14-bedd-d091139a028a.png)
<br>
![image](https://user-images.githubusercontent.com/48430781/200132857-aae565e4-f23c-4746-abba-3c831a2a9e7f.png)


<br><br>

**만약 같은 경로가 아니고, 다른 경로에 Hello.java가 있으면, 어떻게 될까?**
<br>

일단 javac_classpath/HelloDir에 Hello.java를 만들고 컴파일해 Hello.class도 함께 두었다.

<br>

![image](https://user-images.githubusercontent.com/48430781/200132875-28efa25d-4233-4219-9fd8-2f1ab07e1a83.png)

<br>

그리고 javac_classpath/AppDir 에 App.java를 만들었다. 

결과는 직접 그린 그림으로 대체!
<br>

![image](https://user-images.githubusercontent.com/48430781/200132890-55c75d1a-6cc8-45de-a90f-c90b562cb0fc.png)
<br>
![image](https://user-images.githubusercontent.com/48430781/200132899-787623a8-c617-4974-ab91-484c91a1dea9.png)
<br>
![image](https://user-images.githubusercontent.com/48430781/200132903-607570f1-3e28-420d-a427-ce58408dd70f.png)

 
<br><br>

### **⏺ CLASSPATH vs -classspath**

 CLASSPATH 환경변수와 -classpath 옵션을 동시 진행했을 때 우선순위는 무엇이 더 높을까? 

<br>

A.  -classpath가 더 높게 적용 된다. 


<br><br>
---

<br><br>
### References

[https://gispilot.tistory.com/5](https://gispilot.tistory.com/5)

[https://www.baeldung.com/javac-compile-classes-directory](https://www.baeldung.com/javac-compile-classes-directory)

[https://doozi0316.tistory.com/entry/JAVA-7주차-패키지-package-import-classpath](https://doozi0316.tistory.com/entry/JAVA-7%EC%A3%BC%EC%B0%A8-%ED%8C%A8%ED%82%A4%EC%A7%80-package-import-classpath)
