
WhiteShip Java Live Study 의 커리큘럼을 따라 개인적으로 공부한 내용입니다. 
![image](https://user-images.githubusercontent.com/48430781/199002844-e8be4897-4a40-432c-a8d1-f4a3eb4a40ba.png)

<br><br>

# 1주차 : JVM과 자바코드       

<br>

## 목차   
- JVM이란 무엇인가

- 컴파일 하는 방법

- 실행하는 방법

- 바이트코드란 무엇인가

- JIT 컴파일러란 무엇이며 어떻게 동작하는지

- JVM 구성요소

- JDK와 JRE의 차이

<br><br>

------

<br><br>

# JVM이란 무엇인가


<br><br>

## ✅ JVM (Java Virtual Machine) 
운영체제와 자바 바이트코드 사이에서   
자바 바이트코드를 해석해   
모든 운영체제 사이에서 동일하게 동작하도록 하는 가상머신   

<br><br>

OS별로 각각 제공되는 JVM이 자바 바이트 코드를 기계어로 해석해 동작하도록 함

<br>

즉 **자바는 OS에 상관없이 JVM만 설치되어 있으면,**      
**동일한 코드로 동일한 동작** 을 할 수 있다.  

<br><br>

* 기존의 다른 언어 (C,C++)는 운영체제에서 동작하기 때문에 의존적임
<br>

![image](https://user-images.githubusercontent.com/48430781/199007014-cf6b2f50-2e9c-4256-a5d6-35939536e47a.png)


<br>



자바코드와 다양한 OS 사이에서 JVM(Java Virtual Machine)을 통해 동일한 동작을 할 수 있다.
<br><br>

------
<br><br>

# 컴파일 하는 방법
# 실행하는 방법
<br><br>

### ⏺ 애플리케이션 실행 과정

<br>

![image](https://user-images.githubusercontent.com/48430781/199008016-374baceb-22da-4452-bd39-645bc28f4c05.png)


<br>

1) 콘솔에 Hello World!를 출력하는 자바 코드가 있다. 

2) 해당 프로그램을 실행하기 위해 자바 컴파일러가 컴파일이라는 작업을 한다. 

3) .java파일이 컴파일을 거쳐 .class파일로 변경이 되고 이는 바이트 코드가 된다. 

4) 인터프리터가 바이트코드를 해석하며 애플리케이션이 실행된다. 

<br><br>


#### 단어해석

* 컴파일 : 사람이 이해하는 언어를 컴퓨터가 이해할 수 있는 언어로 바꿔주는 과정 (원시코드-> 목적코드)
* 컴파일러 : 번역기/ 해석기 - 고레벨언어를 저레벨언어로 해석해주는 번역 프로그램 ---   javac
* 인터프리터 : 한줄씩 해석해 기계어로 번역 프로그램  


<br><br>


### ⏺ 왜 자바는 컴파일러와 인터프리터를 둘다 가지는가? (WHY)
일반적인 언어는 컴파일러 / 인터프리터 중 한개만 사용해서 번역을 하는데, 왜 자바는 두개의 번역기를 갖고 있는걸까?



- 원래는 자바 JVM에서 인터프리터 방식만 사용했었음

- 성능의 문제가 발생함

- JIT Compiler를 추가해 성능의 효율을 올림


<br><br>


#### 추가 학습

* 링크 : 목적코드를 최종 실행 가능한 실행파일 (.exe)을 만들기 위해 연결하는 작업

* 링커 : 링크를 실행해주는 프로그램


<br><br>




### ⏺  실습

<br><br>

#### 1) 테스트 코드 작성
<br>
##### Hello.java

```java
class Hello{
	public static void main(String[] args){
 		System.out.println("Hello Java 221029");
	}
}
```

<br>

#### 2) .java 파일이 존재하는 곳에서  `javac Hello.java`  명령어 입력

<br>


