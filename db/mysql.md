# mysql

## \[mac\] \[brew\]로 설치한 mysql 클린 삭제하기

* 사정이 있어서 삭제를 하려고 `brew uninstall mysql` \(또는 brew remove mysql\) 하려는데, 제 설치하면 옛날 비번을 물어본다.
* 클린 삭제&설치가 필요하다!!

```bash
# mysql clean 삭제

ps -ax | grep mysql
brew remove mysql
brew cleanup
sudo rm -rf /usr/local/var/mysql
```

이렇게하고 brew install mysql 하면 깔끔하게 새 설치가 된다.

## json 컬럼을 쓰는 table 생성하기

```sql
CREATE TABLE table_name (
    col_name JSON
);
```

## specifc typo \(=&gt; specific\)

[https://github.com/mysql/mysql-connector-j/blob/b3cda4f864902ffdde495b9df93937c3e20009be/src/com/mysql/jdbc/LocalizedErrorMessages.properties](https://github.com/mysql/mysql-connector-j/blob/b3cda4f864902ffdde495b9df93937c3e20009be/src/com/mysql/jdbc/LocalizedErrorMessages.properties)

풀리케날리고싶다. 이슈라도 적고싶다. oracle 가입을 해야해서 매우 허들.

## DB 생성하기 커맨드

```text
create database [DB명];
```

## TIMZONE 확인하기 쿼리

```text
mysql> select now();
+——————————+
| now()               |
+——————————+
| 2018-05-24 15:43:44 |
+——————————+
1 row in set (0.00 sec)

mysql> select @@global.time_zone;
+——————————+
| @@global.time_zone |
+——————————+
| SYSTEM             |
+——————————+
1 row in set (0.00 sec)

mysql>  select @@session.time_zone;
+——————————+
| @@session.time_zone |
+——————————+
| SYSTEM              |
+——————————+
1 row in set (0.00 sec)
```

