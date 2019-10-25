---
layout: post
title: Node.js Study (18)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (18)

## The Node.js http module
http모듈은 HTTP 서버를 만드는데 사용할 수 잇는 유용한 함수와 클래스들을 제공합니다. 해당 모듈은 Node.js 네크워킹의 주요 모듈입니다. 다음과 같이 포함될 수 있습니다.
<center>
```
const http = request('http')
```
</center>
해당 모듈은 클래스, 메소드, 프로퍼티들을 제공합니다.

### Properties
#### http.METHODS
다음은 http 메소드에서 지원되는 모든 프로퍼티의 리스트입니다.

<center>
```
> require('http').METHODS
[ 'ACL',
  'BIND',
  'CHECKOUT',
  'CONNECT',
  'COPY',
  'DELETE',
  'GET',
  'HEAD',
  'LINK',
  'LOCK',
  'M-SEARCH',
  'MERGE',
  'MKACTIVITY',
  'MKCALENDAR',
  'MKCOL',
  'MOVE',
  'NOTIFY',
  'OPTIONS',
  'PATCH',
  'POST',
  'PROPFIND',
  'PROPPATCH',
  'PURGE',
  'PUT',
  'REBIND',
  'REPORT',
  'SEARCH',
  'SUBSCRIBE',
  'TRACE',
  'UNBIND',
  'UNLINK',
  'UNLOCK',
  'UNSUBSCRIBE' ]
```
</center>

#### http.STATUS_CODES
다음은 http status 코드와 설명입니다.

<center>
```
> require('http').STATUS_CODES
{ '100': 'Continue',
  '101': 'Switching Protocols',
  '102': 'Processing',
  '200': 'OK',
  '201': 'Created',
  '202': 'Accepted',
  '203': 'Non-Authoritative Information',
  '204': 'No Content',
  '205': 'Reset Content',
  '206': 'Partial Content',
  '207': 'Multi-Status',
  '208': 'Already Reported',
  '226': 'IM Used',
  '300': 'Multiple Choices',
  '301': 'Moved Permanently',
  '302': 'Found',
  '303': 'See Other',
  '304': 'Not Modified',
  '305': 'Use Proxy',
  '307': 'Temporary Redirect',
  '308': 'Permanent Redirect',
  '400': 'Bad Request',
  '401': 'Unauthorized',
  '402': 'Payment Required',
  '403': 'Forbidden',
  '404': 'Not Found',
  '405': 'Method Not Allowed',
  '406': 'Not Acceptable',
  '407': 'Proxy Authentication Required',
  '408': 'Request Timeout',
  '409': 'Conflict',
  '410': 'Gone',
  '411': 'Length Required',
  '412': 'Precondition Failed',
  '413': 'Payload Too Large',
  '414': 'URI Too Long',
  '415': 'Unsupported Media Type',
  '416': 'Range Not Satisfiable',
  '417': 'Expectation Failed',
  '418': 'I\'m a teapot',
  '421': 'Misdirected Request',
  '422': 'Unprocessable Entity',
  '423': 'Locked',
  '424': 'Failed Dependency',
  '425': 'Unordered Collection',
  '426': 'Upgrade Required',
  '428': 'Precondition Required',
  '429': 'Too Many Requests',
  '431': 'Request Header Fields Too Large',
  '451': 'Unavailable For Legal Reasons',
  '500': 'Internal Server Error',
  '501': 'Not Implemented',
  '502': 'Bad Gateway',
  '503': 'Service Unavailable',
  '504': 'Gateway Timeout',
  '505': 'HTTP Version Not Supported',
  '506': 'Variant Also Negotiates',
  '507': 'Insufficient Storage',
  '508': 'Loop Detected',
  '509': 'Bandwidth Limit Exceeded',
  '510': 'Not Extended',
  '511': 'Network Authentication Required' }
```
</center>

#### http.globalAgent
http.Agent 클래스의 인스턴스로 Agent 객체의 전역 인스턴스를 가리킵니다. connection persistence를 관리하고 HTTP 클라이언트를 재사용하는데 사용되고 노드 HTTP 네트워킹의 핵심 컴포넌트 입니다.

### Methods
#### http.createServer()
http.Server 클래스의 새로운 인스턴스를 리턴합니다.

#### http.request()
http.ClientRequest 클래스의 인스턴스를 생성하고 서버에 HTTP 리퀘스트를 만듭니다.

