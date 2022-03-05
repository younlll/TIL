# com.zaxxer.hikari.pool.HikariPool : HikariPool-2 - Exception during pool initialization.

## 발생원인
```
ERROR 17616 --- [    Test worker] com.zaxxer.hikari.pool.HikariPool        : HikariPool-2 - Exception during pool initialization.
java.sql.SQLNonTransientConnectionException: Could not create connection to database server. Attempted reconnect 3 times. Giving up. 
```

* `데이터베이스 서버에 대한 연결을 생성할 수 없습니다.`라는 오류 이다
* AWS를 통해 배포를 하면서 application.properties에서 spring.datasource.url을 localhost:3306으로 그대로 두고 배포를 진행 했다
* 이후 ./gradlew test를 하며 오류가 발생 했다

<br/>

### 정리할 내용
* Hikari는 Database와의 Connection Pool을 관리해준다


## 해결 방법
`spring.datasource.url=jdbc:mysql://[엔드포인트]:3306/[사용할 데이터베이스 명칭]`으로 변경한 뒤에 ./gradlew test를 진행