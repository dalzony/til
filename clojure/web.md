# web - 클로저로 웹 개발하다가

* 루미너스와는 디펜던시가 많지 않은 개발사건\(?\)들

## mysql TIMEZONE 문제

클로저 web api에서 mysql을 연결하려고 했더니

```
Caused by: java.sql.SQLException: The server time zone value 'KST' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.


Caused by: com.zaxxer.hikari.pool.HikariPool$PoolInitializationException: Failed to initialize pool: The server time zone value 'KST' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.


Caused by: com.mysql.cj.core.exceptions.InvalidConnectionAttributeException: The server time zone value 'KST' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.
```

해결방법이 2가지가 있는 것 같은데,(문제해결도 부족한 상황이라) 우선은 jdbc-url에 TIMEZONE(serverTimezone=UTC)을 명시해서 끝냈다.

```clojure
{:jdbc-url (format  "mysql://%s:%s/%s?user=%s&password=%s&serverTimezone=UTC" host port name user password)}
```

자세한 것은 좀더 알아보고 mysql페이지에 정리할 예정.