#### http.get()
http.request()와 비슷하지만 자동적으로 HTTP의 메소드가 GET으로 설정되며 req.end()를 자동적으로 호출합니다.

### Classes
HTTP 모듈은 5개의 클래스들을 제공합니다.

#### http.Agent
노드는 http.Agent 클래스의 전역 인스턴스를 만들고 연결 지속을 관리하고 HTTP clients 재사용 합니다. 노드 HTTP 네트워킹의 핵심 컴포넌트 입니다. 이 객체는 모든 리퀘스트들이 서버에 큐잉 되는 것을 보장하고 싱글 소켓은 재사용 됩니다. 소켓 풀 관리도 담당하는데 이것이 성능의 주요 원인입니다.

#### http.ClientRequest
http.ClientRequest 객체는 http.request()/http.get()이 호출되었을 때 생성됩니다. 응답이 수신되면 response 이벤트가 response와 함께 호출되며 http.IncomingMessage 인스턴스가 매개변수로 같이 옵니다. 리턴된 response 데이터를 읽는 방법에는 두가지가 있습니다. response.read() 메소드를 사용하거나 response 이벤트 핸들러 안에서 data 이벤트에 대한 이벤트 리스너를 만드는 것입니다.

#### http.Server
이 클래스는 주로 http.createServer()를 사용해서 새로운 서버를 만들 때 초기화 되고 리턴됩니다. 한번 서버 객체를 만들면 서버 객체의 메소드에 접근해야 합니다.
* close() - 서버가 새로운 연결을 수락하는 것을 중지합니다
* listen() - HTTp 서버가 연결을 대기하는 것을 시작합니다.

#### http.ServerResponse
http.Server에 의해 만들어지며 request 이벤트가 발생하였을 때 두번째 매개변수로 전달됩니다. 일반적으로 코드에서 res로 사용됩니다. 핸들러 안에서 항상 호출하는 함수는 end()로 응답을 닫고 메시지가 완성이 됩니다. 그리고 서버는 그것을 클라이언트에게 보낼 수 있습니다. end()는 각 response마다 호출되어야 합니다. 다음은 HTTP 헤더와 상호작용 하는 메소드들입니다.
* getHeaderNames() - 이미 설정된 HTTP 헤더들의 이름을 리스트로 받아옵니다.
* getHeaders() - 이미 설정된 HTTP 헤어들의 이름을 복사해옵니다.
* setHeader('headername', values) - HTTP 헤더의 값을 설정합니다.
* getHeader('headername') - 이미 설정된 HTTP 헤더의 값을 가져옵니다.
* removeHeader('headername') - 이미 설정된 HTTP 헤더를 삭제합니다.
* hasHeader('headername') - response가 헤더를 가지고 있다면 true를 리턴합니다.
* headersSent() - 클라이언트에게 보내진 적이 있는 헤더라면 true를 리턴합니다.

헤더 처리작업 후에 여러분은 클라이언트에게 response.writeHead()를 통해 헤더를 보낼 수 있습니다. 첫 매개변수에는 statusCode가 들어가며 상태 메시지는 선택사항이고 그다음에 헤더 객체가 들어갑니다. 클라이언트에게 response body의 데이터를 보내려면 write()를 사용하면 됩니다. HTTP response stream으로 버퍼된 데이터를 보낼 것입니다.

헤더가 response.writeHead()를 이용해서 보내진 적이 없다면 헤더를 먼저 발송할 것입니다. 헤더는 statusCode와 statusMessage 프로퍼의 값을 수정해서 변경할 수 있습니다.

#### http.IncomingMessage
http.IncomingMessage 객체는 http.Server가 request 이벤트에 리스닝 하고 있거나 http.ClientRequest가 response 이벤트에 대해 리스닝하고 있을 때 생성됩니다. 그것은 response에 접근하는데 사용됩니다.
* status - statusCode/statusMessage 메소드를 사용합니다.
* headers - headers 메소드나 rawHeaders를 사용합니다.
* HTTP method - method 메소드를 사용합니다.
* HTTP version - httpVersion 메소드를 사용합니다.
* URL - url 메소드를 사용합니다.
* underlying - socket 메소드를 사용합니다.

데이터는 http.IncomingMessage에 있는 스트림 인터페이스를 이용해 접근해서 읽을 수 있습니다.
