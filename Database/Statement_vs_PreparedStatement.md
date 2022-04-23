- 자바에서 데이터베이스로 쿼리문을 전송할 때, 사용할 수 있는 인터페이스는 2가지가 존재한다.
⇒ **Statement**, **PreparedStatement**


## Statement

1) Statement 객체는 Statement 인터페이스를 구현한 객체를 Connection 클래스의 **createStatement()** 메소드를 호출함으로써 얻어진다.

```java
String sqlstr = "SELECT name, memo FROM TABLE WHERE name =" + num
Statement stmt = conn.createStatement();
ResultSet rst = stmt.executeQuery(sqlstr);
```

2) Statement 객체가 생성되면 **executeQuery()** 메소드를 호출하여 SQL문을 실행시킬 수 있다.
메소드의 인수로 SQL문을 담은 Srting 객체를 전달한다.

3) Statement는 정적인 쿼리문을 처리할 수 있다.즉, 쿼리문에 값이 미리 입력되어있어야한다.

## PreparedStatement

1) PreparedStatement 객체는 Connection 객체의 **preparedStatement()** 메소드를 사용해서 생성한다. 
이 메소드는 인수로 SQL문을 담은 String 객체가 필요하다.

```java
String sqlstr = "SELECT name, memo FROM TABLE WHERE num = ?"
PreparedStatement stmt = conn.preparedStatement();
stmt.setInt(1, num);
ResultSet rst = stmt.executeQuery(sqlstr);
```

2) SQL문장이 미리 컴파일되고, 실행 시간동안 인수 값을 위한 공간을 확보할 수 있다는 점에서 Statement 객체와 다르다.

3) Statement 객체의 SQL은 실행될 때, 매번 서버에서 분석해야하는 반면 PreparedStatement 객체는 한 번 분석되면 재사용이 용이하다.

4) 각각 인수에 대해 위치홀더(placeholder)를 사용하여 SQL문장을 정의할 수 있게 해준다.
위치 홀더는 ? 로 표현된다.

5) 동일한 SQL문을 특정 값만 바꾸어서 여러번 실행해야 할 때, 인수가 많아서 SQL 문을 정리해야 될 필요가 있을 때 사용하면 유용하다.

### Statement와 PreparedStatement의 가장 큰 차이점

> **캐시 사용 유무**
> 

1) statement : SQL문을 실행할 때마다 SQL을 매 번 구문을 새로 작성하고 해석해야하므로 오버헤드가 존재한다.

2) PreparedStatement : 선처리 방식 사용 (준비된 statement) 즉, SQL문을 미리 준비해 놓고 바인딩 변수(? 연산자)를 사용해서 반복되는 비슷한 SQL문을 쉽게 처리

- **쿼리 실행 순서**
1. 쿼리 문장 분석
2. 컴파일
3. 실행

**Statement** : 매번 쿼리를 수행할 때마다 1~3단계를 거친다.
**PreparedStatement** : 처음 한 번만 3단계를 거친 후 캐시에 담아 재사용한다.

### Prepared Statement를 사용해야 하는 경우

**1) 사용자 입력값으로 쿼리문을 실행하는 경우**

- 특수 기호가 들어오더라도 알아서 파싱해주므로 이로 인한 에러를 막을 우 있음

**2) 쿼리 반복 수행 작업일 경우**
