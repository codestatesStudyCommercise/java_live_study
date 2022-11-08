# 6주차 - 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)

<aside>
➡️ 작성일 : 2022.11.07

</aside>

---

# Method Dispatch

- 자바는 컴파일 타임시점에는 객체 타입에 대한 정보만 가지고 있다가 실질적인 객체 생성은 런타임시점에 이루어진다.
- Method Dispatch 는 메서드를 호출하는 과정에서 
어떤 메서드를 실행할지를 결정하여 실제로 실행시키는 과정

---

# 1. Static Dispatch

- 컴파일타임에서부터 어떤 메서드가 호출될지 정해져있는것
- 컴파일 시점에서 컴파일러가 특정 메서드를 호출할 것이라는 것을 명확히 아는 경우
    - 참조변수의 타입이 메서드를 구현한 클래스의 경우 메서드를 호출하면 어떤 메서드가 호출될지 정적으로 정해진다.
    - 오버로딩으로 매개변수에 따른 여러 메서드가 있다고 해도 같은 원리가 적용된다.
    
    ```java
    public class StaticTest {
        public static void main(String[] arg) {
            StaticDspatch staticCase = new StaticDspatch();
            staticCase.print();
        }
    }
    
    public class StaticDspatch{
    
        public void print(){
            System.out.println("this is Static Dispatch");
        }
    
    		public void print(String str) {
            System.out.println("this is Static Dispatch (" + str + ")");
    		}
    }
    ```
    

# 2. Dynamic Dispatch

- 재정의된 메서드에 대한 호출이 컴파일 시간이 아닌 런타임에 확인되는 프로세스.
- 인터페이스, 추상클래스를 이용해 참조함으로서 호출되는 메서드가 동적으로 정해지는걸 말한다.
- 컴파일러는 컴파일 시점에 추상 메서드만 호출하는것임을 알 뿐, 어떤 메서드를 호출하는지는 모른다.
    - 상위 클래스의 참조 변수를 통해 재정의된 메서드가 호출되는 경우
    - 런타임 시점에 참조변수에 할당된 객체를 보고 메서드를 실행한다.

```java
// 예시 1.
public class DynamicDispatchTest {
    public static void main(String[] arg) {
            Printable dynamicDispatch = new DynamicDispatch();
            dynamicDispatch.print();

            PrintAbstract dynamicDispatchAbst = new DynamicDispatchAbstractChild();
            dynamicDispatchAbst.print();
    }
}

public class DynamicDispatchAbstractChild extends PrintAbstract{
    @Override
    void print() {
        System.out.println("this is Dynamic Dispatch abstract PrintAbstract");
    }
}

public class DynamicDispatch implements Printable{
    public void print(){
        System.out.println("this is Dynamic Dispatch");
    }
}

public abstract class PrintAbstract {
    abstract void print();
}

public interface Printable {
    void print();
}

//--------------------------------------------------------------------
// 예시 2.
List <Service> svc = Arrays.asList(new MyService1(), new MyService2());
svc.forEach(s -> s.run());
```

# 3. **Double** Method Dispatch

- 객체에 따른 메서드 호출과 더불어 객체의 매개변수에 따른 다른 결과를 원한다면 사용하는 패턴
- Dynamic Dispatch 를 2번 실행하는 방법으로 자바가 싱글 디스패치언어임에서 오는 특성의 한계를 해결하기 위한 방법
- Visitor 패턴보다 범용적인 해결방법
    - 여러 객체에 대해 각 객체의 동작들을 지정하는 패턴에서 사용된다
- 예시에서는 메서드를 실행할 객체가 결정될때 1번, 실행된 메서드 내부에서 매개변수로 받은 객체가 메서드를 실행할때 매개변수의 객체가 확정될 시점에 1번으로 2번 실행된다.

## 예제의 문제를 해결해가는 방식으로 구현 by 토비의 봄

