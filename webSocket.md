# webSocket

> websocket

브라우저와 웹서버 간 실시간 양방향 전이중 통신.

웹 서버와 웹 브라우저가 지속적으로 연결된 TCP 라인을 통해 실시간으로 데이터를 주고 받을 수 있는 HTML5의 사양.

ex> 채팅, 게임, 실시간 주식 차트

> webSocket 필요한 경우
- 실시간 양방향 데이터 통신이 필요한 경우
- 많은 수의 동시 접속자를 수용해야 하는 경우
- 브라우저에서 TCP 기반의 통신으로 확장해야 하는 경우
- 개발자에게 사용하기 쉬운 API가 필요할 경우
- 클라우드 환경이나 웹을 넘어 SOA로 확장해야 하는 경우

> webSocket 접속 과정

1. 클라이언트 -> 서버: TCP기반의 Connection을 http로 요청
2. 서버 -> 클라이언트: http 응답
3. 클라이언트 -> 서버: webSocket 연결 요청
4. 서버 -> 클라이언트: "Upgrade" Connection 응답 보냄
5. 클라이언트와 서버 실시간 메세지 전달 가능

1, 2: 일반적인 http 통신.

3, 4: webSocket을 연결하기 위한 핸드쉐이크 과정.


---
## Usage examples

- ### Sending and receiving text data
```javascript
const WebSocket = require('ws');

const ws = new WebSocket('ws://www.host.com/path');

ws.on('open', function open() {
  ws.send('something');
});

ws.on('message', function incoming(data) {
  console.log(data);
});
```
- ### Simple server

```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', function connection(ws) {
  ws.on('message', function incoming(message) {
    console.log('received: %s', message);
  });

  ws.send('something');
});
```

- ### Multiple servers sharing a single HTTP/S server

```javascript
const http = require('http');
const WebSocket = require('ws');
const url = require('url');

const server = http.createServer();
const wss1 = new WebSocket.Server({ noServer: true });
const wss2 = new WebSocket.Server({ noServer: true });

wss1.on('connection', function connection(ws) {
  // ...
});

wss2.on('connection', function connection(ws) {
  // ...
});

server.on('upgrade', function upgrade(request, socket, head) {
  const pathname = url.parse(request.url).pathname;

  if (pathname === '/foo') {
    wss1.handleUpgrade(request, socket, head, function done(ws) {
      wss1.emit('connection', ws, request);
    });
  } else if (pathname === '/bar') {
    wss2.handleUpgrade(request, socket, head, function done(ws) {
      wss2.emit('connection', ws, request);
    });
  } else {
    socket.destroy();
  }
});

server.listen(8080);
```

- ### Client authentication

```javascript
const http = require('http');
const WebSocket = require('ws');

const server = http.createServer();
const wss = new WebSocket.Server({ noServer: true });

wss.on('connection', function connection(ws, request, client) {
  ws.on('message', function message(msg) {
    console.log(`Received message ${msg} from user ${client}`);
  });
});

server.on('upgrade', function upgrade(request, socket, head) {
  // This function is not defined on purpose. Implement it with your own logic.
  authenticate(request, (err, client) => {
    if (err || !client) {
      socket.write('HTTP/1.1 401 Unauthorized\r\n\r\n');
      socket.destroy();
      return;
    }

    wss.handleUpgrade(request, socket, head, function done(ws) {
      wss.emit('connection', ws, request, client);
    });
  });
});

server.listen(8080);
```

