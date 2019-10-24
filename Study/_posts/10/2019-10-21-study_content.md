---
layout: post
title: Node.js Study (15)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (15)

## Using WebSockets in Node.js
웹소켓은 웹 응용프로그램에서 HTTP 통신의 대안입니다. 오랫동안 존재하는 양방향 채널을 클라이언트와 서버간에 제공합니다. 한번 커넥션이 구축되면 채널은 계속 열리며 낮은 지연과 오베헤드를 가진 빠른 커넥션을 제공합니다.

## Browser support for WebSockets
웹소켓은 모든 현대 브라우저에서 지원됩니다.

## How WebSockets differ from HTTP
HTTP는 매우 다른 프로토콜을 가지고 있고 다양한 방식으로 통신할 수 있습니다. HTTP 리퀘스트/응답 프로토콜은 클라이언트가 요청한 데이터를 서버가 보내주는 것입니다.

웹 소켓은 클라이언트가 명시적으로 뭔가를 요구하지 않아도 클라이언트에게 메시지를 보낼 수 있습니다. 그리고 서로간에 동시에 통신을 할 수 있으며 메시지 교환에 필요한 데이터 오버헤드가 낮습니다. 이말은 통신 지연이 낮다는 말입니다. 웹소켓은 실시간과 오래 지속되는 통신에 좋습니다.

HTTP는 주기적인 데이터 교환이나 클라이언트가 유발하는 인터렉션을 처리하는 데 좋습니다. HTTP는 훨씬 구현하기 쉬운반면에 웹소켓은 오버헤드가 좀 있습니다.

## Secured WebSockets
항상 보안을 주의해야 합니다, 웹소켓에 사용되는 암호화 프로토콜은 wss:// 입니다. ws://는 http와 같이 안전하지 않은 웹소켓 버전이므로 명백한 이유가 있는 것이 아니라면 사용을 지양해야 합니다.

## Create a new WebSockets connection
```
const url = 'wss://myserver.com/something'
const connection = new WebSocket(url)
```
connection은 웹소켓 객체입니다. 커넥션이 성공적으로 구축되면 open 이벤트가 발생합니다. 커넥션 객체의 onopen 프로퍼티에 콜백함수를 할당하여 listen을 합니다.
```
connection.onopen = () => {
  //...
}
```
만약 에러가 있다면 onerror 함수 콜백이 실행됩니다.
```
connection.onerror = error => {
  console.log(\`WebSocket error: ${error}\`)
}
```

## Sending data to the server using WebSockets
한번 커넥션이 열리면 서버에 데이터를 보낼 수 있습니다. 편하게 onopen 콜백 함수 내에서 데이터를 보내면 됩니다.
```
connection.onopen = () => {
  connection.send('hey')
}
```

## Receiving data from the server using WebSockets
onmessage의 콜백 함수는 message 이벤트가 수신되면 호출됩니다.
```
connection.onmessage = e => {
  console.log(e.data)
}
```

## Implement a WebSockets server in Node.js
ws는 Node.js의 유명한 웹소켓 라이브러리 입니다. 우리는 이것을 사용해서 웹소켓 서버를 만들 것입니다. 클라이언트를 만드는 데도 사용될 수 있고 백엔드 서버 두개 사이에서 통신을 하는 데 사용할 수도 있습니다. 다음과 같이 쉽게 설치할 수 있습니다.
```
yarn init
yarn add ws
```
여러분이 작성해야 할 코드는 아주 짧습니다.
```
const WebSocket = require('ws')

const wss = new WebSocket.Server({ port: 8080 })

wss.on('connection', ws => {
  ws.on('message', message => {
    console.log(\`Received message => ${message}\`)
    })
    ws.send('ho!')
})
```
이것은 8080포트로(기본 웹소켓 포트) 새로운 서버를 만들어서 커넥션이 구축되면 콜백함 수를 추가하고 클라이언트에게 ho!라고 보내고 수신된 메시지를 로그로 기록합니다.

## See a live example on Glitch
<a href="https://glitch.com/edit/#!/flavio-websockets-server-example">다음</a>은 웹소켓 서버의 예제입니다.

<a href="https://glitch.com/edit/#!/flavio-websockets-client-example">다음</a>은 서버와 인터렉션하는 웹소켓 클라이언트 예제입니다.

## Working with file descriptors in Node.js
여러분의 파일시스템에 있는 파일과 인터렉티브 하기전에 여러분은 파일 디스크립터를 얻어야만 합니다. 파일 디스크립터는 fs 모듈에서 제공되는 open()메소드를 사용하면 리턴되는 디스크립터입니다.
```
const fs = require('fs')

fs.open('/Users/flavio/test.txt', 'r', (err, fd) => {
  //fd is our file descriptor
  })
```
