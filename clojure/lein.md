# clojure - leiningen을 쓰다가..


개인 파일을 추가해서, 로컬에서는 다른 포트로 서비스를 띄우고 싶음

## env


* local에서만 쓰는 환경변수를 파일로 구성하고 싶다.
* 현재 쓰는 luminus를 변형한 템플릿은 lein environ을 사용해 `.lein-env`를 로드해서 쓴다.
* `.lein-env` 는 project.clj 의  env를 읽어서 만든다
* project.clj는 변경하기 싫으므로. 내가 개인 로컬 파일을 추가하는 방법은?
  * 코드를 살펴보기: https://github.com/weavejester/environ/blob/master/lein-environ/src/lein_environ/plugin.clj
  * http://clojuredocs.org/clojure.java.io/file
  * 결국 위 lein_environ plugin코드를 보면 hooks에서 write-env-to-file 로 쓰는데.. 개인 로컬 파일의 추가는 음.
  * read_env에 로컬 환경 변수를 추가할 여지가 있는지 봐야겠다.
  * 아래 코드를 보면 project에서 :env 키만 읽기 때문에 여지가 없어보임.

```clojure
(defn env-file [project]
  (io/file (:root project) ".lein-env")) ;; 프로젝트 루트에서 .lein-env 라는 파일 객체를 만듦  

(spit "a.txt" "test") ;; a.txt에 test라는 텍스트를 씀

(defn read-env [project]
  (map-vals #(replace-project-keyword % project) (:env project {})))
```

### 끗

- 현재쓰는 템플릿은 프로필을 project.clj에 지정해놓고 쓰는 방식이다.
- main함수의 구현이 서비스 포트 변경은 가능하지만, 기타 다른 환경변수는 파일 하나 추가해서는 불가능한 구조
- `lein run -Daaa-port=1238` 이런것도 luminus에서는 되지만 현재 자체 템플릿에서는 안됨.


```clojure
(defn env []
  (merge-maps (or (load-lein-env) {})
              (source/from-system-props)
              (source/from-env)))
```

### 다시 애매한 부분 추가

- system, 환경이나 from-env로는 못읽는건가 -_-
- System.getenv와  System.getProperty의 차이는 뭐지, 이 두개도 머지를 하는데?
