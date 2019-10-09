---
layout: post
title: Node.js Study (2)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (2)
## Differences between Node.js and the Browser
Node.js에서 작성된 자바스크립트 프로그램과 브라우저 내에 웹에서 프로그래밍된 것은 어떻게 다를까요? 브라우저와 노드 둘다 자바스크립트를 프로그래밍 언어로 사용합니다. 웹에서 빌드된 앱은 Node.js에서 빌드된 응용프로그랩과 완전히 달라지게 됩니다.

모든 것이 자바스크립트라는 사실에도 불구하고 몇몇 사항들이 다르기 때문에 완전히 경험을 만들어 줍니다. 프론트엔드 개발자들은 Node.js로 앱을 만들면 커다란 장점이 있습니다. 언어가 여전히 동일하다는 것이죠.

우리는 프로그래밍 언어를 깊고 완벽하게 배우는게 얼마나 힘든지 알기 때문에 이것은 큰 장점입니다. 웹에서 클라이언트와 서버쪽의 코드가 동일한 언어라는 것은 매우 큰 이점이 될 것입니다.

다른 점은 환경입니다.

브라우저에서는 많은 시간동안 여러분이 하는 것은 DOM이나 쿠키와 같은 다른 웹플랫폼과 상호작용 하는 것입니다. 물론 그런것들은 Node.js에 없죠. 브라우저에서 제공하는 document, window와 같은 다른 객체도 없습니다.

브라우저에서는 Node.js에서 모듈로 제공하는 좋은 API들이 없습니다. 예를 들면 파일시스템 접근 같은 것들 말이죠.

다른 큰 차이점은 Node.js에서 여러분은 환경을 조정할 수 있다는 것입니다. 오픈소스로 누구나 어디에서 배포할 수 있는 응용프로그램을 만드는 것이 아니라면 여러분은 정확히 어떤 버전의 Node.js가 응용프로그램에서 사용되는지 알겁니다. 방문자가 어떤 브라우저를 사용할건지 선택하지 못하는 브라우저 환경과 달리 이것은 매우 편리합니다.

이 말은 여러분의 Node버전이 지원하는 모든 최신 자바스크립트를 사용할 수 있다는 것입니다.(ES6~ES9) 자바스크립트는 매우 빠르게 업그레이드 되지만 브라우저는 좀 느린편이고 사용자는 천천히 업그레이드 하죠. 때때로 웹에서 오래된 자바스크립트를 가지고 작업을 하는 것은 굉장히 골치아플 겁니다. 여러분의 코드를 브라우저에서 사용되기 전에 Babel을 이용해서 ES5에서 호환이 되도록 할 수도 있지만 Node.js에서는 그럴필요가 없습니다.

다른 차이점은 브라우저에서는 ES 모듈에 표준으로 구현되고 있는 반면에 Node.js는 CommonJS 모듈 시스템을 사용한다는 것입니다. 실제로 이것이 뜻하는 바는 Node.js에서는 require()을 써야하고 브라우저에서는 import를 써야한다는 것입니다.
## The V8 JavaScript Engine
V8은 구글 크롬에서 제공하는 자바스크립트 엔진의 이름입니다. 크롬에서 자바스크립트를 가지고 실행을 해주는 것이죠. V8은 자바스크립트가 실행될 때 런타임 환경을 제공합니다. DOM과 다른 웹 플랫폼 API들은 브라우저에 의해 제공됩니다.

정말 멋진 점은 자바스크립트 엔진은 브라우저에 독립적이라는 것입니다. 이것은 Node.js가 핫해진 중요한 특징입니다. V8은 2009년에 Node.js의 엔진으로 선택되었으며 Node.js의 인기가 커져감에 따라 V8은 자바스크립트로 작성된 많은 엄청난 양의 코드를 동작시키는 엔진이 되었습니다.

Node.js 환경에 거대하기 때문에 V8은 Electron과 같은 데스크탑 앱도 동작시키게 되었습니다.

### Other JS engines
다른 브라우저들도 자체 자바스크립트 엔진이 있습니다.
* Firefox는 <a href="https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey">Spidermonkey</a>
* Safari는 <a href="https://developer.apple.com/documentation/javascriptcore">JavaScriptCore(Nitro)</a>
* Edge는 <a href="https://github.com/Microsoft/ChakraCore">Chakra</a>
물론 다른 것들도 존재합니다.

위의 엔진들은 자바스크립트의 표준으로 쓰이는 ECMAScript(ECMA ES-262)를 구현합니다.
### The quest for performance
V8은 C++로 작성되었고 지속적으로 개선되고 있습니다. V8은 간편하고 Mac, Windows, Linux를 비롯한 다른 시스템에서 동작합니다. 여기서는 V8의 자세한 구현에 대해서는 생략할 것입니다. 그것들은 V8 공식사이트를 포함해서 더욱 권위있는 곳에서 찾아보시길 권장드리며 변경사항도 잦습니다.

V8은 다른 자바스크립트 엔진들이 웹과 Node.js 환경의 속도를 향상시키기 위해 항상 개선을 거듭하고 있습니다. 웹에서는 몇 년간 성능에 대한 경쟁이 있어왔고 그 때문에 사용자 및 개발자들은 이러한 경쟁에서 많인 혜택을 봤습니다. 해를 거듭할 수록 더욱 빠르고 최적화된 것을 얻게 되었으니까요.

