<br><br><br><br>

# 리터럴

## **✅ 리터럴 (Literal)**

**문자가 가리키는 값(데이터) 그 자체**

```java
int num;
num = l;
```

**num에 할당하고 있는 1이 리터럴이다.**

```java
float weight = 74.5f;
finallong LIGHT_YEAR = 9460730472580L;

float = 9460730472580.0F;
double = 9460730472580.0D;
```

- **float 타입 변수에 실수형 리터럴을 할당 시 리터럴 뒤에 접미사 f를 붙여야함**
- **long 타입 변수에 정수형 리터럴을 할당 시 리터럴 뒤에 접미사 L을 붙여야함 (소문자도 가능하지만 숫자와 혼동 되어 비추)**

### **⏺ 정수 리터럴**

**byte, short, int, long**

10진수 : 소수점이 없는 정수 리터럴

8진수 : 0으로 시작하는 리터럴

16진수 : 0x / 0X로 시작,   0~9  a~f로 구성된 리터럴

### **⏺ 실수 리터럴**

**float, double**

10진수 실수 : 소수점이 있는 리터럴

10진수 지수와 가수 : E/e가 숫자 뒤에 존재하는 리터럴

### **⏺ 논리 리터럴**

**boolean  (true, false)**

### **⏺ 문자 리터럴**

**char**

작은 따옴표( ' ' )로 묶인 하나의 텍스트

- 자바는 **유니코드**로 문자를 저장함.

char c1 = 'c';와 같이 문자 리터럴을 문자형 변수에 할당하면, c1 에는 영문자 c의 유니코드 숫자 값이 저장 된다.

**이스케이프 문자**

## 

---

# 변수 선언 및 초기화하는 방법

 ****

## **✅ 변수 (Variable)**

- **데이터의 저장과 참조를 위해 할당된 메모리 공간**에 붙인 **이름**
- 메모리 공간의 활용/ 할당 및 접근을 위한 이름
- **변수의 선언 : 메모리 공간의 할당**

<aside>
💡 컴퓨터는 메모리에 데이터를 저장
메모리는 1byte크기의 데이터를 저장할 수 있는 메모리 셀들이 모여서 만들어짐.
각 메모리셀엔 고유 번호가 오른차순으로 적혀있는데, 이 고유번호를 메모리 주소라고 함.

</aside>

### **⏺ 변수를 사용하는 이유 (WHY)**

문제점 1. 저장해야 할 값이 많을 때,  **사람이 메모리주소를 식별하기 어려움**

문제점 2. **시스템 운영에 꼭 필요한 데이터 공간에 실수로 덮어 쓸 가능성**도 존재함.

문제점 3. **추상화되지 않은 코드는 비효율적**임.

**해결 : 변수라는, 사람이 식별 가능한, 값을 저장할 수 있는 메모리 공간을 확보함.**

### **⏺ 선언**

변수를 사용하기 위해 변수를 만들어 줌

변수 선언 방법 : **[변수타입 변수명]**

```java
int num;
```

int - 4byte 메모리공간을 확보, num으로 명명

### **⏺ 할당**

변수에 값을 저장하는 것.

**대입연산자 (=)**  사용

```java
num = 1;
```

num이라는 변수에 1을 할당해라

- **초기화되지 않은 변수**는 **프로그램 안전성을 위해** **사용할 수 없다.**

![https://blog.kakaocdn.net/dn/b6c80g/btrPR5SusBk/8OrHRgyT6wcbt21fS3fQK0/img.png](https://blog.kakaocdn.net/dn/b6c80g/btrPR5SusBk/8OrHRgyT6wcbt21fS3fQK0/img.png)

### **⏺ 선언과 동시에 초기화**

```java
int num1 = 10;
int a = 100, b = 200;
```

- 서로 다른 타입들은 동시 초기화 불가능
- 이미 선언된 변수를 동시에 초기화 할 수 없다.

### **⏺ 변수 명명 규칙**

0) **사용목적에 맞는 작명**이 중요함. (사람에게 잘 읽힐 수 있게)

1) 일반적으로 **카멜케이스(camelCase)** 사용 helloWorld

```
int camelCase;
```

2) **영문자 , 숫자 , _ , $**   : **가능**

3) **대소문자 구별**

4) **숫자로 시작하는 변수명**  : **사용불가**

5) **자바의 예약어(reserved word)**  :  **사용불가 void** 

**[네이밍 컨벤션 공식문서](https://www.oracle.com/java/technologies/javase/codeconventions-namingconventions.html)**

<br><br>
-------
<br><br><br><br>

![image](https://user-images.githubusercontent.com/48430781/199239699-b2ef62ed-3db3-45a2-a34b-992599f42c9a.png)

<br><br>

![image](https://user-images.githubusercontent.com/48430781/199239800-643e1b60-ceee-47a5-b1a4-4e4dd32fad1b.png)

<br><br>

![image](https://user-images.githubusercontent.com/48430781/199239888-b42fb460-c61f-41b5-b509-23e4ae648ad2.png)


