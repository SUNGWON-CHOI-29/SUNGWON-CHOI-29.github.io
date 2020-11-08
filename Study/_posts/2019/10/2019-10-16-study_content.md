---
layout: post
title: Node.js Study (10)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (10)

## Understanding process.nextTick()
Node.js의 이벤트 루프를 이해하기 위한 중요한 부분 중 하나가 process.nextTick()입니다. 그것은 이벤트 루프와 특별한 방식으로 상호작용합니다. 이벤트 루프가 한번 완전히 수행될 때마다 우리는 그것을 tick이라고 부릅니다. process.nextTick()에 함수를 전달하면 다음 이벤트 루프 tick이 시작되기 전에 엔진에게 전달된 함수가 현재 operation의 끝에 실행되도록 할 수 있습니다.
```
process.nextTick( () => {
  //do something
  })
```
이벤트 루프는 현재 함수코드를 busy processing 합니다. 이 operation이 끝이나면 자바스크립트 엔진은 해당 operation동안 nextTick에 넘겨진 모든 함수를 실행합니다. 이것이 우리가 자바스크립트 엔진에게 함수를 비동기적으로 (현재 함수가 끝이난 다음) 실행되도록 하는 방법입니다. 큐에 넣는 것이아니라 가능한 빨리 실행하는 것이죠.

Calling setTimeout(() => {}, 0)은 다음번 tick에서 함수를 실행할 것이기 때문에 nextTick()을 사용하는 것보다 늦게 실행하게 됩니다. nextTick을 사용하면 이벤트 루프가 이미 실행된 코드의 다음을 순회할 것을 보장할 수 있습니다.
## Understanding setImmediate()
여러분이 몇줄의 코드를 비동기적으로 가능한 빨리 실행하고 싶다면 Node.js가 제공하는 setImmediate()를 사용하는 것도 선택지 중 하나입니다.
```
setImmediate(() => {
  //run something
  })
```
setImmediate()의 매개변수로 전달된 콜백은 이벤트 루프의 다음번 순회 때 실행되게 됩니다. setImmediate()가 setTimout(() => {}, 0)이나 process.nextTick()과 어떻게 다를까요?

process.nextTick()으로 전달된 함수는 지금 작업중인 것이 끝나면 현재 이벤트루프의 iteration에서 실행될 것입니다. 이 말은 항상 setTimeout()이나 setImmediate()보다 먼저 실행된다는 것입니다.

0ms 딜레이를 설정한 setTImeout()은 setImmediate()와 매우 유사합니다. 실행 순서는 다양한 요소에 따라 달라지지만 둘다 똑같이 이벤트 루프의 다음번 iteration에 실행됩니다.
## Timers
자바스크립트 코드를 작성할 때 함수의 실행을 지연시키고 싶을 수 있습니다. setTimeout()과 setInterval()로 함수의 실행을 예약하는 법을 배워봅시다.

### setTimeout()
자바스크립트 코드를 작성할 때 함수 실행을 지연시키고 싶다면 setTImeout을 사용하면 됩니다. 나중에 실행될 함수를 콜백으로 지정ㅇ하고 여러분이 얼마나 나중에 실행시키고 싶은지를 밀리세컨드로 표현하여 전달하면 됩니다.
```
setTimeout(() => {
  // 2초뒤 실행
  }, 2000)

setTimeout(() => {
  // 50밀리세컨드 뒤에 실행
  }, 50)
```
이 문법은 새로운 함수를 정의합니다. 거기에 여러분이 원하는 어떤 함수던지 호출할 수 있고 존재하는 함수의 이름을 전달하거나 매개변수 집합을 전달할 수 있습니다.
```
const myFunction = (firstParam, secondParam) => {
  //do something
}
// runs after 2 seconds
setTimeout(myFunction, 2000, firstParam, secondParam)
```
setTimeout()은 타이머 아이디를 리턴합니다. 일반적으로 사용되지 않지만 이 아이디를 저장해놨다가 나중에 예약된 함수실행을 삭제하고 싶을 때 사용할 수 있습니다.
```
const id = setTimeout(() => {
  // should run after 2 seconds
  }, 2000)
clearTimeout(id)
```

### Zero delay
딜레이를 0으로 지정하게 되면 콜백 함수는 현재 함수가 실행된 뒤 가능한한 빨리 실행됩니다.
```
setTimeout(() => {
  console.log('after ')
  }, 0)
console.log(' before ')
//결과
//before after
```
이것은 CPU를 멈출 수 있는 작업을 피하거나 무거운 연산 도중 다른 작업이 실행될 수 있도록 하는데 유용합니다. 함수를 스케줄러의 대기행렬에 넣는 것이죠. IE나 Edge같은 브라우저들은 setImmediate()메소드를 구현해서 같은 기능을 수행합니다만 다른 브라우저에서는 동작하지 않습니다. 그러나 Node.js에서는 표준이죠.

### setInterval()
setInterval()은 setTimeout()과 비슷 하지만 다른점은 함수를 한번 실행하는 것이아니라 여러분이 주기로 지정한 정확한 시간마다 실행된다는 것이죠
```
setInterval(() => {
  //runs every 2 seconds
  }, 2000)
```
위의 함수는 여러분이 setInterval을 수행할 때 리턴된 아이디를 이용하여 clearInterval을 사용해서 멈추지 않는한 2초마다 실행될 것입니다.
```
const id = setInterval(() => {
  //runs every 2 seconds
  }, 2000)
clearInterval(id)
```
일반적으로 clearInterval은 setInterval 콜백함수으 ㅣ내부에서 호출되어 자동적으로 계속 실행될지 아닐지를 판단합니다. 아래의 코드는 App.somethingIWait의 값이 arrived가 될 때까지 코드를 실행합니다.
```
const interval = setInterval(function() {
  if (App.somethingIWait === 'arrived') {
    clearInterval(interval)

    //otherwise do things every 100 ms
  }
  }, 100)
```

### Recursive setTimeout
setInterval은 함수를 매 n 밀리세컨초마다 실행하며 이것은 함수의 실행이 끝난 것을 고려하지 않습니다. 함수가 매번 같은 시간만큼 실행된다면 문제가 되지 않습니다.
<center>
<img src="https://miro.medium.com/max/2390/1*-p6f7BrqUX2YtHsRxf7Clg.png"/>
</center>

네트워크 환경에따라 함수의 실행시간이 달라질 수도 있는 것이죠.
<center>
<img src="https://miro.medium.com/max/2382/1*8q5UStUDhRW6HUSykyK-yQ.png"/>
</center>

그리고 다음번 실행을 덮을 정도로 길게 실행될 수도 있습니다.
<center>
<img src="https://miro.medium.com/max/2380/1*TmTAffufe-DoGf4-t972ag.png"/>
</center>

이것을 피하기 위해 여러분은 재귀적으로 setTimeout을 예약하여 콜백함수가 끝났을 때 호출되도록 할 수 있습니다.
```
const myFunction = () => {
  //do something

  setTimeout(myFunction, 1000)
}
setTimeout(
  myFunction()
  , 1000)
```
<center>
<img src="https://miro.medium.com/max/2378/1*S94HNjZQFg6VP4mXNK3Cng.png"/>
</center>
setTimeout과 setInterval은 Node.js의 Timers 모듈을 통해 사용가능합니다. Node.js는 setImmediate()또한 지원하며 setTimeout(() => {}, 0)과 동일하게 동작하며 Node.js 이벤트루프에서 많이 사용됩니다.
