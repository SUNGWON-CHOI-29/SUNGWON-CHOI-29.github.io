---
layout: post
title: Node.js Study (9)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (9)

## The Event Loop
이벤트 루프는 자바스크립트를 이해하는 데 가장 중요한 측면 중 하나입니다. 이 영역에서는 자바스크립트가 단일 스레드로써 어떻게 동작하는 지 내부적으로 살펴보고 비동기적으로 함수처리하는 법에 대해서 알아보겠습니다.

저자는 자바스크립트로 몇년간 프로그래밍을 했지만 아직도 내부적으로 어떻게 동작하는지 전체적으로 이해하진 못했습니다. 여기서 개념을 자세하게 알지 못해도 괜찮습니다만 확실히 어떻게 동작하는 지 아는 것이 도움이 되고 여러분도 이부분에 대해서 궁금할 것입니다.

여러분의 자바스크립트 코드는 단일 스레드로 동작합니다. 한번에 한가지 작업만 수행되는 것이죠. 이러한 제한은 실제적으로 매우 도움이되는데 여러분이 동시성 문제에 대해서 걱정하지 않고 프로그램을 할 수 있도록 단순화되기 때문이죠. 여러분은 단지 스레드를 멈추는 것들만 피하는데 집중해서 코드를 작성하면 됩니다. 예를 들면 동기적인 네트워크 호출이나 무한루프같은 것들 말이죠.

일반적으로 많은 브라우저는 각 브라우저 탭마다 이벤트루프가 있고 다른 웹페이지가 무한루프에 빠지거나 무거운 연산을 해도 브라우저 전체가 멈추지 않도록 독립된 프로세스를 가지게 합니다.

해당 환경은 다수의 동시성 이벤트루프를 관리하며 API 호출을 처리합니다. Web Worker 또한 자체적인 이벤트 루프에서 동작합니다. 여러분이 주의해야 할 것은 단일 스레드로 동작하기 때문에 멈추게 되는 것만 피하도록 작성하면 됩니다.
### Blocking the event loop
모든 자바스크립트 코드는 리턴할 때까지 너무 오래걸리면 제어를 이벤트루프에게 돌려주게되고 현재 페이지의 모든 자바스크립트 코드의 실행이 멈출 것입니다. 심징어 UI스레드도 멈추게 되어 페이지 스크롤이나 클릭도 할 수 없게되죠

자바스크립틍의 거의 모든 I/O 기본형들은 논블로킹입니다. 네트워크 요청, Node.js 파일시스템 작업 등등 말이죠. 블로킹되는 것이 예외사항으로 이것이 자바스크립트에서 많은 것을 콜백에 기반하는 것이고 최근에는 프로미스와 async/await에 기반을 둡니다.

### The call stack
콜스택은 LIFO 큐입니다. 이벤트 루프는 지속적으로 콜스택을 검사하여 실행이 필요한 함수가 있는지 확인합니다. 그렇게 하면서 함수호출을 발견하면 콜스택에 추가하고 순서에 따라 하나씩 실해합니다. 여러분은 디버거나 브라우저 콘솔의 에러 스택 추적도 비슷하다는 걸 알고 계시나요?

브라우저는 콜스택의 함수이름을 찾아보고 현재 호출이 어떤 함수에서 발생했는 지 알려줍니다.
<center>
<img src="https://miro.medium.com/max/1184/1*5FlLYTXv01O0R3D3SP3M1Q.png"/>
</center>

### A simple event loop explanation
다음과 같은 예제를 봅시다.
```
const bar = () => console.log('bar')

const baz = () => console.log('baz')

const foo = () => {
  console.log('foo')
  bar()
  baz()
}
foo()

//출력 결과
//foo
//bar
//baz
```
예상대로 출력이 나왔네요. 코드를 실행하면 처음에 foo()가 호출되고 foo()내부에서 처음 bar()가 호출되고 그다음 baz()를 호출합니다. 이 때 콜스택은 다음과 같습니다.

<center>
<img src="https://miro.medium.com/max/2544/1*Jw6-ttv6fWExUrcSV8cqng.png"/>
</center>

