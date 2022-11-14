# Annotation
	 주석과 같이 프로그래밍 언어에 영향을 미치지 않으며, 유용한 정보를 제공.
**프로그램의 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것.**


#### "주석"
``Annotation`` vs  ``comment``

차이는 정보를 전달하는 대상이 누구(무엇)인가에 있다.
![](https://velog.velcdn.com/images/bokimy/post/480e86a9-4a5b-4766-a0bc-377e83c209d5/image.png)

## 🟡 등장 배경
#### 주석
과거에는 소스코드에 대한 문서를 따로 저장했기 때문에 소스코드를 변경할 때마다 문서를 같이 변경해야 했다. 그러다보니 소스코드 변경 후 문서를 변경하는 것을 놓치고 넘어가는 경우가 종종 있었다. -> 관리 어려움 => 주석의 등장
소스코드와 개발문서 버전 불일치 발생 많았음 -> 주석의 적극 도입으로 해결
주석의 등장으로 소스코드와 개발 문서를 하나의 파일로 관리할 수 있게 되었다.
``/** ~ */`` : javadoc.exe 주석 (소스코드의 주석으로부터 HTML 문서를 생성해내는 프로그램)

#### 애너테이션
소스코드와 설정 파일(.xml) 따로 존재했었다. -> 주석의 경우와 마찬가지로 어려움이 있음 => 애너테이션의 등장
애너테이션의 등장으로 소스코드와 설정에 대한 정보를 하나의 파일로 관리할 수 있게 되었다.

## 🟡 주요 역할
> 1) 컴파일에게 문법 에러 체크하도록 정보 전달
2) 프로그램 빌드 시 코드를 자동으로 생성할 수 있도록 정보 제공
3) 런타임에 특정 기능 실행할 수 있도록 정보 제공

**해당 애너테이션을 수행하는 프로그램 외에 다른 프로그램들에게 아무런 영향을 주지 않는다.
=> 명확한 타겟 존재, 타겟 외 대상에게는 없는 존재이다.**


---
## 🟡 애너테이션 종류
- 표준 애너테이션
- 메타 애너테이션
- 사용자 정의 애너테이션  : 사용자 직접 정의

### 👉🏻 표준 애너테이션 : 주로 컴파일러를 위한 것
> 자바 기본 제공
![](https://velog.velcdn.com/images/bokimy/post/2816204e-7d17-49fd-a613-f187935913bb/image.png)

### 👉🏻 매타 에너테이션
> '애너테이션의 애너테이션' => 애너테이션 정의 
애너테이션 만들 때 사용
``java.lang.annotation`` 패키지에 포함되어 있음
![](https://velog.velcdn.com/images/bokimy/post/a26f1c5a-cfee-4c83-94ee-0e4a724ebaf5/image.png)

### 👉🏻 사용자 정의 애너테이션
> 사용자가 직접 정의

---
## 🟡 @Target
> 애너테이션이 적용 가능한 대상을 지정하는 데에 사용.
애너테이션을 적용할 수 있는 대상을 ``@Target`` 으로 지정.
여러 개의 값을 지정할 때는 배열처럼 중괄호 ``{}`` 를 사용.

```java
//ex)
@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR})
```

**@Target으로 지정할 수 있는 애너테이션 적용 대상**
![](https://velog.velcdn.com/images/bokimy/post/eb038fb2-f0d2-46fb-a672-7a30aba4aa70/image.png)

```
TYPE : 타입 선언할 때, 애너테이션을 붙일 수 있음.
TYPE_USE : 해당 타입의 변수를 선언할 때, 붙일 수 있음.
FIELD : 기본형 타입에 사용.
TYPE_USE : 참조형 타입에 사용.
```

---
## 🟡 @Retention
애너테이션이 유지(retention)되는 기간을 지정하는 데에 사용.

애너테이션 유지 정책 (retention policy)
![](https://velog.velcdn.com/images/bokimy/post/3cbc0202-98ce-49e6-87a3-5c203f294906/image.png)

### 👉🏻 ``SOURCE``
컴파일러에 의해 사용되는 애너테이션 
	컴파일러를 직접 작성할 것이 아니면, 이 유지정책은 사용할 일이 없다.
### 👉🏻 ``RUNTIME``
유지정책을 RUNTIME으로 하면 실행 시에 reflection을 통해 클래스 파일에 저장된 애너테이션의 정보를 읽어서 처리할 수 있다.

```
cf)
@FunctionalInterface
컴파일러가 체크해주는 애너테이션이지만, 실행 시에도 사용되기 때문에 유지 정책이 RUNTIME으로 설정되어있다.
```
### 👉🏻 ``CLASS``
컴파일러가 애너테이션의 정보를 클래스 파일에 저장할 수 있게 함.
그러나 클래스 파일이 JVM에 로딩될 때 애너테이션의 정보가 무시되기 때문에 실행 시에 애너테이션에 대한 정보를 얻을 수 없다.
그렇기 때문에 CLASS가 유지 정책의 기본값임에도 불구하고 잘 사용되지 않는다.

```
cf)
지역 변수에 붙은 애너테이션은 컴파일러만 인식할 수 있기 때문에,
유지 정책이 RUNTIME인 애너테이션을 지역변수에 붙여도 실행 시에 인식되지 않는다.
```

---
## 🟡 @Documented
> 애너테이션에 대한 정보를 javadoc으로 작성한 문서에 포함시킴.

- 기본 애너테이션 중 @Override 와 @SuppressWarnings 를 제외하고는 @Documented가 붙어있다.

- ex

```java
@Documented
@Retention (RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @Interface FunctionInterface {}
```

---
cf)
자바의 정석(남궁 성)
