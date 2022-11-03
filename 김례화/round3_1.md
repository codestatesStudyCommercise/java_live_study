## equals()

- 메서드
- 대상의 내용 자체를 비교

---
## ==
- 비교 연산자
- 비교하고자 하는 대상의 주소값 비교

---
## ⭐️ equals()를 써야 하는 이유

ex)
![](https://velog.velcdn.com/images/bokimy/post/3ed83826-39ca-4e3a-adf5-1eeda5e1a040/image.png)


문자열 생성 방법 2가지
1) str1, str2 : String literal로 생성하는 방법
2) str3, 4, 5 : new 연산자를 사용해 생성하는 방법

=> 결과적으로 큰따옴표 안에 있는 문자열이 생성되는 것은 같지만, 내부적으로 저장되는 위치가 다르다.
![](https://velog.velcdn.com/images/bokimy/post/61444619-7b53-4720-96c5-fc13d0e202f7/image.png)


- String 객체이므로, Heap에 저장. 
- 리터럴을 사용해 생성된 문자열(str1,str2)은 Heap 내부에 존재하는 Constant String Pool에 저장된다.
- new 연산자를 사용해 생성된 문자열은 heap 내부에 저장된다.
- str1과 str5는 "One"으로 값이 같지만, 다른 위치에 있는 문자열 객체의 값을 저장하는 것이다. 
- String Pool에 저장된 문자열 객체는 똑같은 값을 또 생성해도 같은 위치에 있는 객체를 저장한다.
	반면, new 연산자를 사용해 새로운 객체를 생성할 경우, heap 내부에 새로운 객체를 만들어 저장한다.
    
### 👉🏻 문자열 비교 ( == & equals)
![](https://velog.velcdn.com/images/bokimy/post/b5e07576-579a-4d62-8f5a-53b6ee916e9a/image.png)

결과값
![](https://velog.velcdn.com/images/bokimy/post/330b8444-5750-4d95-9517-1d4f234b6c3c/image.png)



- '==' 연산자는 해당 문자열의 **주소를 비교**한다. 
- 때문에, str1, str2는 같은 주소에 있는 문자열의 값을 갖고 있기 때문에 비교했을 때 True를 반환하지만, str1, str5는 같은 문자열임에도 불구하고 다른 위치에 있는 문자열의 값을 갖고 있으므로, False를 반환하는 것이다. 
또한, str5와 str6는 new 연산자를 이용해서 생성한 것이므로 주소값이 서로 달라 False가 반환된다. 
- 그러나 보통은 우리가 원하는 것은 주소를 비교하는 것이 아니라 값이 같은지를 묻는 것이기 때문에, 문자 하나하나를 비교하는, 즉 ``값``을 비교하는 equals() 메서드를 사용하는 것이다.


#### 🟡 equals() 메서드 사용
![](https://velog.velcdn.com/images/bokimy/post/d938ba29-894a-499f-a074-c8ce8443f7d5/image.png)

결과값
![](https://velog.velcdn.com/images/bokimy/post/55391a04-7285-4687-9620-1f1121bd2bf5/image.png)

주소를 비교하는 '==' 연산자와 달리,  **equals() 메소드는 문자 하나하나 비교해서 값이 같은지 확인하기 때문에 str1과 str5를 같다고 출력하고 str5와 str6이 같다고 출력**한다.


#### equals() 존재 이유
즉, primitive type은 데이터를 동일한 값을 저장하면 같은 주소에 있는 값을 저장한다. (위의 리터럴 방식처럼)
그러나, primitive type이 아닌 경우, 리터럴 방식이 아닌 경우에는 같은 데이터라도 새로운 메모리 공간을 생성하여 저장하여 각자 다른 주소에 저장되어 있기 때문에 우리가 눈으로 보는 값이 같더라도 같지 않다(false)고 출력된다.
때문에, non-primitive type은 equals() 메서드를 지원하는 것이다.


---
cf)
https://chanos.tistory.com/entry/JAVA-%EB%AC%B8%EC%9E%90%EC%97%B4String%EC%83%9D%EC%84%B1-%EB%AC%B8%EC%9E%90%EC%97%B4-%EB%B9%84%EA%B5%90-Equals-%EC%97%B0%EC%82%B0%EC%9E%90%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90

