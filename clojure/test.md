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
* 내가 비교할 결과를 json-body로 싸거나, 모델의 test 를 만들자

### 결론

* 디버그 환경을 좀더 구축하자.
* 어차피 현재는 핸들러 테스트를 하려는 것이지, 로직 테스트는 아니기 때문에 json body를 고치는 것보다 모델의 테스트를 만드는 걸로.
* 결국은 ByteArrayInputStream과는 상관없는 이야기가 되어버렸다. 해당 에러를 보면 내가 어떤 포맷을 보려고 했는지 잘 생각해보자.



