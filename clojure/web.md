# web - 클로저로 웹 개발하다가

* 루미너스와는 디펜던시가 많지 않은 개발사건\(?\)들

## conman 라이브러리 사용시, jdbc driver 에러

루미너스를 사용하지 않고, conman라이브러리를 사용해서 db(mysql)를 연결하려고 하니, 계속 드라이버 관련 에러가 난다.

```
Caused by: java.lang.RuntimeException: Failed to get driver instance for jdbcUrl=jdbc:mysql://localhost:3306/dbname?user=user&password=pw

...

Caused by: java.sql.SQLException: No suitable driver
...
```

 conman이 루미너스의 helper이기 때문에 관련 에러이려나... 했는데, 그게 아니라 mysql을 쓰려면 jdbc 드라이버가 필요한 까닭이었다.
 해당 드라이버를 사용하려면 `[mysql/mysql-connector-java "6.0.5"]`를 project.clj에 디펜던시로 추가하면 된다.

## mysql TIMEZONE 문제

클로저 web api에서 mysql을 연결하려고 했더니

```
Caused by: java.sql.SQLException: The server time zone value 'KST' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.


Caused by: com.zaxxer.hikari.pool.HikariPool$PoolInitializationException: Failed to initialize pool: The server time zone value 'KST' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.


Caused by: com.mysql.cj.core.exceptions.InvalidConnectionAttributeException: The server time zone value 'KST' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the serverTimezone configuration property) to use a more specifc time zone value if you want to utilize time zone support.
```

우선은 jdbc-url에 TIMEZONE(serverTimezone=UTC)을 명시해서 끝냈다.

```clojure
{:jdbc-url (format  "mysql://%s:%s/%s?user=%s&password=%s&serverTimezone=UTC" host port name user password)}
```

5.xx대 부터는 비슷한 문제들이 있어서, KST관련 모듈을 설치해야한다는 말도 있는데, DB전문가(?)의 답변은 일단 KST를 쓰려면 같은 옵션에서 Asia/Seoul을 쓰면 되는 것으로.

```clojure
{:jdbc-url (format  "mysql://%s:%s/%s?user=%s&password=%s&serverTimezone=Asia/Seoul" host port name user password)}
```

- [TIMEZONE 확인 참고](https://dalzony.gitbook.io/til/db/mysql#timzone)

## conmman 라이브러리 사용

### JSON 컬럼을 사용할 때

json컬럼의 값들을 select로 가져왔을때,string으로 결과가 나오고, 이를 클로저 맵으로 변환이 필요했다.
상황은 이랬다.

`hugsql`의 queries.sql에서 select구문을 사용중이고, 응답도 잘 나오는데, swagger-ui에서 계속, 잘못된 포맷이라고 나온다.
해당 쿼리 결과를 잘 보다보니,

```
#결과 찍어봤을때...
[ {:a_key "a-value", :b {"c": "cc", "d": "cccc"}} ....]
```

내가 :b의 value를 json으로 쓰고 있는데, 이것이 string으로 들어간 느낌이 있다.
묘하게 해시맵 같이 생겨서 계속 눈치를 못챈 것 같다.
class 를 찍어보니, 역시나!! `java.lang.String`이다.

자 이제 어떻게할까.

#### parse-string과 익명함수 축제

```
require [cheshire.core :refer [parse-string]])

(def m [ {:a_key "a-value", :b {"c": "cc", "d": "cccc"}} ....])
(map (fn [x] (update x :b (fn [y] (parse-string y (fn [k] (keyword k)))))) m)
```

단순히 parse-string만 쓰고 싶었지만, 그러면 또 string 키의 string 값의 맵이 된다.
keyword 키와, string이 값인 맵을 써야하므로.. 우선 저렇게 구현했는데, parse-string 쪽 함수를 빼는 편이 낫겟지.
conman과  hugsql에서 json 리턴은 알아서 변환해주면 좋으련만..