- [https://www.youtube.com/watch?v=s-tXAHub6vg&list=PLZurYav1io3IAh9_13_gb881_EHeRITO4&index=3&t=3550s&ab_channel=TobyLee](https://www.youtube.com/watch?v=s-tXAHub6vg&list=PLZurYav1io3IAh9_13_gb881_EHeRITO4&index=3&t=3550s&ab_channel=TobyLee)
- 목표 : 객체에 따른 다른 메서드가 실행됨과 더불어 매개변수에 따라 다른 결과를 가져오자

### ver 1. 예제코드

```java
public class SNSFirst {

    /*
    문제점 1. 객체의 타입을 판별하는 방식으로 if 문 로직을 사용함 (instanceof 는 안티패턴으로 많이 지적)
             1-1. if 문 로직에 걸리지 않을 수도 있으며 if 문 로직을 그대로 통과해버리면 로직에 장애가 발생
             1-2. 새로운 SNS 종류가 추가 될 시 새로운 SNS 타입을 반영하는 if 문 로직을 추가해줘야함 : 잊고 빼먹을 여지가 있음
						-> 개선 시도
     */

    // Post
    interface Post {
        void postOn(SNS sns);
    }
    static class Text implements Post {
        public void postOn(SNS sns) {
            // 문제 지점
            if (sns instanceof Facebook) {
                System.out.println("text - facebook");
            }
            if (sns instanceof Twitter) {
                System.out.println("text - twitter");
            }
//            if (sns instanceof GooglePlus) {
//                System.out.println("text - google plus");
//            }
        }
    }
    static class Picture implements Post {
        public void postOn(SNS sns) {
            // 문제 지점
            if (sns instanceof Facebook) {
                System.out.println("picture - facebook");
            }
            if (sns instanceof Twitter) {
                System.out.println("picture - twitter");
            }
        }
    }

    // SNS
    interface SNS{

    }
    static class Facebook implements SNS {
    };
    static class Twitter implements SNS {
    };
//    static class GooglePlus implements SNS {
//    };

    // main
    public static void main(String[] args) {
        List<Post> posts = Arrays.asList(new Text(),new Picture());
        List<SNS> sns = Arrays.asList(new Facebook(),new Twitter() // , new GooglePlus()
        );

        // 다이나믹 디스패치 수행 : 이중 for문
        posts.forEach( p -> sns.forEach( s -> p.postOn(s)));

        // ==
        // posts.forEach((Post p) -> sns.forEach((SNS s) -> p.postOn(s)));
    }
}
```

### ver2. 예제코드 : 에러발생 - 실행불가능

```java
public class SNSSecond {

    // 문제점 1을 개선하여 나온 2번째 코드 : 메서드 오버로딩과 SNS 를 구체화 하여 매개변수로 받아 처리
    /*
        문제점 2. 적용 불가능
            55번째 줄 컴파일 시점에 SNS타입을 찾을수 없다는 내용의 에러 발생
            원인 : 메서드 오버로딩 시 매개변수가 구체적인 타입이기 때문
            메서드 오버로딩은 스테틱 디스패치가 이루어지기 때문에 컴파일 시점에 매개변수의 타입을 정확하게
            지정해두어야한다.
            매서드 오버로딩일 일어나기 위해선 스태틱 디스패치를 해야하는데 주어진 정보만 가지고는
            어느메서드를 실행해야하는지 잡을 수 없다.
            다이나믹 디스패칭 시 다이나믹 조건이 파라미터에 걸려있기때문에 실행되지 않음 : 파라미터는 다이나믹 디스패치의 조건이 되지않는다.
            -> 이를 해결하기 위해선 다형성을 두번 적용하는 과정이 필요함
     */

    // Post
    interface Post {
        // 2. 메서드 오버로딩과 매개변수 타입 구체화 추가
        void postOn(Facebook sns);
        void postOn(Twitter sns);
    }
    static class Text implements Post {
        // 문제 지점
        // 2. 메서드 오버로딩과 매개변수 타입 구체화 추가
        public void postOn(Facebook sns) {
            System.out.println("text-facebook");
        }
        public void postOn(Twitter sns) {
            System.out.println("text-twitter");
        }
    }
    static class Picture implements Post {
        // 2. 메서드 오버로딩과 매개변수 타입 구체화 추가
        public void postOn(Facebook sns) {
            System.out.println("picture-facebook");
        }
        public void postOn(Twitter sns) {
            System.out.println("picture-twitter");
        }
    }

    // SNS
    interface SNS{
    }
    static class Facebook implements SNS {
    };
    static class Twitter implements SNS {
    };

    // main
    public static void main(String[] args) {
        List<Post> posts = Arrays.asList(new Text(),new Picture());
        List<SNS> sns = Arrays.asList(new Facebook(),new Twitter() // , new GooglePlus()
        );

        // 에러발생
        // 다이나믹 디스패치 수행 : 이중 for 문
        // posts.forEach( p -> sns.forEach( s -> p.postOn(s)));

        // ==
        // posts.forEach((Post p) -> sns.forEach((SNS s) -> p.postOn(s)));
    }
}
```

### ver3. 예제코드

```java
public class SNSThird {

    /*
        3. 객체지향스러운 결과 : SNS 를 새로 추가하는것이 자유롭고 코드를 추가하는 시점에서 의존하는 코드(Post 측)에 직접적인 영향을 주지 않음
                            단, Post 측의 변경이 일어날때는 다른 고민이 필요함
     */

    // Post
    interface Post {
        // 3. 다시 원상복귀 SNS 타입으로 받는다.
        void postOn(SNS sns);
    }
    static class Text implements Post {
        // 문제 지점
        // 3. 구현을 SNS 로 옮긴다.
        public void postOn(SNS sns) {
            sns.post(this); // sns의 post 를 호출하고 자기 자신을 넘기도록 구현
            // 다이나믹 디스패칭 시점 2. : sns 에 대한 다이나믹 디스패칭이 일어남
        }
    }
    static class Picture implements Post {
        // 문제 지점
        // 3. 구현을 SNS 로 옮긴다.
        public void postOn(SNS sns) {
            sns.post(this); // sns의 post 를 호출하고 자기 자신을 넘기도록 구현
            // 다이나믹 디스패칭 시점 2. : sns 에 대한 다이나믹 디스패칭이 일어남
        }
    }

    // SNS
    interface SNS{
        // 3. 메서드 추가
        void post(Text post);
        void post(Picture post);
    }
    static class Facebook implements SNS {
        // 3. 구현 추가
        public void post(Text post) {
            System.out.println("text-facebook");
        }
        // 3. 구현 추가
        public void post(Picture post) {
            System.out.println("picture-facebook");
        }
    };
    static class Twitter implements SNS {
        // 3. 구현 추가
        public void post(Text post) {
            System.out.println("text-twitter");
        }
        // 3. 구현 추가
        public void post(Picture post) {
            System.out.println("picture-twitter");
        }
    };
    // 새로운 SNS 추가
    static class GooglePlus implements SNS {
        // 3. 구현 추가
        public void post(Text post) {
            System.out.println("text-google plus");
        }
        // 3. 구현 추가
        public void post(Picture post) {
            System.out.println("picture-google plus");
        }
    };

    // main
    public static void main(String[] args) {
        List<Post> posts = Arrays.asList(new Text(),new Picture());
        List<SNS> sns = Arrays.asList(new Facebook(),new Twitter() ,new GooglePlus());

        // 에러발생
        // 다이나믹 디스패치 수행
        posts.forEach( p -> sns.forEach( s -> p.postOn(s))); // 다이나믹 디스패칭 시점 1.

        // ==
        // posts.forEach((Post p) -> sns.forEach((SNS s) -> p.postOn(s)));
    }
}
```

---

- 참고
    - [https://multifrontgarden.tistory.com/133](https://multifrontgarden.tistory.com/133)
    - [https://dev-jj.tistory.com/entry/Java-Method-Dispatch-Static-Dispatch-Dynamic-Dispatch-Double-Dispatch?category=861922](https://dev-jj.tistory.com/entry/Java-Method-Dispatch-Static-Dispatch-Dynamic-Dispatch-Double-Dispatch?category=861922)
    - [https://www.javatpoint.com/runtime-polymorphism-in-java](https://www.javatpoint.com/runtime-polymorphism-in-java)
    - [https://defacto-standard.tistory.com/entry/JAVA-Static-Method-Dispatch-Dynamic-Method-Dispatch-Double-Dispatch](https://defacto-standard.tistory.com/entry/JAVA-Static-Method-Dispatch-Dynamic-Method-Dispatch-Double-Dispatch)
    - [https://www.notion.so/e5c33507880b4d098f83a2c4f8f02c04](https://www.notion.so/e5c33507880b4d098f83a2c4f8f02c04)
    - [https://www.youtube.com/watch?v=s-tXAHub6vg&list=PLZurYav1io3IAh9_13_gb881_EHeRITO4&index=3&t=3550s&ab_channel=TobyLee](https://www.youtube.com/watch?v=s-tXAHub6vg&list=PLZurYav1io3IAh9_13_gb881_EHeRITO4&index=3&t=3550s&ab_channel=TobyLee)