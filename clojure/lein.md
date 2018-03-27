# clojure - leiningen을 쓰다가..



## env

* local에서만 쓰는 환경변수를 파일로 구성하고 싶다.
* 현재 쓰는 luminus를 변형한 템플릿은 lein environ을 사용해 `.lein-env`를 로드해서 쓴다.
* `.lein-env` 는 project.clj 의  env를 읽어서 만든다
* project.clj는 변경하기 싫으므로. 내가 개인 로컬 파일을 추가하는 방법은? 
  * 코드를 살펴보기: https://github.com/weavejester/environ/blob/master/lein-environ/src/lein\_environ/plugin.clj



