# 타입 추론 var

# 타입추론이란?

타입추론은 개발자가 변수의 타입을 명시하지 않아도, 컴파일러가 변수의 타입을 대입된 리터럴로 타입을 추론.

# var

- 자바 10부터 지원.
- 선언과 동시에 초기화가 필수.
- null이 할당될 수 없다.
- 키워드가 아니기 때문에 변수명으로 할용가능.
  ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/2931d4fe-cfe4-4010-a207-30bac6611ff4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T001843Z&X-Amz-Expires=86400&X-Amz-Signature=f31bb70f717274023e63e711fba5b3a82e64b9764677ffd2d6090ff2c4a61705&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
- 지역변수로만 이용가능.(멤버변수(필드), 메소드의 매개변수(파라미터), 리턴타입으로 사용 불가)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/146600ae-3119-4eec-b6ee-285f84eff94c/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T001906Z&X-Amz-Expires=86400&X-Amz-Signature=dccbfd753564a7a3df7b1040749f19072010aa97c2698c3f690659393bfdfd35&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 컴파일에 추론하기 때문에 runtime에는 추가 연산이 없어 성능 영향 x
    <aside>
    💡 컴파일 되면 타입이 바뀔 일이 없음!!
    
    </aside>

- 배열에 사용불가.
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6809f048-9683-4bc5-9705-eb04c78b8784/Untitled.png)
    <aside>
    💡 동일한 타입만 들어갈 수 있는데, 타입을 모르기 때문.
    
    </aside>

- 다이아몬드 연산자`<>` 에 타입 명시 안 하면 `<Object>`로 추론.
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a7b9bd1c-d7b2-4a04-b1f4-d73a76fda18d/Untitled.png)
    <aside>
    💡 다이아몬드 연산자란?
    자료형 데이터 타입에 타입을 추론할 수 있도록 도와주는 연산자
    
    </aside>

- (람다 사용시 정확한 타입 명시 필요.)

# var 쓰는 이유

- 데이터의 타입을 유추할 수 없어 변수 명명에 더욱 신경씀.
  ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6809f048-9683-4bc5-9705-eb04c78b8784/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T001920Z&X-Amz-Expires=86400&X-Amz-Signature=45b91219a4106a549388bcb90fcc7becfb20645428c24619726bc892f3cceb39&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
- `forEach`에서 사용시 타이핑이 더 간결해지고, `Object` 타입을 단정할 필요 x
  ![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a7b9bd1c-d7b2-4a04-b1f4-d73a76fda18d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T001937Z&X-Amz-Expires=86400&X-Amz-Signature=4c3a8c10b3c32df7fc4393d471607dc45694c9130266041c708b1f3429c5523f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
- (익명 클래스에서 사용시, 선언한 이후에는 변수가 바뀔 일이 없기 때문에 편리)
- (람다에는 파라미터 어노테이션을 넣을 수 없는데, 넣고 싶다면 따로 메소드를 만들거나 익명 클래스로 정의해야함.)

[https://93jpark.tistory.com/124](https://93jpark.tistory.com/124)

[https://velog.io/@bk_log/Java-타입-추론](https://velog.io/@bk_log/Java-%ED%83%80%EC%9E%85-%EC%B6%94%EB%A1%A0)

[https://catch-me-java.tistory.com/19](https://catch-me-java.tistory.com/19)

배열이란, 동일한 타입의 값들을 하나의 묶음으로 묶은 자료 구조.

# n차원 배열의 선언

- 차원이란 축의 갯수
- 배열의 요소가 또 다른 배열인 경우
  - 배열의 중첩 정도에 따라 1차원 배열, 2차원 배열, 3차원 배열

# 1차원 배열

- 축이 하나인 배열
- 중첩된 요소가 없는 배열

```java
type[] 배열명 = new type[];
type[] 배열명 = new type[]{};
type[] 배열명 = {값, ...};
```

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/72ce3bf0-3cd2-488f-aae2-935e73519405/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T002044Z&X-Amz-Expires=86400&X-Amz-Signature=768b348c3b15dec717ac94d7f9c3a41a1056e20043969dfe392914fb8770f8b2&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3 at App.main(App.java:33)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/94417d92-0e2e-42aa-8970-8cce0cdcd713/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T002101Z&X-Amz-Expires=86400&X-Amz-Signature=29f666ec5e8651f292f36a72b810a22a0e179a4bfbd1d024bcb7aea22de2b3f8&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3bebb042-e4d4-4d98-93c4-a1801b4566a3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T002117Z&X-Amz-Expires=86400&X-Amz-Signature=1fc9201644e1e45ad45f5fa55fcd61b473f3d2a9ea4ff07b339e2e0c9569b56e&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

- 모든 배열은 인덱스로 접근, 인덱스 0부터 길이의 -1 인덱스까지 존재

# 2차원 배열

- 축이 두 개인 배열
- 중첩된 요소가 하나있는 배열

```java
type[][] 배열명;
배열명 = new 타입[][];

타입[][] 배열명 = new 배열명[][]'
배열명 = {{}, ...}
```

![Array constants can only be used in initializers](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/741c3557-d580-4a02-bf4f-42a745fa8010/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T002127Z&X-Amz-Expires=86400&X-Amz-Signature=5a25b454779819bdfcc1f3fe5b7b6a727dd737661d8012e01d384249447641da&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

Array constants can only be used in initializers
