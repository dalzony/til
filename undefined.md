# 임시저장페이지

## 보안 참고

* [https://www.slideshare.net/ssuser800974/ss-76664853](https://www.slideshare.net/ssuser800974/ss-76664853)
* 암호화 안한애를 디코딩하면?
* 웹페이지 암호화는 어떻게 되는가?
* [http://myshare.tistory.com/9](http://myshare.tistory.com/9)

웹 페이지 암호화는... 자바 스크립트도 암호화 하는 라이브러리 애들이 있긴 있다. 일반적으로는 HTTPS쓰면 전달은 문제 없는거 같은데 최종은 확인

현재 보이고 있음

## logback

[https://m.blog.naver.com/PostView.nhn?blogId=goddes4&logNo=30130234290&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F](https://m.blog.naver.com/PostView.nhn?blogId=goddes4&logNo=30130234290&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F) [http://jeong-pro.tistory.com/154](http://jeong-pro.tistory.com/154)

\[janino "2.5.15"\]

\*heath\*NEUTRALDENY

return true

NEUTRAL

DENY &lt;/filter&gt;

## exceptions

java.sql.SQLIntegrityConstraintViolationException 를 잡아서 처리하고 싶어 엉엉

[https://github.com/luminus-framework/conman/blob/9e7d3c72958bc4126f660f8b564c9b0e96e75e2d/src/conman/core.clj](https://github.com/luminus-framework/conman/blob/9e7d3c72958bc4126f660f8b564c9b0e96e75e2d/src/conman/core.clj) commna에서 씹음

[https://github.com/luminus-framework/conman/issues/44](https://github.com/luminus-framework/conman/issues/44)

throwble map

\(if \(= \(.getErrorCode \(.getCause e\)\) MysqlErrorNumbers/ER\_DUP\_ENTRY\) \(throw \(ex-info "Duplicated gid target\_name" {:type :duplicated-key}\)\) \(throw e\)\)

\(com.mysql.cj.core.exceptions MysqlErrorNumbers\)

## pkgutil

pkgutil --pkgs uk.co.dssw.powermanager.openpam

## lein deps보기

lein deps :tree

## dynamic var

왜 dynamic var를 db에 쓸까 dynamic var는 언제 바인딩 될까

def나 defn으로 생성한 바인딩은 var의 루트 바인딩으로 모든 스레드에서 공유된다. binding 매크로를 사용하면 스레드에 한정된 var의 바인딩을 만들 수 있다

런타임 중에 변경되지 않는 값을 선언하려는 경우 var를 사용하여  _주위에_ 를 놓습니다. ??

스레드 단위로 값을 변경하려면 var 동적을 선언하십시오.

전역 상태 \(스레드가 아닌\)를 유지하려면 atom , ref \(트랜잭션이 필요한 경우\) 또는 agent \(비동기 변경의 경우\) 중 하나를 사용하십시오.

이에 반해 thread-local binding을 이용하려면, 다음 두 가지 조건을 모두 충족시켜 주어야 한다.

def 선언시 ^:dynamic을 반드시 포함해 주어야 한다.

'binding 매크로 안'에서만 dynamic var를 참조해야 한다.