이벤트루프는 스택이 비어있을 때까지 매 순회마다 콜스택에 뭔가가 있는지 들여다보고 그것을 실행합니다.
<center>
<img src="https://miro.medium.com/max/932/1*ykBMMZxvxZVJfV3Al9Rp_w.png"/>
</center>

### Queueing function execution
위의 예제는 특별한 것없이 평범해 보입니다. 자바스크립트가 실행할 것을 찾고 순서대로 실행하죠. 다른 함수를 사용해서 스택이 비워질 때까지 확인해 봅시다.

setTimeout( () => {},0)은 함수를 호출하는 데 사용되지만 다른 함수의 코드가 실행되고 난 뒤에 실행됩니다.
```
const bar = () => console.log('bar')

const baz = () => console.log('baz')

const foo = () => {
  console.log('foo')
  setTimeout(bar, 0)
  baz()
}

foo()

//출력 결과
//foo
//baz
//bar
```
이 코드를 실행하면 처음에 foo()가 호출됩니다. foo()내부에서 처음에 bar를 매개변수로 전달하며 setTimeout을 실행하고 우리는 가능한한 즉시 실행되기 위해서 0을 타이머로 설정하였습니다. 그리고나서 baz()가 호출됩니다. 이 때 콜스택은 다음과 같습니다.
<center>
<img src="https://miro.medium.com/max/1888/1*vlVRW5NDB00AtD3ojElTMQ.png"/>
</center>

다음은 프로그램의 모든 함수들의 실행 순서입니다.
<center>
<img src="https://miro.medium.com/max/932/1*ykBMMZxvxZVJfV3Al9Rp_w.png"/>
</center>

왜 이렇게 된걸까요?
### The Message Queue
setTimeout()이 호출되면 브라우저나 Node.js는 타이머를 시작합니다. 이 경우에는 우리가 0을 타임아웃으로 설정하였지만 타이머가 실행되면 콜백함수가 <b>Message Queue</b>에 들어갑니다.

메시지큐는 사용자가 유발하는 이벤트인 클릭이나 키보드 이벤트, 응답 가져오기 등이 queue되어 여러분의 코드가 해당 이벤트에 반응할 기회를 가지게 됩니다. onLoad와 같은 DOM이벤트도 있습니다.

루프는 콜스택에 우선순위를 줍니다. 처음 프로세스는 콜스택에 모든 것을 찾고 아무것도 없으면 그다음 메시지 큐를 봅니다. 우리는 setTimeout과 같은 함수나 fetch 등 스스로 작업하는 것들을 기다릴 필요가 없습니다. 왜냐하면 브라우저에 의해 제공되는 그들 스스로의 스레드가 있기 때문이죠. 예를들어 setTimeout을 2초뒤에 타임아웃 되도록 설정해도 2초를 기다릴 필요가 없습니다. 기다리는 것은 다른 곳에서 발생합니다.

### ES6 Job Queue
ECMAScript 2015는 프로미스를 사용하는 잡큐의 개념을 소개했습니다. 그것은 비동기 함수를 콜스택의 끝에 넣어지는 대신에 바로 실행하는 방식입니다. 현재 함수가 끝나기 전에 resolve된 함수는 현재 함수가 끝난 뒤 바로 실행될 것입니다. 비유를 하자면 놀이공원에서 롤러코스터를 타는 것에 빗댈 수 있습니다. 메시지큐는 여러분을 다른사람들 제일 뒤에 큐에 넣는 반면에 잡큐는 프리패스가 있어서 다음 롤러코스터가 오면 바로 여러분이 탈 수 있도록 하는 것입니다.
```
const bar = () => console.log('bar')

const baz = () => console.log('baz')

const foo = () => {
  console.log('foo')
  setTimeout(bar, 0)
  new Promise((resolve, reject) => {
    resolve('should be right after baz, before bar')
    }).then(resolve => console.log(resolve))
  baz()
}

foo()
//출력결과
//foo
//baz
//should be right after foo, before bar
//bar
```

이것은 프로미스(프로미스를 기반으로 하는 async/await 포함)와 기본 구식 비동기 함수(setTimeout(), 기타 플랫폼 API)와의 큰 차이점 입니다.
