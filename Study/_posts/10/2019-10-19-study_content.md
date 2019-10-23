---
layout: post
title: Node.js Study (13)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (13)

## The Node.js Event Emitter
Node.js에서 커스텀 이벤트로 작업을 할 수 있습니다. 브라우저에서 자바스크립트로 작업한다면 이벤트를 통해 얼마나 많은 종류의 사용자 인터랙션이 처리되는지 알 것입니다: 마우스클릭, 키보드 입력, 마우스 움직임 등등..

백엔드 측면에서 Node.js는 이벤트 모듈을 사용해서 비슷하 시스템을 구축할 수 있는 선택지를 제공합니다. 특히 이 모듈이 제공하는 EventEmitter 클래스는 우리가 이벤트를 처리할 때 사용할 것입니다. 다음과 같이 초기화를 할 수 있습ㄴ다.
```
const eventEmitter = require('events').EventEmitter()
```
이 객체는 on과 emit 메소드를 통해 다른 곳에 노출됩니다.
* emit은 이벤트 발생에 사용됩니다.
* on은 이벤트가 발생되었을 때 실행될 콜백함 수를 추가하는 데 사용합니다.

예를 들어 start 이벤트를 만들고 샘플로써 콘솔에 로그를 남길 것입니다.
```
eventEmitter.on('start', () => {
  console.log('started')
})
```
다음을 실행하면 이벤트 핸들러 함수가 실행되고 콘솔에 로그가 남을 것입니다.
```
eventemitter.emit('start')
```
emit()에 추가적인 매개변수를 넣어서 이벤트 핸들러로 매개변수를 전달할 수 있습니다.
```
eventEmiter.on('start', (number) => {
  console.log(\`started ${number}\`)
  })

eventEmitter.emit('start', 23)
// Multiple arguments case

eventEmitter.on('start', (start, end) => {
  console.log(\`started from ${start} to ${end}\`)
  })
eventEmitter.emit('start', 1, 100)
```
EventEmitter 오브젝트는 다른 이벤트들과 상호작용 할 수 있는 다른 메소드들도 제공합니다.

* once(): 일회용 리스너를 추가합니다.
* removeListener() / off(): 이벤트에서 이벤트 리스너를 제거합니다.
* removeAllListeners(): 해당 이벤트에 모든 리스너들을 제거합니다.

## How HTTP requests work
브라우저에 URL을 입력하게 되면 처음부터 끝까지 어떤 일이 발생할까요?

이 섹션에서는 HTTP/1.1 프로토콜을 사용하여 브라우저가 페이지 요청을 처리하는 것을 설명합니다. 만약 면접을 봤다면 다음과 같은 질문을 받았을 수도 있습니다. "구글 검색창에 뭔가를 입력하고 엔터를 치면 어떤 일이 발생하나요?" 이것은 여러분이 받는 질문 중 가장 유명할 것입니다. 면접관들은 여러분이 기본적인 개념을 설명하고 인터넷이 실제로 어떻게 동작하는지 흐름을 알고 있는지 보고싶어 합니다.

여기서는 브라우저 주소창에 URL을 입력하면 어떤 일이 일어나는 지 분석할 것입니다. 이것은 매우 흥미로울 것이고 많은 기술들이 대두될 것입니다. 이 기술은 거의 변하지 않았고 인간이 만든 환경중에 가장 넓고 복잡하고 강력한 것입니다.

## The HTTP protocol
URL 요청들만 분석할 것입니다. 현대 브라우저는 여러분이 주소창에 실제 URL을 입력했는지 검색어를 입력했는지 구분할 수 있는 능력이 있습니다. 그래서 유효한 URL이 아니면 기본 검색엔진을 사용할 것입니다. 여기서는 실제 URL을 입력한 것으로 가정하겠습니다.

URL을 입력하고 엔터를 누르면 먼저 브라우저는 전체 URL을 구성합니다. xingxing.com과 같이 그냥 도메인만 입력했다면 브라우저는 기본적으로 앞에 HTTP://를 붙일 것입니다.

### Things relate to macOS / Linux
그냥 참고로 윈도우에서는 살짝 다르게 동작할 수도 있습니다.

### DNS Lookup phase
브라우저는 서버 IP 주소를 가져오기 위해 DNS를 찾아볼 것입니다. 도메인 이름은 사람에게는 간단하지만 인터넷은 컴퓨터가 아이피 주소를 통해 정확히 어디에 서버가 위치해 있는지 찾을 수 있어야 합니다. IP주소는 222.234.3.1과 같은 숫자 집합입니다.

먼저 로컬 캐시에 DNS를 들여다보고 최근에 resolved된 도메인이 있는지 확인합니다. <b>크롬은 편리한 DNS 캐시 시각화가 있어서 다음의 URL에서 볼 수 있습니다. chrome://net-internals/#dns (copy and paste it in the Chrome browser address bar)</b>

만약 거기에 아무것도 없다면 브라우저는 DNS resolver를 사용해서 gethostbyname POSIX 시스템을 호출해서 호스트 정보를 가져올 것입니다.

### gethostbyname
gethostbyname은 먼저 로컬 호스트 파일을 들여다 봅니다. macOS나 리눅스에서는 /etc/hosts에 있습니다. 시스템이 해당 정보를 지역적으로 제공하는지 확인합니다. 도메인에 대한 정보가 아무것도 없다면 시스템은 DNS 서버에 요청을 합니다.

DNS 서버의 주소는 시스템 프레퍼런스에 저장되어 있습니다. 다음은 유명한 2개의 DNS 서버입니다.
* 8.8.8.8: 구글 퍼블릭 DNS 서버
* 1.1.1.1: CloudFlare DNS 서버

