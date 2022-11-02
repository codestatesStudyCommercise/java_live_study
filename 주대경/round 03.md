# 시프트 연산자

Shift

| 기호 | 설명                                      | 예시    |
| ---- | ----------------------------------------- | ------- |
| <<   | 왼쪽 항을 왼쪽으로 오른쪽 항만큼 시프트   | a << 2  |
| >>   | 왼쪽 항을 오른쪽으로 오른쪽 항만큼 시프트 | a >> 2  |
| >>>  | >>와 동일 (단, unsigned 부호없음)         | a >>> 2 |

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3436da9f-6834-41ea-b512-b2032392cc09/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T133005Z&X-Amz-Expires=86400&X-Amz-Signature=b986ce02d6d4cb9efc4fa82ceb73eb58c4adfe7fccddf38a4ae4c371a9fdc516&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/6b0bfea2-e592-4653-8b7c-bcf62a4c32f3/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T133021Z&X-Amz-Expires=86400&X-Amz-Signature=e00fc4f474b489f6e6ee072a8140ad011279e43c0fe19ec14ab6c6ea2f6a418c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

### `>>` vs `>>>`

`>>` 와 `>>>`는 양수를 계산할 때는 차이가 없지만, 음수를 계산할 때 차이가 남.

`>>` 는 시프트 연산을 하고 빈 공간을 `1`로 채움.

`>>>`는 시프트 연산을 수행하고 빈 공간을 `0`으로 채움. 때문에 `-` 부호가 사라져서 `+` 부호가 됨

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/e5e2c9af-95b7-41c5-a610-5d07b18f41cc/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T133035Z&X-Amz-Expires=86400&X-Amz-Signature=b761805dbfe056dfbc2ebd79ddc7b1936bed264cf4bba4b6eacebc1579948565&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

# 복합 대입 연산자

| 기호 | 설명                                 | 풀이        |
| ---- | ------------------------------------ | ----------- |
| +=   | 좌변의 변수 + 연산하고 좌변에 할당   | a = a + 1   |
| -=   | 좌변의 변수 - 연산하고 좌변에 할당   | a = a - 1   |
| \*=  | 좌변의 변수 \* 연산하고 좌변에 할당  | a = a \* 1  |
| /=   | 좌변의 변수 / 연산하고 좌변에 할당   | a = a / 1   |
| %=   | 좌변의 변수 % 연산하고 좌변에 할당   | a = a % 1   |
| &=   | 좌변의 변수 & 연산하고 좌변에 할당   | a = a & 1   |
| ^=   | 좌변의 변수 ^ 연산하고 좌변에 할당   | a = a ^ 1   |
| ㅣ = | 좌변의 변수 ㅣ 연산하고 좌변에 할당  | a = a ㅣ 1  |
| <<=  | 좌변의 변수 << 연산하고 좌변에 할당  | a = a << 1  |
| >>=  | 좌변의 변수 >> 연산하고 좌변에 할당  | a = a >> 1  |
| >>>= | 좌변의 변수 >>> 연산하고 좌변에 할당 | a = a >>> 1 |

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/15bffe4a-0d69-49be-9b72-40b046f2bd22/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T133051Z&X-Amz-Expires=86400&X-Amz-Signature=1ff613ac274bb0dbd1826e24eac1f22653415957de4c73f7ae0bfda3eb82b10d&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b7435d17-e007-4e95-ae43-c0873425d74f/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T133107Z&X-Amz-Expires=86400&X-Amz-Signature=8a4237f902465eca248bdf6251c867c0d8e1d779e7223df718191c7501f47e8c&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/3fb32931-4adf-41b6-a17a-5aaa616c1711/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20221102%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20221102T133121Z&X-Amz-Expires=86400&X-Amz-Signature=94c11c48611ec8bc398459cd0b09c99e1e7f7225552e61190cc9034ee1b373d6&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)
