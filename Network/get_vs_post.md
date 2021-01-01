# 📌 GET

서버로부터 정보를 조회하기 위해 설계된 메소드

- 요청하는 데이터가 `HTTP Request Message Header 부분` 의 url에 담겨서 전송됨.
- url 상 ? 뒤에 데이터가 붙어 request를 보내게 됨. (쿼리스트링을 통해 전송)
  - 다중 파라미터이면 & 로 연결
  - url에 조회 조건 표시하므로 특정 페이지를 링크하거나 북마크 가능
- url 이라는 공간에 담겨서 전송되기 때문에 데이터 크기가 제한적
- 보안이 필요한 데이터에는 적절하지 않음 (url에 그대로 노출) ex) password

<pre>
예시)
www.example-url.com/resources?name1=value1&name2=value2
</pre>

# GET vs POST

# 📌 POST

리소스를 생성/변경하기 위해 설계됨.

- request가 `HTTP Message의 Body 부분` 에 데이터가 담겨서 전송됨.
- GET 방식보다는 데이터의 크기가 큼. (대용량 데이터 전송 가능)
- GET 방식보다 보안 측면에서 낫다. ( but 암호화하지 않는 이상 비슷비슷.. )
- 요청 헤더의 Content-Type에 요청 데이터의 타입을 표시해야 함.

# 📌 GET vs POST

[GET]

- 가져오는 것.

  → 서버에서 어떤 데이터를 가져와서 보여주는 용도

  → SELECT적인 성향

- 브라우저에서 caching 가능

- Idempotent( 멱등 ) 하게 설계됨 : 서버에게 동일한 요청을 하면 여러 번 전송하더라도 동일한 응답이 돌아와야 한다.

[POST]

- 서버의 값이나 상태를 변경 or 추가하기 위해 사용
- Non-Idempotent( 멱등 ) 하게 설계됨 : 서버에게 동일한 요청을 여러 번 전송해도 응답은 항상 다를 수 있다.
