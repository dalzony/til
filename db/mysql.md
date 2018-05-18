# mysql

##  [mac] [brew]로 설치한 mysql 클린 삭제하기

- 사정이 있어서 삭제를 하려고 `brew uninstall mysql` (또는 brew remove mysql) 하려는데, 제 설치하면 옛날 비번을 물어본다.
- 클린설치가 필요하다!

```sh
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
