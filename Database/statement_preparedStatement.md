# Statement vs PreparedStatement

우선 속도 면에서 `PreparedStatement`가 빠르다고 알려져 있다. 이유는 쿼리를 수행하기 전에 이미 쿼리가 컴파일 되어 있으며, 반복 수행의 경우 프리 컴파일된 쿼리를 통해 수행이 이루어지기 때문이다.

`PreparedStatement`에는 보통 변수를 설정하고 바인딩하는 `static sql`이 사용되고 `Statement`에서는 쿼리 자체에 조건이 들어가는 `dynamic sql`이 사용된다. `PreparedStatement`가 파싱 타임을 줄여주는 것은 분명하지만 `static sql`을 사용하는데 따르는 퍼포먼스 저하를 고려하지 않을 수 없다.

하지만 성능을 고려할 때 시간 부분에서 가장 큰 비중을 차지하는 것은 테이블에서 레코드(row)를 가져오는 과정이고 SQL 문을 파싱하는 시간은 이 시간의 10 분의 1 에 불과하다. 그렇기 때문에 `SQL Injection` 등의 문제를 보완해주는 `PreparedStatement`를 사용하는 것이 옳다.



- `public interface **Statement**extends Wrapper `

정적 SQL 문을 실행해, 작성된 결과를 돌려주기 위해서(때문에) 사용되는 객체입니다.  

디폴트에서는,`**Statement**` **객체 마다 1 개의** `**ResultSet**` **객체만이 동시에 오픈할 수 있습니다**. 따라서, 1 개의 `ResultSet` 객체의 read가, 다른 read에 의해 끼어들어지면(자), 각각은 다른 `Statement` 객체에 의해 생성된 것이 됩니다. `Statement` 인터페이스의 모든 execution 메소드는, 문장의 현재의 `ResultSet` 객체로 오픈되고 있는 것이 존재하면, 그것을 암묵에 클로즈 합니다.

- **관련 항목:**

  [`Connection.createStatement()`](https://java.ihoney.pe.kr/76) , [`ResultSet`](https://java.ihoney.pe.kr/76)

- `public interface **PreparedStatement**extends Statement `

프리컴파일 된 SQL 문을 나타내는 객체입니다.  

SQL 문은, 프리컴파일 되어`PreparedStatement` 객체에 포함됩니다. 거기서, 이 객체는, 이 문장을 여러 차례 효율적으로 실행하는 목적으로 사용할 수 있습니다.

**주:** IN 파라미터치를 설정하는 설정 기능 메소드 (`setShort`,`setString` 등)는, 입력 파라미터의 정의된 SQL 형과 호환이 있는 형태를 지정하지 않으면 안됩니다. 예를 들어, IN 파라미터에 `INTEGER` 라고 하는 SQL 형이 있는 경우,`setInt` 메소드를 사용하지 않으면 안됩니다.

임의의 파라미터형 변환이 필요한 경우는,`setObject` 메소드는, 목적의 SQL 형으로 사용하지 않으면 안됩니다.  

파라미터 설정의 예를 다음에 나타냅니다. `con` 는 액티브한 접속을 나타냅니다.

```
PreparedStatement pstmt = con.prepareStatement("UPDATE EMPLOYEES
SET SALARY = ? WHERE ID = ? ");
pstmt.setBigDecimal(1, 153833.00)
pstmt.setInt(2, 110592)
```

출처: https://java.ihoney.pe.kr/76 [허니몬(Honeymon)의 자바guru]

