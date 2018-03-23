# Test

## 테스트를 하다가 ByteArrayInputStream 관련 에러를 만남

* `/a/b/c`로의 요청을 했을 때에는 json 으로 응답이 잘 오는데 ring의 mock을 써서 응답을 받으면 ByteArrayInputStream으로 오는 상황

```
#응답 예
:body #object[java.io.ByteArrayInputStream 0x56fae55c java.io.ByteArrayInputStream@56fae55c]
```

### 응답 크기가 영향을 줄 수 있을까?

* [검색 결과](http://baeksupervisor.tistory.com/39) 를 보면 그럴 수도.

  * ByteArrayInputStream 클래스는 바이트 배열을 차례로 읽어들이는 클래스
  * ByteArrayOutputStream 클래스는 내부 저장공간에 바이트 배열을 저장하는 클래스
  * ByteArrayOutputStream의 toByteArray\(\)메소드를 통해 저장공간에 있는 내용을 얻을 수 있다.
  * JVM이 다루는 힙 메모리 사이즈 보다 큰 배열을 사용할 수 없다.

* 테스트를 실수해서 크기가 영향을 받은 것 처럼 보였다...

### mock의 결과가 json인데...

* 당연히 clojure map이라고 착각했다. ~~바보~~
* 이미 app의 리턴으로 json이 나왔을 텐데 map이라고 착각하고 열어보려고 한 죄.
* 내가 비교할 결과를 json-body로 싸거나, (json으로 나온)결과를 map으로 바꾸거나, 모델의 test 를 만들자

```clojure
;; json으로 나온 결과를 map으로 파싱하는 방법
(parse-string (slurp (:body response)) true)
```

### 결론

* 디버그 환경을 좀더 구축하자.
* 어차피 현재는 핸들러 테스트를 하려는 것이지, 로직 테스트는 아니기 때문에 json body를 고치는 것보다 모델의 테스트를 만드는 걸로.
* 결국은 ByteArrayInputStream과는 상관없는 이야기가 되어버렸다. 해당 에러를 보면 내가 어떤 포맷을 보려고 했는지 잘 생각해보자.

## \ㅜn 과 \\n (문자열 escape)

- api개발시 swagger 나 postman 등의 클라이언트request에는 `abc\nd`으로 보내는 것이 test나 clojure 코드 내에서는 `abc\\nd`로 만들어야 같은 문자열로 인식한다.
- escape 문제라는 것은 알겠는데, 계속 헷갈리기에 `clojure.string/split` 함수를 보며 간단히 정리해보자.

```clojure
;; 주의할 점 : 단순히 문자열 \ㅜㅜㅜㅜn을 찾아서 자른 것이 아니다, escape가 동작한 것이다.
(require '[clojure.string :as str])
(def s "a\nbb\\ncccc\\\nd")
(str/split s #"\n")
;; => ["a" "bb\\ncccc\\" "d"]
;; \를 보고 escape 했기 때문에 논리적으로, 공백문자 (\n)를 기준으로 자른 것, 만약 문자열그대로 raw값이라고 판단했다면, bb\rhk cccc도 분리가 되었어야 한다.
(str/split s #"\\n")
;; => ["a\nbb" "cccc\\\nd"]
;; 마찬가지 이유로 문자열 \과 공백문자를 합쳐서 찾아 자른 것이다. cccc 와 d는 왜 분리가 안되었냐면, 역슬래시가 한번 더 escape되었기 때문이다.
(str/split s #"\\\n")
;; => ["a\nbb\\ncccc" "d"]
;; escape가 아닌 역슬래시와 공백을 찾아서 자른 것
(str/split s #"\\\\n")
;; => ["a\nbb\\ncccc\\\nd"]
;; 처음부터 여기 매칭되는 것은 없었다.
```

### 여담

- 내가 클로저를 사용하면서 `(def temp "aaa\n")`와 같이 바인딩을 할 때, escape문자를 쓰지 않고 "aaa\n" 자체를 raw 값으로 바인딩하고 싶지만, 그럴 순 없다. 다른 언어도 대부분 마찬가지 일 것이다. 애초에 string 객체를 만들 때 escape 할테니까.
- https://clojuredocs.org/clojure.string/escape 이런 것도 있지만, 여기선 진짜 문자열 변환이니까 또 다른 문제이다.
- 요청/응답 처리를 할 때, 정신을 똑바로 차리자.

## slurp, stream

```clojure
(let [body (parse-string (slurp (:body response)) true)]
  (println body)
  (println  (slurp (:body response))))
```
- 두개의 print 결과물을 기대했는데, 첫번째 body만 출력된다. 음?
- response 가 stream이고 https://clojuredocs.org/clojure.java.io/input-stream, slurp로 한번 빨아들였기 (?) 때문에, 두번째 slurp에서는 동작하지 않은 것, 값이 여러번 필요할 때는 let으로 적절히 바인딩해서 쓰자.
