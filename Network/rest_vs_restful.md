# REST & RESTful



REST란 Representational State Transfer의 약자로 웹의 장점을 최대한 활용할 수 있는 Client와 Server 간 통신 방식 중 하나이다.

설계 기본 규칙으로 HTTP URI를 통해 자원을 명시하고 HTTP method(GET, POST, PUT, DELETE)를 통해 자원을 처리하도록 설계된 아키텍처이다.

RESTful은 REST라는 아키텍처를 구현하는 웹 서비스를 나타내는 것으로 REST 원리를 따르는 시스템을 RESTful이라는 용어로 지칭한다.

## 📌 REST란?

`Representational State Transfe`라는 용어의 약자이다.
자원을 `URI`로 표시하고 해당 자원의 상태를 주고 받는 것을 의미한다.

REST의 구성 요소는

- `자원(Resource): URI`
- `행위(Verb): HTTP METHOD`
- `표현(Representations)`
  로 이루어져 있다.

즉 `Rest`는 `URI`를 통해 자원을 표시하고, `HTTP METHO`를 이용하여 해당 자원의 행위를 정해주며
그 결과를 받는 것을 말한다.

## 📌 REST API란?

Rest 기반의 규칙들을 지켜서 설계된 API를 Rest API 혹은 Restful API이라고 한다.



## 📌 RESTFUL API란?

위에서 설명했던 REST를 REST답게 쓰기 위한 방법이지만 누군가가 공식적으로 발표한 것이 아니고
그저 개발자들이 비공식적으로 의견을 제시한 것이라 명확한 정의는 없다고 한다.
하지만 RESTFUL의 목적은 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것이다.



| CRUD             | HTTP METHOD | URI        |
| ---------------- | ----------- | ---------- |
| user들을 표시    | GET         | /users     |
| user 하나만 표시 | GET         | /users/:id |
| user를 생성      | POST        | /users     |
| user를 수정      | PUT         | /users:id  |
| user를 삭제      | DELETE      | /users:id  |

- Restful 하지 못한 경우

- CRUD 기능을 전부 POST METHOD로만 처리하는 API

- URI에 자원과 id외 정보가 들어가는 경우

  ```tex
   PUT /users/update-nickname [X]
   PUT /users/:id/nickname [O]
  ```

출처 : https://velog.io/@stampid/REST-API%EC%99%80-RESTful-API

