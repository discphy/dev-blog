# Postman 글로벌 함수 

`Postman`을 사용 하다가..

여러  `HTTP request` 의  `Pre-request Script`에서 공통적으로 호출하는 **함수**가 필요해(반복이 제일 싫다.. 🤣) 내용을 찾아보다 좋은 방법을 발견하여 간단하게 공유합니다!! 

> `Pre-request Script` :  `HTTP`호출 전 실행 할 스크립트를 이야기 한다. 

1. `New` 버튼을 클릭하여 `Collection` 생성 

<img width="1512" alt="1_1" src="https://user-images.githubusercontent.com/106896235/197662670-73b70c8f-0a91-45ed-83b6-eea0b02afbb7.png">
<img width="1512" alt="1_2" src="https://user-images.githubusercontent.com/106896235/197662738-b413e913-2bba-4efb-a379-30d4cc14cccf.png">

2. 아래와 같이 `Pre-request Script` 클릭후 공통으로 사용할 함수를 정의 한다. 

<img width="1512" alt="2_1" src="https://user-images.githubusercontent.com/106896235/197662788-aaffbbd7-1c86-40db-a2c2-da3489ff4b83.png">
<img width="1512" alt="2_2" src="https://user-images.githubusercontent.com/106896235/197662799-f3fd4ce2-e659-43fa-9eca-a94a444f4554.png">

> 함수를 정의할 때 `var`, `let`으로 변수를 선언하게 되면 `Postman`의 전역(`global`) 변수로 선언되기 때문에 변수 타입없이 선언해야합니다. 

3. `HTTP Request` 생성 후 마찬가지로 `Pre-request Script` 작성 및 `HTTP`요청 `URL`을 작성 한다.

<img width="1512" alt="3_1" src="https://user-images.githubusercontent.com/106896235/197662846-b35123f3-8a5c-4f8e-b135-d4011502ba1d.png">
<img width="1512" alt="3_2" src="https://user-images.githubusercontent.com/106896235/197662851-25da0bad-c14d-40f7-9060-7b97c8f113e9.png">
<img width="1512" alt="3_3" src="https://user-images.githubusercontent.com/106896235/197662858-a6f6ed1d-4924-413b-855d-1ab334ac7c05.png">


> 여기까지 완료하면 테스트 환경 구축 완료 🙃

---

### 테스트 및 결과 확인 

 `Console`을 열고 `Send`로 `HTTP`를 요청하면 다음과 같이 결과가 출력된다는 걸 확인 할 수 있다…

<img width="1512" alt="4_1" src="https://user-images.githubusercontent.com/106896235/197662866-55a98f05-74e3-444b-8acc-d78bc9f54b5f.png">

> `{{url}}`이라는 `Postman`의 전역(`global`) 변수를 지정하지 않았기 때문에 `Console`에 에러가 나는 걸 확인 할 수 있다. 

---

항상 반복을 제거하기 위해 `Search`하자.. 🧑🏻‍💻

###### 참고
[Stackoverflow](https://stackoverflow.com/questions/45673961/how-to-write-global-functions-in-postman).  
[Postman 공식 doucment](https://learning.postman.com/docs/writing-scripts/pre-request-scripts/#re-using-pre-request-scripts).



