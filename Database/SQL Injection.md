# SQL Injection

### SQL Injection

SQL Injection는 악의적인 사용자가 보안상의 취약점을 이용하여 임의의 SQL문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위이다.

</br>

</br>

### 공격 방법

**Error based SQL Injection** : 논리적 에러를 이용한 SQL Injection

```sql
SELECT * FROM Users WHERE id = 'INPUT1' OR 1 = 1 -- AND password = 'INPUT2';
```

해당 구문에서 악의적인 사용자가 임의의 SQL 구문인 `OR 1 = 1--`을 삽입한 것이다. `OR 1 = 1--` 은 조건문을 모두 참으로 만들고, `--` 를 통해 뒤에 나오는 구문을 모두 주석 처리하였다. 이렇게 되면 Users 테이블에 있는 모든 정보를 조회할 수 있게 된다.

</br>

**Union based SQL Injection** : Union 명령어를 이용한 SQL Injection

Union 키워드는 두 개의 쿼리문에 대한 결과를 통합해서 하나의 테이블로 보여주게 하는 키워드이다.

```sql
SELECT * FROM Board WHERE title LIKE '%' UNION SELECT null, id, password From Users --
```

Board 테이블에서 게시글을 검색하는 쿼리문인데, Union 키워드를 추가하면 두 쿼리문이 합쳐져서 하나의 테이블로 보여지게 된다. 이때 사용자의 개인정보 (id, password)와 게시글 정보가 함께 유출된다.

</br>

**Blind SQL Injection** : Boolean based SQL

데이터베이스로부터 특정한 값이나 데이터를 전달받지 않고, 단순히 참과 거짓 정보만 알 수 있을 때 사용한다. 로그인 폼에 SQL Injection이 있다고 가정할 때, 서버가 응답하는 로그인 성공과 실패 메시지를 이용하여 DB의 테이블 정보를 유출하는 것이다.

</br>

**Blind SQL Injection** : Time based SQL

서버로부터 특정한 응답 대신에 참 혹은 거짓의 응답을 통해서 데이터베이스의 정보를 유출하는 기법이다.

```sql
SELECT * FROM Users WHERE id = 'abc123' OR (LENGTH(DATABASE())) = 1 AND SLEEP(2)) --
```

</br>

</br>

### 대응 방안

**입력 값에 대한 검증**

사용자의 입력 값에 대한 검증을 하는 것이다. 예를 들어서 특수문자가 포함되어 있는지 검사하여 허용되지 않은 문자열이나 문자가 포함된 경우에는 모두 에러로 처리한다. 

</br>

**Error Message 노출 금지**

SQL 서버의 에러 메시지를 사용자에게 보여주지 않는 것이다. 이는 Blind SQL Injection를 막을 수 있다. 사용자에게 보여줄 수 있는 에러 메시지가 필요하다면 새로운 페이지를 제작하는 방식으로 해결하면 된다.

</br>

**웹 방화벽 사용**

서버 내에 소프트웨어를 직접 설치하거나 네트워크 상에서 하드웨어 장비로 구성하는 방법이다.