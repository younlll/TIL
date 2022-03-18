# HikariPool-1 - Exception during pool initialization - SQLNonTransientConnectionException

## 발생 원인

```
com.zaxxer.hikari.pool.HikariPool : HikariPool-1 - Exception during pool initialization.
java.sql.SQLNonTransientConnectionException: Could not create connection to database server. Attempted reconnect 3 times. Giving up.
```

* HikariPool-2 - Exception during pool initialization 오류에 대해 앞서 정리 했는데 이어서 HikariPool-1 - Exception during pool initialization 오류가 발생했다
* 1과 2의 숫자 차이는 오류에 대한 코드나 그런게 아니라 관련해서 발생한 오류의 갯수를 말하는거 같기도 하다....(정확한건 찾지 못했음)
* MySQL Database에 접속하기 위해서는 url, databse, driver명, username, password가 필요했는데 8.0이후 부터 보안이슈로 userSSL 옵션이 추가되었다
* 프로젝트를 진행하며 선택한 버전은 8.0.27인데 기존의 옵션들만 설정해주면서 발생한 오류이다
* SQLNonTransientConnectionException -> 공개키 검색이 허용되지 않는다

<br/>

### 정리할 내용
* allowPublicKeyRetrieval: 서버에서 RSA 공개키를 검색하거나 가져오는 것
    * `allowPublicKeyRetrieval=true` 설정을 통해서 공개키 검색을 허용해준다
* useSSL: DB에 SSL로 연결
    * MySQL의 기본값은 SSL 사용값이 true이다
    * 이것을 사용하지 않겠다고 `useSSL=false`를 설정해준다

<br/>

## 해결 방법
```properties
pring.datasource.url=jdbc:mysql://[엔드포인트]:3306/[사용할 데이터베이스]?allowPublicKeyRetrieval=true&useSSL=false&serverTimezone=UTC&characterEncoding=UTF-8
```