### Compilation
자바스크립트는 일반적으로 인터프리터 언어로 해석됩니다. 그러나 최신 자바스크립트 엔진은 단순히 자바스크립트를 해석하는 게 아니라 컴파일도 합니다. 이것은 2009년에 Firefox 3.5에 SpiderMonkey 자바스크립트 컴파일러가 추가되기 시작하면서 모두가 이 아이디어를 따라하기 시작했습니다.

자바스크립트는 실행의 속도를 향상시키기 위해 내부적으로 V8에 의해 just-in-time(JIT) 컴파일 됩니다. 이것은 직관에 상반되는 것처럼 보이지만 구글 맵이 2004년에 출시된 이후 자바스크립트는 단순히 수십줄의 코드를 실행하는 수준에서 브라우저에서 동작하는 수천/수백줄의 완벽한 응용프로그램의 코드가 되었습니다.

우리의 응용프로그램들은 단지 간단한 스크립트나 유효성 체크를 하는 것이 아니라 브라우저 내에서 몇시간 동안 수행될 수 있습니다. 이 새로운 국면에서 자바스크립트 컴파일은 자바스크립트가 준비되는데 조금 더 시간이 걸리긴 하지만 순수하게 해석된 코드보다 더욱 성능이 좋습니다.
## How to exit from a Node.js program
Node.js 프로그램을 끝내는 방법은 여러가지가 있습니다. 콘솔에서 프로그램이 동작하고 있을 땐 ctrl+c로 종료할 수 있지만 제가 여기서 말하고자 하는 것은 프로그래밍적으로 종료하는 것입니다. 가장 과감한 것부터 시작해서 왜 ctrl+c를 사용하지 않는게 좋은지 확인해봅시다.

process코어 모듈은 여러분에게 Node.js프로그램을 프로그래밍적으로 쉽게 종료할 수 있는 메소드를 제공합니다: prcess.exit()

Node.js가 이 코드를 실행하면 프로세스는 즉시 강제적으로 종료됩니다. 이 말은 모든 콜백은 기다리고 있고 모든 네트워크 요청은 보내진 상태며 모든 파일 시스템이 접근되어 있거나 프로세스가 stout/stderr을 작성하는 중입니다. 이런 모든 것들이 꼴사납게 바로 종료될 것입니다.

이 방법이 괜찮다면 여러분은 정수를 전달해서 운영 시스템에 exit code를 알려줄 수 있습니다.
```
process.exit(1)
```
기본적으로 exit code의 값은 0으로 성공을 나타냅니다. 다른 exit code는 다른 의미를 가지고 있으며 여러분의 시스템이 다른 프로그램과 통신을 하고 싶을 경우 사용합니다. exit code에 대한 것은 <a href="https://nodejs.org/api/process.html#process_exit_codes">여기</a>에서 확인할 수 있습니다. 여러분은 process.exitCODE 프로퍼틸를 설정할 수도 있습니다.
```
process.exitCode = 1
```
그리고 나중에 프로그램이 끝나면 Node.js는 exit code를 리턴할 것입니다. 프로그램은 모든 프로세스가 끝이나면 우아하게 종료될 것입니다. 많은 경우 다음과 같은 HTTP 서버를 Node.js에서 서버로 실행합니다.
```
const express = require('express')
const app = express()

app.get('/', (req, res) => {
  res.send('Hi!')
  })

app.listen(3000, () => console.log('Server ready'))
```
이 프로그램은 절대로 종료되지 않습니다. 여러분이 process.exit()를 호출하면 현재 기다리는 작업이나 실행중인 요청이 중단괼 것입니다. 이것은 좋지 않죠. 이 경우에 여러분은 SIGTERM 신호를 보내고 프로세스 시그널 핸들러로 처리할 필요가 있습니다. processsms require를 필요로 하지 않습니다. 자동적으로 사용가능 하다는 것을 기억하세요.
```
const express = require('express')

const app = express()

app.get('/', (req, res) => {
  res.send('Hi!')
  })

app.listen(3000, () => console.log('Server ready'))

process.on('SIGTERM', () => {
  app.close(() => {
    console.log('Process terminated')
    })
  })
```
시그널이 무엇일까요? 시그널은 시스템과 서로 통신하기 위한 Portable Operating System Interface(POSIX)로써 프로세스에게 이벤트가 발생했다는 것을 알려주기 위한 알림입니다.

SIGKILL은 process.exit()와 비슷하게 동작하는 시그널로 프로세스에게 즉시 종료하라고 하는 시그널입니다. SIGTERM은 프로세스에게 우아하게 종료하라는 시그널입니다. SIGTERM은 upstart나 supervisord나 다른 것들처럼 프로세스 매니저로부터 발생되는 시그널 입니다. 프로그램 내부나 다른 함수에서도 이 시그널을 보낼 수 있습니다.
```
process.kill(process.pid, 'SIGTERM')
```
실행되는 다른 Node.js 프로그램이나 시스템에서 동작하는 모든 앱들을 종료키고 싶다면 프로세스의 PID를 알고 있어야합니다.
## How to read environment variables from Node.js
Node의  코어 모듈 process는 프로세스가 시작했을 당시에 모든 환경 변수들을 가지고 있는 env 프로퍼티를 제공합니다. 다음은 환경 변수 NODE_ENV에 접근하는 예제로 그것은 기본적으로 development로 설정됩니다.
```
process.env.NODE_ENV // "development"
```
스크립트가 동작하기 전에 해당 변수를 production으로 설정하면 Node.js에게 이것이 production 환경이라고 알려줄 것입니다. 여러분이 설정한 다른 환경변수도 위와 같은 방법으로 접근할 수 있습니다.
