# 4.2 예외 전환
* 예외전환의 목적
  * 런타임 예외로 포장해서 굳이 필요하지 않은 catch/throws를 즐겨주는 것이다
  * 로우레벨의 예외를 좀 더 의미 잇고 추상화된 예외로 바꿔서 던져주는 것이다

## JDBC의 한계
* JDBC는 자바를 이용해 DB에 접근하는 방법을 추상화된 API형태로 정의해 놓고 각 DB업체가 JDBC표준을 따라 만들어진 드라이버를 제공해준다
* DB 종류에 상관없이 사용할 수 있는 데이터 엑세스 코드를 작성하는 일은 쉽지 않다
  * 비표준 SLQL
    * SQL은 어느 정도 표준화된 언어이고 몇 가지 표준 규약이 있긴 하지만, 대부분의 DB는 표준을 따르지 않는 표준 문법과 기능을 제공한다
  * 호환성 없는 SQLExceptoin의 DB 에러정보
    * DB를 사용하다 발생할 수 있는 예외의 원인은 다양하다


</br>

## DB에러코드 매핑을 통한 전환
* DB 종류가 바뀌더라도 DAO를 수영하지 않으려면 이 두가지 문제를 해결해야 한다
* SQLException의 비표준 에러 코드와 SQL 상태정보에 대해
  * DB별 에러코드를 참고해서 발생한 예외의 원인이 무엇인지 해석해주는 기능을 만드는 것

</br>

## DAO 인터페이스와 DataAccessException 계층구조
* 계층구조를 이용해 기술에 독립적인 예외를 정의하고 사용하는게 나은지

### 1. DAO 인터페이스와 구현의 분리
* DAO를 따로 만들어서 사용하는 이유는 **데이터 엑세스 로직을 담은 코드에 성격이 다른이유**이다

### 2. 데이터 액세스 예외 추상화와 DataAccessException 계층구조
* JdbcTemplate는 SQLException의 에러 코드를 DB별로 매핑해서 그에 해당하는 의미있는 DaataAccessException의 서브클래스 중 하나로 전환해서 던져준다
* JdbcTemplate과 같이 스프링의 데이터 엑세스 지원 기술을 이용해 DAO를 만들면 사용 기술에 독립적인 일관성 있는 예외를 던질 수 있다

</br>

## 기술에 독립적인 UserDao 만들기
### 1. 인터페이스 적용
* 인터페이스를 구분하기 위해 인터페이스 이름 앞에는 I라는 접두어를 붙이거나 인터페이스 이름은 가장 단순하게 하고 구현 클래스는 각각의 특징을 따르는 이름을 붙이는 경우도 있다

### 2. 테스트 보완
```java
public class UserDaoTest {
    @Autowired
    private UserDao dao;
}
```

* UserDao는 UserDaoJdbc가 구현한 인터페이스이므로 userDaoTest의 dao변수에 UserDaoJdbc 클래스로 정의된 빈을 넣는데 아무런 문제가 없다

### 3. DataAccessException 활용 시 주의사항
* 스프링을 활용하면 DB 종류나 데이터 액세스 기술에 상관없이 키 값이 중복이 되는 상황에서는 동일한 예외가 발생하라고 기대할 것이다
* 하지만 DuplicateKeyExceptoin은 아직까지는 JDBC를 이용하는 경우에만 발생한다
* SQLException 전환 기능의 학습 테스트

```java
@Test
public void sqlExceptionTranslate() {
    dao.deleteAll();

    try {
        dao.add(user1);
        dao.add(user2);
    } catch (DuplicateKeyException ex) {
        SQLException sqlEx = (SQLException)ex.getRootCause();
        SQLExceptionTranslator set = 
            new SQLErrorCodeSQLExceptionTranslator(this.dataSource);

        assertThat(set.translate(null, nullm sqlEx),
            is(DuplicateKeyException.class));
    }
}
```