Hello.class가 생성된 것을 확인할 수 있다.<br>
![image](https://user-images.githubusercontent.com/48430781/199002350-fe2d837c-72f0-44bb-95f4-ae69e93cfe1a.png)

<br>

<Hello.class를 열어봤을 때><br>
![image](https://user-images.githubusercontent.com/48430781/199002323-9c80e3ea-a86f-47f3-b8cc-f30e2f62ba85.png)
<br>
잘된건진 모르겠지만 일단 못알아먹겠다.
<br>




#### 3) javap -c Hello.class  를 입력해서 해석된 바이트 코드를 볼 수 있다. 

![image](https://user-images.githubusercontent.com/48430781/199002260-40c3b294-7eb8-48a5-9f55-543dcf3aa311.png)


<br>



#### 4)  java Hello  를 입력해서 컴파일한 .class를 실행할 수 있다. 

>> Hello Java 221029

<br><br>

------

<br><br>

# 바이트코드란 무엇인가


<br><br>

## ✅ 자바 바이트 코드 (Java Bytecode) 
<br>
JVM이 이해할 수 있는 언어로 변환된 자바 소스코드

자바 컴파일러에 의해 변환된 코드의 명령어 크기가 1byte이기 때문에 바이트코드라고 불린다. 

바이트 코드는 다시 실시간 번역기 / JIT 컴파일러에 의해 바이너리 코드로 변환된다. 

<br>

*바이너리코드 (이진코드) : 컴퓨터가 인식할 수 있는 0과 1로 구성된 이진 코드

<br>

가상머신이 이해하는 코드 : 바이트코드

CPU가 이해하는 코드 : 바이너리코드

<br><br>


------


<br><br>

# JIT 컴파일러란 무엇이며 어떻게 동작하는지

<br><br>

## ✅ JIT 컴파일러
프로그램을 실제 실행하는 시점에 기계어로 변환하는 컴파일러

<br><br>
정의만 봐서는 잘 모르겠으니 아래 내용을 보며 이해해보자.

<br><br>

### ⏺ 왜 JIT 컴파일러를 사용할까? (WHY)


위에서 자바는 컴파일러와 인터프리터를 모두 갖고 있다고 말했다. (이 방식에는 문제가 있었다.)



문제 : 매번 컴파일을 통해 Java파일을 Bytecode(.class)로 변환하고, 다시 인터프리터를 통해 한줄한줄 기계어로 변환하는 작업이 속도면에서 비효율적이다.



해결 : JIT컴파일러를 사용해서 속도를 개선



먼저 JIT컴파일러가 소스코드 전체를 확인 후 중복된 부분을 미리 기계어로 번역시켜서 저장한다.

이후 인터프리터 방식으로 번역하다가 중복된 부분을 만났을 때 이미 변환된 기계어 코드를 재사용하며 속도를 개선했다. 

<br><br>

### JIT 컴파일러를 이용한 자바 실행 과정
![image](https://user-images.githubusercontent.com/48430781/199002171-8da56b8c-1303-4192-a67f-354717d575fd.png)



볼만한 자료 :https://youtu.be/8y0L9QT7U74

<br><br>

**💥 해당 과정을 수행하기 위해 초반에 메모리를 잡아두는 등의 선행 작업들이 있어 초기 실행 속도가 다소 느릴 수 있다. 그 이후 바이트 코드를 사용할 때마다 기계어로의 변환 작업이 덜 들어 속도의 개선이 일어난다. (일반적)**

<br>

**💥 중복된 코드가 거의 없어 코드가 재사용될 일이 없거나, 규모가 작은 프로그램에선 초기 실행 속도에 의해 배보다 배꼽이 더 클 수 있다.**

<br><br>

------

<br><br>


# JVM 구성요소
<br>

![image](https://user-images.githubusercontent.com/48430781/199002070-904f3c4d-48ea-44a2-8a4c-6c1ce1a5c427.png)

<br><br>

## ✅ JVM 구성요소

<br>

#### 1. 클래스 로더 (Class Loader)
#### 2. 실행 엔진 (Execution Engine)
> 인터프리터 (Interpreter)   
> JIT 컴파일러 (Just-in Time Compiler)   
> 가비지 컬렉터 (Garbage Collector)   
#### 3. 런타임 데이터 영역(Runtime Data Area)
> Method Area   
> Heap Area   
> Stack Area   
> PC Register   
> Native Method Stack   



<br><br>

### ⏺ 클래스 로더 (Class Loader)
바이트 코드 .class파일을 런타임시에 동적으로 로드 함

- 읽은 바이트코드를 Runtime Data Area에 배치시키는 역할


<br><br>


### ⏺ 실행 엔진 (Execution Engine)
클래스 로더가 JVM내 Runtime Data Area에 배치시킨 바이트코드를 실행시킨다.



<br>

**1) 인터프리터 (Interpreter)**

바이트 코드를 기계어 코드로 해석해 한줄씩 실행 함


<br>


**2) JIT 컴파일러 (Just-in Time Compiler)**

인터프리터의 느린 실행 속도를 보완하고, 성능을 향상시킨 컴파일러

그 순간 컴파일 되기 때문에 반복되는 코드를 컴파일 해서 사용한다.


<br>


**3) 가비지 컬렉터  (Garbage Collector)**     
- 이름 그대로를 해석하면 쓰레기 수집가..

- 메모리를 자동으로 관리하는 자바 프로그램이다.


- 데몬 스레드에서 항상 백그라운드로 실행된다.

- 기본적으로 Heap영역의 메모리를 JVM이 판단하여,

더이상 사용되지 않는 인스턴스를 찾아 메모리에서 삭제한다.


<br><br>


### ⏺ 런타임 데이터 영역 (Runtime Data Area)

<br>

프로그램을 수행하기 위해,  JVM이OS에서 할당받은 메모리 공간/영역

<br>

![image](https://user-images.githubusercontent.com/48430781/199001935-be7ad2e8-cd88-4798-9d0f-e5b400c7e9cb.png)

<br><br>



**Method Area**
클래스 멤버 변수의 이름, 데이터 타입, 리턴 타입, 상수풀, static 변수 등이 저장   
클래스 수준의 정보가 저장

<br>

**Heap Area**
new 연산자로 생성된 객체, 배열이 저장 됨

<br>

**Stack Area**
스레드가 생성될 때마다 생성되는 영역   
지역변수 저장   
메소드를 호출할 때마다 스택이 개별적으로 생성됨 -> 동시성 문제 해결하기 위해 메소드에 동기화 블럭을 지정 함.

<br>

**PC Registers**
쓰레드가 생성될 때마다 생성되는 영역   
Prigram Counter - 현재 스레드가 실행되는 부분의 주소와 명령을 저장하고 있는 영역

<br>

**Native Method Stack**
자바 프로그램이 실제 실행할 수 있는 기계어로 작성된 프로그램을 실행시키는 영역
자바 언어 이외의 언어로 작성된 코드를 저장하는 메모리영역 
주로 native키워드가 붙은 것들이 저장 됨.

<br><br>

------

<br><br>

# JDK와 JRE의 차이

<br><br>

## ✅ JDK
Java Development Kit  : 자바 개발 키트

자바를 사용하기 위해 필요한 모든 기능을 갖춘 Java용 SDK (Software Development Kit)

* SDK : HW플랫폼, OS, 프로그래밍 언어 제작사가 제공하는 툴

<br>

- JDK는 JRE를 포함하고 있음

- 컴파일러(javac), jdb, javadoc 과 같은 도구들도 있음



⏩ JDK는 프로그램을  생성, 실행, 컴파일  할 수 있다. 

⏩ JRE와 JVM을 모두 포함하는 포괄적 키트

<br><br>

## ✅ JRE
Java Runtime Environment : 자바 런타임 환경

컴파일된 Java 프로그램을 실행하는데 필요한 패키지



- JVM + 자바 클래스 라이브러리 등으로 구성



⏩ 자바프로그램을 실행 가능하게 하는 도구
<br>
⏩ JVM을 포함하고 있음







<br><br><br><br>






References


https://dkswnkk.tistory.com/416
https://kingofbackend.tistory.com/123
https://logical-code.tistory.com/149
https://doozi0316.tistory.com/entry/1%EC%A3%BC%EC%B0%A8-JVM%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%9E%90%EB%B0%94-%EC%BD%94%EB%93%9C%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%8B%A4%ED%96%89%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B8%EA%B0%80
https://moon-seung-chan.tistory.com/45
