# nodejs

잠시 쓸일이 생겼다.

## hello World

version 4.x..

https://nodejs.org/docs/latest-v4.x/api/synopsis.html

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

```sh
=> node hello.js
```

## version 에 따른 디펜던시 문제

나는 5.xx를 가지고 있었는데, 4.x..의 프로젝트에서 계속 디펜던시를 못 받아옴

- nvm을 사용하자
- nvm install [version]을 쓰면 해당 로컬 컴퓨터의 환경은 해당 version이 설치되고 설정됨.
