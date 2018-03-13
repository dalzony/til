# ByteArrayInputStream

* `/a/b/c`로의 요청을 했을 때에는 json 으로 응답이 잘 오는데 ring의 mock을 써서 응답을 받으면 ByteArrayInputStream으로 오는 상황
* 가정: 응답 크기가 영향을 줄 수 있을까?
* \[검색 결과\] \([http://baeksupervisor.tistory.com/39](http://baeksupervisor.tistory.com/39\)\) 를 보면 그럴 수도.
  * ByteArrayInputStream 클래스는 바이트 배열을 차례로 읽어들이는 클래스
  * ByteArrayOutputStream 클래스는 내부 저장공간에 바이트 배열을 저장하는 클래스
  * ByteArrayOutputStream의 toByteArray\(\)메소드를 통해 저장공간에 있는 내용을 얻을 수 있다.