대개 사람들이 사용하는 DNS 서버는 해당 인터넷 공급자가 제공하는 DNS 서버를 사용합니다. 브라우저는 DNS 리퀘스트를 UDP 프로토콜을 사용해서 요청합니다. TCP와 UDP는 기본적인 컴퓨터 네트워킹 프로토콜입니다. 그것들은 개념적으로 같은 수준이지만 TCP는 커넥션 기반이고 UDP는 커넥션 리스 프로토콜로 더욱 가볍고 오버헤드가 적은 메시지를 보내는 데 사용됩니다.

UDP 리퀘스트가 어떻게 동작하는 지는 여기서 다루지 않습니다.(추후 찾아볼 것)

DNS 서버는 도메인 IP를 캐시에 가지고 있을 수도 있습니다. 만약 없다면 <b>root DNS server</b>에 물어봅니다. 해당 시스템은 13개의 실제 서버로 구성되어 있고 전 세계적으로 분산되어 있습니다. 그리고 전체 인터넷을 돌아다닙니다.

DNS 서버는 지구에 모든 도메인 이름에 대한 주소를 알고 있는 것이 아닙니다. 걔네들이 아는 것은 상위 레벨의 DNS resolvers가 어디있는 지 아는 것입니다. 상위 레벨 domain은 .com, .it, .pizza와 같이 도메인 확장입니다.

일단 root DNS 서버가 요청을 받으면 top-level domain(TLD) DNS 서버로 요청을 포워딩 합니다. 만약 xingxing.com을 찾는 중이라면 root 도메인 DNS 서버는 .com TLD 서버의 IP 주소를 리턴할 것입니다.

이제 우리 DNS resolver는 TLD 서버의 IP를 캐싱할 것이고 나중에 또 다시 root DNS 서버에 물어볼 필요가 없게 됩니다. TLD DNS 서버는 우리가 찾고 있는 도메인에 대한 믿을만한 네임서버의 주소를 가지고 있을 것입니다.

도메인을 구입하면 도메인 레지스터가 적절한 TDL에게 네임 서버를 전달합니다. 네임 서버를 업데이트 하면 이 정보는 자동적으로 여러분의 도메인 레지스터에 업데이트 됩니다. 저런 것들은 호스팅 제공자의 DNS 서버입니다. 백업 용으로 1개 이상 보통 존재하죠.

DNS resolver는 처음부터 시작해서 여러분이 찾고 있는 도메인의 IP를 요청할 것입니다. 이것이 IP 주소의 진실에 대한 궁극적인 근본입니다. 이제 IP주소를 얻게 되었으니 다음을 진행해 봅시다.

### TCP request handshaking
사용가능한 서버 IP를 가지고 브라우저는 TCP 연결을 시도합니다. TCP 연결은 데이터를 보내기 시작하기 전에 3-way 핸드쉐이킹을 요구하고 그것을 통해 전체적으로 초기화가 될수 있는지 확인합니다. 한번 연결이 구축되면 리퀘스트를 보낼 수 있습니다.

### Sending the request
요청은 통신 프로토콜에 의해 정확하게 결정된 일반 텍스트 구조입니다. 리퀘스트는 세가지 부분으로 구성됩니다.
* request line
* request header
* request body

### The request line
request line은 한줄로 설정됩니다.
* the HTTP method
* the resource location
* the protocol version

```
GET / HTTP/1.1
```

### The request header
리퀘스트 헤더는 field: value의 쌍으로 특정 값들의 집합입니다. 2가지 주요 필드가 있는데 하나는 호스트이고 다른 것은 커넥션 입니다. 다른 필드는 선택사항입니다
```
Host: xingxing.com
Connection: close
```
호스트는 여러분이 목표로하는 도메인 이름을 가리키고 커넥션은 반드시 열려진 상태로 유지되어야 할 것이 아니라면 항상 close로 설정됩니다. 자주 사용되는 다른 헤더 필드는 다음과 같습니다.
* Origin
* Accept
* Accept-Encoding
* Cookie
* Cache-Control
* Dnt

다른 것도 매우 많습니다. 헤더 부분은 공백에 의해 종료됩니다.

### The request body
리퀘스트 바디는 선택 사항이고 GET 리퀘스트에서는 사용되지 않지만 POST 리퀘스트나 다른 것에는 많이 사용되고 JSON 형태로 데이터를 담을 수 있습니다. 우리는 지금 GET 리퀘스트를 분석하고 있고 body가 비어있기 때문에 더 들여다보진 않겠습니다.

### The response
일단 request기 보내지면 서버는 응답을 보내옵니다. 응답은 status code와 status message로 시작합니다. 만약에 성공적이었다면 200을 리턴하고 다음과 같이 시작합니다
```
200 OK
```
리퀘스트는 다른 status code와 메시지들을 보낼 수 있습니다.
```
404 Not Found
403 Forbidden
301 Moved Permanently
500 Internal Server Error
304 Not Modified
401 Unauthorized
```
응답은 HTTP 헤더들과 response body의 리스트를 가지고 있습니다.
### Parse the HTML
브라우저는 이제 수신된 HTML을 가지게 되었고 그것을 파싱하기 시작하면서 다른 자원들에 대해서도 같은 프로세스를 반복할 것입니다.
* CSS files
* images
* JavaScript files

브라우저가 어떻게 페이지를 렌더링 하는 지는 해당 포스트의 영역을 넘어서지만 해당 프로세스를 이해하는 것이 매우 중요하기 때문에 그냥 HTML 페이지가 아니라 아이템을 조금 가지고 있는 것을 설명하겠습니다.
