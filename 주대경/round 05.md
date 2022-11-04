# new 연산자와 생성자

`new` 키워드는 클래스의 인스턴스를 만드는데 사용.

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/d4559f62-c0ab-4a8a-a812-d6701e25f094/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221104T085547Z&X-Amz-Expires=86400&X-Amz-Signature=70b2f8a9f3cf3cab03b519d118fb8caec102edb867aad99dd87ef3e08af6a29d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![study.drawio-2.png](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/480b4692-f59c-4136-b9a8-361465cfb208/study.drawio-2.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221104T085602Z&X-Amz-Expires=86400&X-Amz-Signature=9e6dc06d87938a67301e4da7d29401074f374229283c328e4041ec4dcda7dd2b&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22study.drawio-2.png%22&x-id=GetObject)

1. 변수가 스택에 생성.
2. `new` 뒤에 있는 생성자의 클래스 이름을 보고, 해당하는 클래스를 메모리를 올림(인스턴스화)
   - 클래스 영역에서 클래스 데이터를 고대로 복사.
3. 생성된 인스턴스의 생성자를 호출.
   - 만약 컴파일 시점에서 생성자가 존재하지 않으면 컴파일러가 기본 생성자를 생성.
4. 생성자가 인스턴스를 초기화.
   - 내부 멤버의 필드가 기본 타입이면 스택에 메모리 생성하고, 참조 타입이면 다시 힙에 메모리 생성.
5. 생성된 메모리의 주소값을 반환.
6. `=` 연산자로 변수에 주소값이 할당

# 기본 타입과 참조 타입의 이해

출력 값 예상해보기

```java
public class App {
    public static void main(String[] args) {
        int num = 1;
        int[] nums = { 0, 1 };
        Dog dog1 = new Dog("1번 개");
        Dog dog2 = new Dog("2번 개");

        foo(num, nums, dog1, dog2);

        System.out.println(num);
        System.out.println(nums[0]);
        System.out.println(dog1.getName());
        System.out.println(dog2.getName());

    }

    static void foo(int num, int[] nums, Dog dog1, Dog dog2) {
        num = 100;
        nums[0] = 100;
        dog1 = new Dog("3번 개");
        dog2.setName("4번 개");
    }
}

class Dog {
    private String name;

    public Dog(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

출력 결과

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/07f32593-686b-43b2-8ae1-4fa159aa5525/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221104%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221104T085623Z&X-Amz-Expires=86400&X-Amz-Signature=0e50370fdd83f818bf797b89d0496fb22a278a69b49b8c2575b1904c4134ef1f&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
