---
layout: post
title: Node.js Study (19)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (19)

## Node.js Streams
스트림은 노드 응용프로그램을 동작시키는 기본 개념 중에 하나입니다. 스트림은 파일 읽기/쓰기, 네트워크 통신, 그리고 다른 end-to-end 정보 교환 등을 효율적으로 처리할 수 있는 방식입니다. 스트림은 노드에서만 특별한 개념이 아닙니다. 몇십년 전 유닉스 기반 운영체제에서 소개되었으며 파이프 연산자인 |을 통해 프로그램은 서로 스트림을 주고받으며 상호작용 할 수 있습니다.

예를 들어 고전적으로 프로그램이 파일을 읽을 때 처음부터 끝까지 메모리에서 파일을 읽어오고 그 다음 프로세스를 할 수 있습니다. 스트림을 사용하면 조각 조각 떼에서 읽을 수 있으며 메모리에 모든 걸 넣어두고 프로세싱 하지 않아도 됩니다. 노드는 streaming API들을 구성하는 모든 기본요소를 stream 모듈로 제공합니다.

### Why streams?
스트림은 기본적으로 다른 데이터 처리 방식에 비해 두가지의 주요 장점이 있습니다.
* 메모리 효율성 - 큰 규모의 파일을 프로세싱 하기 전에 메모리에 다 올릴 필요가 없습니다.
* 시간 효율성 - 전체 데이터 페이로드가 사용가능 할 때까지 기다렸다가 시작하는 것이 아니기 때문에 데이터 프로세싱을 더 빠르게 시작할 수 있습니다.

### An example of a stream
전통적인 예제는 디스크로부터 파일을 읽어오는 것입니다. 노드에서 fs모듈을 사용하면 팡ㄹ을 읽을 수 있고 http 서버애서 구축된 새로운 연결이 있을 때 HTTP로 보낼 수 있습니다.

```
const http = require('http')
const fs = require('fs')

const server = http.createServer(function, (req, res) {
  fs.readFile(__dirname + '/data.txt', (err, data) => {
      res.end(data)
    })
  })
server.listen(3000)
```
readfile()은 파일의 전체 내용을 읽어와서 완료되었을 때 콜백을 실행시킵니다. 콜백안에 res.end(data)는 HTTP 클라이언트에게 파일의 내용을 리턴할 것입니다. 파일이 크다면 해당 작업은 시간이 좀 걸릴 것입니다. 다음은 스트림을 사용해서 작성된 똑같은 내용입니다.
<center>
```js
const http = require('http')
const fs = require('fs')

const server = http.createServer((req, res) => {
  const stream = fs.createReadStream(__dirname + '/data.txt')
  stream.pipe(res)
})
server.listen(3000)
```
파일을 전부 읽을 때까지 기다리는 것 대신에 어느정도 데이터가 준비가 되면 클라잉너트에게 바로 데이터를 보내기 시작합니다.
</center>

### pipe()
위의 예제에서 stream.pipe(res) 라인에 있는 pipe()메소드가 파일 스트림에 호출됩니다. 이 코드는 무슨 일을 할까요? 소스를 받아서 파이프로 보내줍니다. 이 경우에는 파일스트림이 HTTP response로 파이프됩니다. pipe() 메소드의 리턴값은 목적지 스트림으로 여러개의 pipe()를 체이닝할 때 매우 편합니다.
<center>
```js
src.pipe(dest1).pipe(dest2)
//same
src.pipe(dest1)
dest1.pipe(dest2)
```
</center>

### Streams-powered Node.js APIs
이런 장점들 때문에 많은 노드 코어 모듈은 네이티브 스트림 처리 능력이 있습니다. 다음은 주요 항목들입니다.
* process.stdin - stdin에 연결된 스트림을 리턴합니다.
* process.stdout - stdout에 연결된 스트림을 리턴합니다.
* process.stderr - stderr에 연결된 스트림을 리턴합니다.
* fs.createReadStream()- 파일을 읽을 수 있는 스트림을 만듭니다.
* fs.createWriteStream() - 파일에 쓸 수 있는 스트림을 만듭니다.
* net.request() - 스트림 기반 연결을 초기화합니다.
* http.request() - 쓰기 가능한 스트림인 http.ClientRequest 클래스의 인스턴스를 리턴합니다.
* zlib.createGzip() - gzip을 이용하여 스트림에서 데이터를 압축합니다.
* zlib.createGunzip() - gzip 스트림을 압축해제 합니다.
* zlib.createDeflate() - deflate 방식을 이용하여 스트림으로 데이터를 압축합니다.
* zlib.createInflate() - deflate 스트림을 압축해제 합니다.

### Different types of streams
4개의 스트림 클래스가 있습니다.
* Readable - 데이터를 받을 수는 있지만 쓰기는 안되는 스트림입니다. 데이터를 읽기 가능한 스트림에 집어 넣으면 사용자가 데이터를 읽기 시작하기 전까지 버퍼됩니다.
* Writable - 쓰기는 가능하지만 읽기는 안되는 스트림입니다.
* Duplex - 읽기/쓰기가 가능한 스트림으로 Readable/Writeable 파이프의 조합입니다.
* Transform - Duplex와 비슷한 스트림이지만 출력이 입력으로 변환됩니다.

### How to create a readable stream
stream 모듈에서 읽기 가능한 스트림을 얻을 수 있고 초기화할 것입니다.
<center>
```js
const Stream = require('stream')
const readableStream = new Stream.Readble()
// 이제 초기화 되었으니 스트림에 데이터를 보낼 수 있습니다
readableStream.push('hi!')
readableStream.push('ho!')
```
</center>

### How to create a writable stream
쓰기 가능한 스트림을 만들기 위해 Writable 객체를 확장해서 \_write() 메소드를 구현할 것입니다.
<center>
```js
//먼저 스트림 객체를 만듭니다
const Stream = require('stram')
const writableStream = new Stream.Writable()
//_write를 구현합니다
writableStream._write = (chunk, encoding, next) => {
  console.log(chunk.toString())
  next()
}
//이제 쓰기 스트림으로 파이프 할 수 있습니다.
process.stdin.pipe(writableStream)
```
</center>

### How to get data from a readble stream
읽기가능한 스트림에서 어떻게 데이터를 읽어올까요? 쓰기가능한 스트림을 사용합시다.
<center>
```js
const Stream = require('stream')

const readableStream = new Stream.Readable()
const writableStream = new Stream.Writable()

writableStream._write = (chunk, encoding, next) => {
  console.log(chunk.toString())
  next()
}

readableStream.pipe(writableStream)

readableStream.push('hi')
readableStream.push('ho')
//readable 이벤트를 이용해서 읽기 가능한 스트림을 직접적으로 소비할 수 있습니다.
readableStream.on('readble', () => {
  console.log(readableStream.read())
})
```
</cemterz>

### How to send data to a writable stream
스트림의 write() 메소드를 사용하면 됩니다.
<center>
```js
writableStream.write('hey!\n')
```
</center>

### Signaling a writable stream that you ended writing
<center>
```js
//end()메소드를 사용합니다.
const Stream = require('stream')

const readableStream = new Stream.Readable()
const writableStream = new Stream.Writable()

writableStream._write = (chunk, encoding, next) => {
  console.log(chunk.toString())
  next()
}

readableStream.pipe(writableStream)

readableStream.push('hi!')
readableStream.push('ho! ')

writableStream.end()
```
</center>
