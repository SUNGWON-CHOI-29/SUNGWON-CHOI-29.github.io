---
layout: post
title: Basic of the JavaScript (3)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Basic of the JavaScript (3)
## Asynchronous programming
<a href="https://flaviocopes.com/javascript-callbacks/"> Asynchronous programming and callbacks </a>

### Asynchroicity in Programming Languages
컴퓨터는 비동기적으로 설계되어 있습니다. 비동기화의 의미는 메인 프로그램의 흐름과 독립적으로 작업이 수행될 수 있다는 것입니다. 현재 일반 컴퓨터에서는 모든 프로그램은 특정 타임슬롯에서만 실행되고 멈춥니다. 그리고 다른 프로그램이 계속 실행됩니다. 이러한 동작 사이클은 매우 빠르기 때문에 알아차릴 수 없어서 우리는 컴퓨터의 많은 프로그램이 동시에 동작하는 것처럼 느껴집니다. 그러나 이건 착각이죠(멀티프로세스 머신에서는 다릅니다.)

프로그램은 내부적으로 인터럽트를 사용합니다. 시스템으로부터 관심을 받은 프로세서에게 신호를 주는 것이죠.

비동기화의 내부적으로 깊이 들어가고 싶지 않지만 단지 프로그램의 비동기화는 일반적 것이고 프로그램이 다시 시스템의 자원을 사용할 수 있을 때까지 멈추고 컴퓨터는 그동안 다른 것을 수행한다는 것을 기억하세요. 프로그램이 네트워크 응답을 기다리는 중에는 응답이 끝날 때까지 프로세스가 멈출 수 없습니다.

일반적으로 프로그래밍언어는 동기화되어 언아차원 혹은 라이브러리들을 통해 비동기화를 관리할 수 있는 방법을 제공합니다. C,Java,C#, PHP, Go, Ruby, Python들은 동기화가 기본입니다. 이 언어중 몇몇은 비동기를 쓰레드를 이용해서 처리합니다.

### JavaScript
자바스크립트는 기본적으로 동기화 되어 있으며 단을 스레드 입니다. 이 말은 코드가 쓰레드를 만들어 병렬적으로 수행될 수 없다는 것이죠. 코드 라인은 순서대로 실행됩니다. 하나가 실행되고 그 다음이 실행되죠

```
const a = 1
const b = 2
const c = a * b
console.log(c)
doSomething()
```
그러나 자바스크립트는 브라우저 내에서 탄생했으며 최초 주요 사용처는 onClick, onMouseOver, onChange, onSubmit과 같은 사용자 액션에 응답하는 것이었습니다. 동기화 프로그래밍 모델을 가지고 어떻게 이 작업을 수행할 수 있을까요?

정답은 자바스크립트의 환경입니다. 브라우저는 이런 종류의 기능을 처리할 수 있는 API들을 제공함으로써 해결할 수 있도록합니다.

최근에 Node.js는 이러한 개념을 파일접근, 네트워크 호출 등에도 확장하여 논블로킹 I/O 환경을 소개했습니다.

### Callbacks
여러분은 사용자가 언제 버튼을 클릭할 지 알 수 없습니다. 따라서 여러분이 해야할 것은 클릭 이벤트를 위한 이벤트 핸들러를 정의하는 것입니다. 이 이벤트 핸들러는 함수를 매개변수로 받아서 해당 이벤트가 발생하면 그 함수를 호출할 것입니다.
```
document.getElementById('button').addEventListener('click', () => {
    //item clicked
  })
```
이것이 콜백이라는 것입니다.

콜백은 다른 함수에 값처럼 전달되는 간단한 함수로서 이벤트가 발생했을 때만 실행됩니다. 자바스크립트가 일급 클래스 함수를 가지고 있어서 이렇게 변수에 할당하거나 다른 함수에 전달할 수 있습니다.

여러분의 모든 클라이언트 코드를 window객체에 load 이벤트 리스너로 감싸는 것은 일반적입니다. 그러면 페이지가 준비되었을 때만 콜백이 실행됩니다.
```
window.addEventListener('load', () => {
    //window loaded
    //do what you want
}
```
콜백은 DOM이벤트를 제외하고 어디서나 사용될 수 있습니다. 또 다른 일반적인 사용은 타이머속에 사용되는 것입니다.
```
setTimeout(() => {
    //runs after 2 seconds
  }, 2000)
```
XHR 리퀘스트도 콜백을 받으며 이 예제에서는 함수를 프로퍼티에 할당하여 특정 이벤트가 발생했을 떄 호출되도록 할 것입니다.(이 경우에는 요청의 상태가 변경됩니다.)
```
const xhr = new XHMHttpRequest()
xhr.onreadystatechange = () => {
  if (xhr.readyState === 4) {
    xhr.state === 200 ? console.log(xhr.reponseText) :
    console.error('error')
  }
}
xhr.open('GET', 'https://yoursite.com')
xhr.send()
```
### Handling errors in callbacks
콜백의 에러는 어떻게 처리할까요? 가장 일반적인 방법은 Node.js에서 채택한 것입니다. 콜백 함수의 첫 매개변수를 에러 객체로 하는 것입니다. 이것은 error-first 콜백입니다.

만약 에러가 없다면 그 객체는 null이 될 것이고 에러가 있다면 에러와 다른 정보에 대한 디스크립션을 가지게 될 것입니다.
```
fs.readFile('/file.json', (err, data) => {
  if (err !== null) {
    //handle error
    console.log(err)
    return
  }

  //no errors, process data
  console.log(data)
  })
```
### The problem with callbacks
콜백은 매우 간단한 경우에 좋습니다. 그러나 많은 콜백들이 중첩되는 경우나 콜백이 많은 경우 코드는 급격하게 복잡해집니다.
```
window.addEventListener('load', () => {
  document.getElementById('button').addEventListener('click', () => {
    setTimeout(() => {
      items.forEach(item => {
        //your code here
        })
      }, 2000)
    })
}
```
이것은 단지 4계층의 구조이지만 더 단계가 많아지면 심각해 질겁니다. 이걸 어떻게 해결할 수 있을까요?
### Alternatives to callbacks
ES6에서는 콜백을 사용하지 않는 몇몇 비동기 피쳐들을 소개했습니다. 바로 Promises와 Async/Await입니다.

<a href="https://flaviocopes.com/javascript-timers/"> JavaScript Timers </a>

### setTimeout()
자바스크립트로 코드를 작성할 때 여러분은 함수의 실행을 지연시키고 싶을 수 있습니다. 이것은 setTimeout이 수행합니다. 나중에 실행될 함수를 콜백에 지정하고 밀리세컨드 단위로 얼마나 기다릴지 표현하면 됩니다.
```
setTimeout(() => {
  // runs after 2 seconds
}, 2000)

setTImeout(() => {
  //runs after 50 miliseconds
}, 50)
```
이 문법은 새로운 함수를 정의합니다. 다른 어떤 함수를 원하든 호출할 수 있고 매개변수로 설정해서 함수의 이름을 전달할 수 있습니다.
```
const myFunction = (firstParam, secondParam) => {
  // do something
}

//runs after 2 seconds
setTimeout(myFunction, 2000, firstParam, secondParam)
```
setTImeout은 타이머 아이디를 리턴합니다. 일반적으로는 쓰이지 않지만 여러분은 id를 저장하여 여러분이 원할 때 이 함수 실행 일정을 삭제할 수 있습니다.
```
const id = setTimeout(() => {
  // should run after 2 seconds
  }, 2000)
//I changed my mind
clearTimeout(id)
```

### Zero delay
여러분이 타임아웃 딜레이를 0으로 설정했다면 콜백은 가능한한 바로 실행될 것입니다. 그러나 현재 함수 다음에 실행됩니다.
```
setTimeout(() => {
  console.log('after ')
  }, 0)
  console.log(' before')
  //will print before after.
```
이것은 특별히 집중적인 작업을 수행할 때 CPU가 블록되는 것을 피하거나 무거운 연산을 수행중 일 때 다른 함수가 실행될 수 있게 할 수 있어서 유용합니다. 스케줄러에 함수를 큐잉하는 것이죠. IE나 엣지같은 브라우저들은 setImmediate() 메소드를 구현하여 같은 일을 수행합니다 그러나 이것은 다른 브라우저에서는 동작하지 않습니다. 그러나 Node.js에서는 표준함수 입니다.
### setInterval()
setInterval은 setTimeout과 비슷하지만 다른 점이 있습니다. 콜백을 한번 실행하는 것 대신에 지정된 인터벌 시간에 따라서 무한히 콜백함수를 실행하는 것입니다.
```
setInterval(() => {
  //runs every 2 seconds
  }, 2000)
```
위의 함수는 setInterval을 사용할 때 리턴된 인터벌 id값을 사용하여 clearInterval을 사용하지 않는한 2초마다 계속해서 실행될 것입니다.
```
const id = setInterval(() => {
  //runs every 2 seconds
  }, 2000)
  clearInterval(id)
```
일반적으로 setInterval 콜백함수 내에서 clearInterval을 호출합니다. 자동적으로 멈출 지 계속 수행할 지 결정할 수 있게 하기 위함입니다. 아래의 코드는 arrived 밸류를 가질 때 까지 게속 동작합니다.
```
const interval = setInterval(() => {
  if(App.somethingIWait === 'arrived') {
    clearInterval(interval)
    return
  }
  // otherwise ddo things
  }, 100)
```

### Recursive setTimeout
setInterval은 매 n밀리세켠드마다 함수의 실행이 끝났는지 확인하지 않고 그냥 실행됩니다. 만약 함수가 항상 같은 시간만큼 동작한다면 괜찮습니다.
<center>
<img src="https://flaviocopes.com/javascript-timers/setinterval-ok.png"/>
</center>

그러나 예제처럼 함수가 네트워크 상황에 따라 다른 실행 시간을 가질 수 있습니다.
<center>
<img src="https://flaviocopes.com/javascript-timers/setinterval-varying-duration.png"/>
</center>

그리고 긴 실행시간이 다음 실행을 덮을 수도 있죠.
<center>
<img src="https://flaviocopes.com/javascript-timers/setinterval-overlapping.png"/>
</center>

이것을 피하기 위해 콜백 함수가 끝난 경우 recursive setTImeout을 호출할 수 있습니다.

```
const myFunction = () => {
  // do something
  setTimeout(myFunction, 1000)
}

setTimeout( () => {
  myFunction()
  }, 1000)
```

<center>
<img src="https://flaviocopes.com/javascript-timers/recursive-settimeout.png"/>
</center>
setTimeout과 setInterval은 Node.js에서 Timers module을 통해 사용할 수 있습니다. Node.js는 또한 setImmediate를 제공하여 setTimeout(()=> {},0)과 동일한 작업을 수행할 수 있습니다.

<a href="https://flaviocopes.com/javascript-promises/"> JavScript Promises </a>

### Introduction to promises
프로미스는 일반적으로 언젠가는 변하게 될 값을 대리로 정의합니다. 프로미스는 많은 콜백을 사용하지 않고 비동기 코드와 작업할 수 있는 한가지 방법입니다. 몇 년밖에 되지 않았지만 ES2015에서 표준으로 소개되었고 ES2017에서는 비동기 함수로서 자리매김 했습니다. 어싱크 함수는 프로미스 API를 빌딩블록으로 사용하기 떄문에 여러분들이 프로미스 대신에 어싱크 함수를 사용한다고 해도 프로미스에 대한 기본적인 이해가 필요합니다.
### How promises work, in brief
한번 프로미스가 호출되면 펜딩 상태에 진입합니다. 이 말은 약속된 작업을 하도록 기다리는 동안 콜러 함수가 실행을 계속한다는 말이며 콜러함수에게 피드백을 전달합니다. 이 때 콜러 함수는 프로미스가 resolved/rejected 상태를 리턴하는 것을 기다리지만 프로미스가 작업을 하는 동안 함수는 계속 실행됩니다.

### Which JS API use promises?
여러분의 코드와 라이브러리 코드를 포함하여 프로미스는 다음과 같은 최신 Web API표준에 사용됩니다.
* Battery overlapping
* Fetch API
* Service Workers
최신 자바스크립트에서는 프로미스를 사용하지 않으므로 바로 프로미스에 대해 더욱 알아봅시다.

### Creating a promise
프로미스 API는 프로미스 생성자를 통해 초기화 할 수 있도록 합니다. new Promise()
```
let done = true

const isItDoneYet = new Promise((resolve, reject) => {
  if (done) {
    const workDone = 'Here is the thing I built'
    resolve(workDOne)
  } else {
    const why = 'Still working on something else'
    reject(why)
  }
  })
```
보시다시피 프로미스는 글로벌 상수 done을 검사하고 true일 경우 해결된 프로미스를 리턴하고 그렇지 않을 경우 거절된 프로미스를 리턴합니다. resolve와 reject를 사용해서 우리는 값과 다시 통신할 수 있으며 위의 경우에는 단순히 문자열을 리턴하지만 객체가 될 수도 있습니다.
### Consuming a promise
우리는 어떻게 프로미스를 만드는지 살펴봤습니다. 이제는 어떻게 프로미스를 소비하는지 알아보겠습니다.
```
const isItDoneYet = new Promise()
//...

const checkIfItsDone = () => {
  isItDoneYet
  .then(ok => {
    console.log(ok)
  })
  .catch(err => {
    console.error(err)
  })
}
```
checkIfItsDone함수를 실행하면 isItDoneYet() 프로미스를 실행하고 then 콜백을 사용하여 resolve되길 기다릴 것입니다. 그리고 에러가 있다면 catch 콜백에서 처리될 것입니다.

### Chaining promises
프로미스는 프로미스 체인을 만들어서 또 다른 프로미스를 리턴할 수 있습니다. 가장 좋은 예제는 Fetch API 입니다. XMLHttpRequestAPi의 상위 레이어로서 리소스를 가져오는데 사용할 수 있고 리소스를 가져올 때 프로미스 체인을 큐잉할 수 잇습니다. FetchAPI는 프로미스 기반의 메커니즘으로 fetch()를 호출하는 것은 new Promise를 정의하는 것과 동일합니다.
### Example of chaining promises

```
const status = response => {
  if (response.status) >= 200 && response.status < 300) {
    return Promise.resolve(response)
  }
  return Promise.reject(new Error(response.statusText))
}

const json = response => response.json()

fetch('/todos.json')
  .then(status)
  .then(json)
  .then(data => {
    console.log('Request succeeded with JSON response', data)
  })
  .catch(error => {
    console.log('Request failed', error)
  })
```
이 예제에서 우리는 도메인 루트에 있는 todos.josn 파일에서 TODO 리스트의 아이템을 가져오기 위해 fetch()를 호출합니다. 그리고 프로미스 체인을 만듭니다.

fetch()를 실행하면 response를 리턴하는데 많은 프로퍼티를 가지고 있고 그 중에 우리가 조회할 것은 다음과 같습니다.
* status, HTTP 상태 코드를 나타내는 숫자입니다.
* statusText, 상태메시지로 리퀘스트가 성공이라면 OK를 나타냅니다.
응답은 json()메소드를 가지고 있는데 프로미스를 리턴합니다. 프로미스에는 JSON 형태로 변환된 처리된 본문의 내용이 있습니다. 그래서 주어진 프로미스들은 다음과 같은 일이 발생합니다. 체인의 처음 프로미스는 우리가 정의한 status()입니다. 응답의 상태를 검사하여 성공이 아니라면(200~299 사이) 프로미스를 거절합니다.

이 동작은 나열된 체인프로미스들을 모두 지나쳐서 아래의 catch 구문으로 가서 에러메시지와 함께 Request failed를 기록할 것입니다.

성공했을 경우 우리가 정의한 json()함수를 호출할 것입니다. 이전의 프로미스가 성공적이었다면 response 객체를 리턴할 것이고 다음 프로미스에 넘겨줄 것입니다. 이 경우에 우리는 JSON 처리된 데이터를 리턴 받게 되며 세번째 프로미스는 JSON을 바로 받게 됩니다.
```
.then((data) => {
  console.log('Request succeeded with JSON response', data)
  })
```
그리고 콘솔에 기록을 합니다.
### Handling errors
위의 예제에서는 프로미스 체인에 추가된 catch가 있었씁니다. 프로미스 체인의 어떤 것이라도 실패하거나 에러를 일으키거나 프로미스가 거절되면 컨트롤은 가장 가까운 catch() 구문으로 내려갑니다.
```
new Promise((resolve, reject) => {
  throw new Error('Error')
  }).catch(err => {
    console.error(err)
  })

//or

new Promise((resolve, reject) => {
  reject('Error')
  }).catch(err => {
    console.error(err)
  })
```
### Cascading errors
캐치 구문에서 에러가 발생했다면 두번째 catch()를 추가해서 계속해서 처리할 수 있습니다.
```
new Promise((resolve, reject) => {
  throw new Error('Error')
  })
  .catch(err => {
    throw new Error('Error')
  })
  .catch(err => {
    console.error(err)
  })
```
### Orchestrating promises
#### Promise.all()
여러분이 모든 프로미스를 동기화할 필요가 있다면 Promise.all()이 프로미스 리스트를 정의하고 그들이 모두 resolved되었을 때 뭔가를 실행하도록 정의하는데 도움이 될 것입니다.

```
const f1 = fetch('/something.json')
const f2 = fetch('/something2.json')

Promise.all([f1, f2])
  .then(res => {
    console.log('Array of results', res)
  })
  .catch(err => {
    console.error(err)
  })
```
ES2015 비구조 할당 문법은 다음과 같이 사용할 수 있습니다.
```
Promise.all([f1, f2]).then(([res1, res2]) => {
  console.log('Result', res1, res2)
  })
```
물론 fetch에만 사용해야 되는 것이 아니라 어떤 프로미스에서도 사용할 수 있습니다.
#### Promise.race()
Promise.race()는 하나의 프로미스라도 resolve가 되면 실행이 되며 해당 프로미스의 결과로 부착된 콜백을 실행합니다.
```
const promiseOne = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, 'one')
  })
const promiseTwo = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'two')
  })
Promise.race([promiseOne, promiseTwo]).then(result => {
  console.log(result) // two
  })
```
### Common errors
만약 여러분이 Uncaught TypeError: undefined is not a promise 에러를 콘솔에서 받게 된다면 Promise() 대신에 new Promise()를 사용했는지 확인해보세요.

<a href="https://flaviocopes.com/javascript-async-await"> Async and Await </a>

### Introduction
자바스크립트는 매우 짧은 기간에 콜백에서 프로미스까지 개선되었습니다. 그리고 ES2017 이후로 자바스크립트에서 비동기화는 async/await 문법으로 더욱 간단해 졌습니다. 비동기 함수들은 프로미스와 생성자들의 조합입니다. 기본적으로 프로미스 상위의 추상화 단계입니다. 다시한번 강조드립니다. <b>async/await는 프로미스를 기반으로 합니다. </b>
### Why were async/await introduced?
그들은 프로미스 주변의 boilerplate와 프로미스 체인의 제한(don't break the chain)을 감소시켰습니다. ES2015에서 프로미스는 비동기화 코드의 문제를 해결하기 위해 소개되었습니다. 정말로 그랬지만 2년 후 ES2015와 ES2017로 분리되었을 때 프로미스가 마지막 해결책이 될 수 없다는 게 명백해졌습니다.

프로미스는 유명한 콜백 지옥 문제를 해결하기 위해 소개되었지만 그들 스스로의 복잡성과 문법 복잡도가 있었습니다. 개발자들에게 더욱 좋은 문법으로 알려질 수 있는 좋은 기본형이었고 그래서 결국 우리는 비동기 함수를 갖게 되었습니다.

비동기 함수는 동기된 코드처럼 보이지만 뒤쪽에서는 비동기적이고 논블로킹으로 동작합니다.

### How it works
아래의 예제처럼 비동기 함수는 프로미스를 리턴합니다.
```
const doSomethingAsync = () => {
  return new Promise(resolve => {
    setTImeout(() => resolve('I did something'), 3000)
    })
}
```
이 함수를 호출하고 싶다면 여러분은 앞에 await를 사용해야 하며 호출된 코드는 프로미스가 해결되거나 거절될 때까지 멈출 것입니다. 클라이언트 함수는 async로 정의되어야 합니다.
```
const doSomething = async () => {
  console.log(await doSomethingAsync())
}
```
### A quick example
함수를 비동기적으로 실행시키는데 사용되는 간단한 async/await 예제입니다.

```
const doSomethingAsync = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve('I did something'), 3000)
    })
}

const doSomething = async () => {
  console.log(await doSomethingAsync())
}
console.log('Before')
doSomething()
console.log('After')
//Before
//After
//I did something // after 3s
```
### Promise all the things
어떤 함수 앞에 async 키워드를 앞에 붙이는 것은 함수가 프로미스를 리턴한다는 것입니다. 명시적인 것이 없더라도 내부적으로는 프로미스를 리턴합니다. 이 때문에 다음과 같은 코드가 동작합니다.

```
const aFunction = async () => {
  return 'test'
}

aFunction().then(alert) // this will alert 'test'
```
뒤의 코드는 아래와 같습니다.
```
const aFunction = async () => {
  return Promise.resolve('test')
}

aFunction().then(alert) // this will alert 'test'
```
### The code is much simpler to read
위의 예제에서 보셨듯이 코드가 훨씬 간단해 집니다. 그냥 체이닝이나 콜백 함수와 함께 쓴 일반 프로미스들을 사용한 코드와 비교해보세요.

이것은 매우 간단한 예제이지만 코드가 복잡해 질수록 주요 이익은 더욱 커질것입니다. 아래의 예제는 프로미스를 사용하여 JSON 리소스를 가져오고 파싱하는 것입니다.
```
const getFirstUserData = () => {
  return fetch('/users.json') // get user list
  .then(response => response.json()) // parse JSON
  .then(users => users[0]) // pick first user
  .then(user => fetch(`/users/${user.name}`)) // get user data
  .then(userResponse => userResponse.json()) // parse JSON
}

getFirstUserData()
```
그리고 아래는 await/async를 사용하여 같은 기능을 구현했습니다.
```
const getFirstUserData = async () => {
  const response = await fetch('/users.json') //get users list
  const users = await response.json // parse JSON
  const user = users[0] // pick first user
  const userData = await userResponse.json() // parse JSON
  return userData
}
getFirstUserData()
```

### Multiple async functions in series
비동기 함수들은 매우 쉽게 연결될 수 있고 일반 프로미스보다 훨씬 읽기 쉬운 문법입니다.
```
const promiseToDoSomething = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve(`I did something`), 10000)
    })
}

const watchOverSomeoneDoingSomething = async () => {
  const something = await promiseToDoSomething()
  return something + ' and I watched'
}

const watchOverSomeoneWatchingSomeoneDoingSomething = async () => {
  const something = await watchOverSomeoneDoingSomething()
  return something + ' and I watched as well'
}

watchOverSomeoneWatchingSomeoneDoingSomething().then( res => {
  console.log(res)
  })
// I did something and I watched and I watched as well
```
### Easier debugging
프로미스를 디버깅하는 건 매우 힘듭니다. 왜냐하면 디버거가 비동기 코드에서 넘어가지 않기 때문입니다. Async/await는 이 부분을 매우 쉽게만드는데 왜냐하면 컴파일러가 동기화 코드처럼 다루기 때문입니다.

## Events

<a href="https://flaviocopes.com/javascript-event-loop/"> The JavaScript Event Loop </a>

### Introduction
이벤트 루프는 자바스크립트를 이해하는 데 가장 중요한 측면 중 하나 입니다.
> 자바스크립트로 몇 년간 개발하고 있지만 아직도 어떻게 내부적으로 동작하는지 완벽히 이해하지 못했습니다. 이 개념을 자세하게 이해하지 않아도 상관없지만 어떻게 동작하는지 아는게 도움이 되겠죠 그리고 이 부분에 대해서 궁금해 하실수도 있구요.
{:.lead}

여기서는 자바스크립트가 단일 스레드로 어떻게 작업을 하는것과 비동기 함수를 어떻게 처리하는 지에대해 내부의 자세한 사항에 대해서 설명하겠습니다. 여러분의 자바스크립트 코드는 단일 쓰레드에서 동작합니다. 한 번에 오직 한 가지 일만 일어나죠.

이 제한은 시렞로 매우 도움이 됩니다. 동시성 문제를 걱정하지 않고 프로그램을 할 수 있거든요. 여러분은 단지 동기 네트워크 콜이나 무한 루프같이 스레드를 중단시키는 작업만 피해서 코드를 작성하시면 됩니다.

일반적으로 많은 브라우저들은 각 브라우저 탭마다 이벤트 루프가 있고 각 프로세스들은 독립되어 웹페이지가 무한루프나 브라우저 전체를 멈추게하는 무거운 연산을 피할 수 있도록 합니다.

여러개의 동시 이벤트를 관리하는 환경은 API 요청을 처리하기 위한 것입니다. Web Workers 또한 그들의 이벤트 루프에서 동작합니다. 여러분은 코드가 단일 이벤트 루프에서 동작하고 중단되는 것을 피하도록 염두하면서 코딩을 하시면 됩니다.

### Blocking the event loop
어떤 자바코드라도 이벤트 루프에 제어를 돌려주기까지 오래 걸리게 된다면 해당 페이지에 있는 모든 실행을 중단시킬 것입니다. UI 쓰레드와 사용자의 클릭, 페이지 스크롤 등등 말이죠. 거의 모든 I/O 기본작업들은 자바스크립트에서 논블로킹 입니다. 네트워크 요청, Node.js 파일시스템 연산 등등도 논블로킹입니다. 블록되는 것이 예외사항으로 이것은 자바스크립트가 많은 부분을 콜백, 프로미스, async/await에 기반을 두는 이유입니다.

### The call stack
콜 스택은 Last in First out 큐입니다. 이벤트 루프는 지속적으로 콜스택을 검사하여 실행햐야 할 함수가 있는지 확인합니다. 그렇게 하면서 이벤트 루프가 발견하는 모든 함수 호출을 콜스택에 추가하고 하나씩 순서대로 살행합니다. 디버거나 브라우저 콘솔에서 익숙히 볼 수 있는 에러 스택 추적을 아시나요? 브라우저는 당신에게 현재 호출이 어떤 함수에서 일어났는지 알려주기위해 콜스택에서 함수 이름을 찾습니다.
<center>
<img src="https://flaviocopes.com/javascript-event-loop/exception-call-stack.png"/>
</center>

### A simple event loop explanation
다음과 같은 예제를 한번 봅시다.
```
const bar = () => console.log('bar')

const baz = () => console.log('baz')

connt foo = () => {
  console.log('foo')
  bar()
  baz()
}
foo()
//this code prints as expedted
//foo
//bar
//baz
```
이 코드를 실행시키면 먼저 foo()가 호출됩니다. foo()의 내부에서 처음에 bar()를 호출하고 그다음 baz()를 호출합니다. 이 때 콜 스택은 다음 그림과 같습니다.
<center>
<img src="https://flaviocopes.com/javascript-event-loop/call-stack-first-example.png"/>
</center>
이벤트 루프는 콜스택이 비어있을 때까지 매번 콜스택에 무언가 있는지 확인하고 그것을 실행합니다.
<center>
<img src="https://flaviocopes.com/javascript-event-loop/execution-order-first-example.png"/>
</center>

### Queuing function execution
위의 예제는 평범해 보이죠, 특별할 것없이 자바스크립트가 실행할 것을 찾고 순서대로 실행합니다. 스택에 아무것도 남지 않을 때까지 어떻게 함수를 연기시키는지 알아봅시다.

setTimeout(() => {}), 0)의 사용법은 함수를 호출하지만 현재 실행되는 다른 함수가 실행되고나서 실행됩니다. 다음의 예제를 보시죠.
```
const bar = () => console.log('bar')

const baz = () => console.log('baz')

const foo = () => {
  console.log('foo')
  setTImeout(bar, 0)
  baz()
}
foo()
//code prints
//foo
//baz
//bar
```
코드를 실행시키면 처음에 foo()가 호출됩니다. foo() 내부에서 처음에 Timeout을 설정하고 bar를 매개변수로 전달합니다. 우리가 가능한 즉시 실행하도록 0을 타이머에 전달했습니다. 그리고 우리는 baz()를 호출합니다. 이 때 콜스택은 다음의 그림과 같습니다.
<center>
<img src="https://flaviocopes.com/javascript-event-loop/call-stack-second-example.png"/>
</center>
다음은 우리 프로그램에서 모든 함수가 실행되는 순서입니다.
<center>
<img src="https://flaviocopes.com/javascript-event-loop/execution-order-second-example.png"/>
</center>
왜 이렇게 되었을까요?
### The Message Queue
setTimeout()이 호출되면 브라우저나 Node.js는 타이머를 시작합니다. 한번 타이머가 시작하면 이 경우에는 우리가 0을 넣었지만, 콜백 함수는 메시지 큐에 들어가게 됩니다.

메시지 큐는 클릭이나 키보드 이벤트처럼 사용자가 일으키는 이벤트 혹은 여러분의 코드가 반응하기 전에 응답을 가져오는 큐 혹은 onLoad같은 DOM 이벤트 들입니다.

<b>루프는 콜스택에 우선순위를 부여하여 처음 프로세스가 콜스택에서 모든 것을 찾고 아무것도 없다면 메시지 큐에서 다음 것을 가져옵니다.</b>

우리는 setTimeout같은 함수를 기다릴 필요가 없고 다른 작업들을 수행합니다. 왜냐하면 타임아웃은 브라우저에 의해 제공되고 타임아웃은 스스로의 스레드에 있기 때문입니다. 만약 여러분이 setTImeout에 2초를 설정한다면 여러분은 2초를 기다릴 필요가 없습니다 - 기다리는 것은 어디에서나 일어납니다.
### ES6 Job Queue
ECMAScript 2015는 프로미스에 사용되는 Job 큐의 개념에 대해서 소개했습니다 그것은 비동기 함수의 결과를 콜스택의 끝에 넣는 것 대신에 가능한 빨리 실행하는 방법입니다.

프로미스가 현재 함수가 끝나기 전에 해결되면 현재 함수의 바로 뒤에 실행될 것입니다.

저는 놀이공원에서 롤러코스터를 타는 것과 아주 유사한 점을 발견했습니다. 메시지 큐는 큐의 제일 뒤에 여러분을 놓을 것입니다. 모든 다른 사람들 뒤에 줄을 세우는 것이죠. 여러분이 차례가 올 때까지 기다리는 반면에 Job 큐는 여러분에게 이전의 작업이 끝나면 바로 탈 수 있는 패스트 티켓을 주는 것과 같습니다.

```
const bar = () => console.log('bar')

const baz = () => console.log('baz')

const foo = () => {
  console.log('foo')
  setTimeout(bar, 0)
  new Promise((resolve, reject) =>
  resolve('should be right after baz, before bar')
  ).then(resolve => console.log(resolve))
  baz()
}
foo()
//This prints
//foo
//baz
//should be right after baz, before bar
//bar
```
이것이 프로미스(프로미스에 기반한 async/await)와 일반 고전 비동기 함수(setTimeout, 다른 플랫폼의 API들)의 큰 차이입니다.

<a href="https://flaviocopes.com/javascript-events/"> JavaScript Events</a>
### Introduction
브라우저 내에서 자바스크립트는 event-driven programming 모델을 사용합니다. 모든 것은 따라오는 이벤트에 의해 시작됩니다. 이벤트란 DOM이 로딩된 것일 수도 있고 비동기 요청이 가져오는 작업을 끝냈거나 사용자가 요소를 클릭하거나 페이지를 스크롤링하거나 키보드를 누른 것입니다.
### Event handlers
여러분은 모든 이벤트에 이벤트 핸들러를 사용해서 응답할 수 있습니다. 이벤트 핸들러는 이벤트가 발생했을 떄 호출되는 함수입니다. 하나의 이벤트에 여러개의 핸들러를 등록할 수 있으며 모든 핸들러들이 해당 이벤트가 발생했을 때 호출될 것입니다. 자바스크립트는 세가지의 이벤트 핸들러 등록방법을 제공합니다.
### Inline event handlers
이 스타일은 제약사항 때문에 요즘에는 잘 쓰으지 않습니다만 예전에는 딱 이 방법으로만 이벤트 핸들러 등록이 가능했습니다.
```
a href="site.com" onClick="doSomething();">A link</a>
```
### Dom on-event handlers
이것은 객체가 하나의 이벤트 핸들러를 가질 때 가장 일반적인 방법이며 추가적인 이벤트 핸들러를 가질 수 없습니다.
```
window.onload = () => {
  window loaded
}
//XHR 요청을 처리하는데 가장 일반적인 방식입니다.
const xhr = new XMLHttpRequest()
xhr.onreadystatechange = () => {
  //.. do something
}
```
여러분이 핸들러가 특정 프로퍼티에 할당되었는지 확인하고 싶다면 if('onsomething' in window) {}로 확인할 수 있습니다.
### Using addEventListener()
이 방법이 가장 최신방식입니다. 이 방법은 우리가 필요한만큼 핸들러를 추가할 수 있으며 여러분이 가장 많이 볼 수 있는 방식입니다.
```
window.addEventListener('load', () => {
  //window loaded
}
```
IE8과 그 이하버전은 이것을 지원하지 않기 때문에 attachEvent() API를 사용해야 합니다. 여러분이 오래된 브라우저를 지원해야 할 경우 기억해두세요.
### Listening on different elements
여러분은 window를 이용해서 키보드 사용과 같은 전역이벤트를 가로챌 수 있습니다. 그리고 특정 요소에 마우스 클릭과 같은 이벤트가 발생한 것도 캐치할 수 있습니다. 이것이 addEventListener가 때때로 window에서 호출되고 또 어떤 때는 DOM요소에서 호출되는 이유입니다.
### The Event object
이벤트 핸들러는 이벤트 객체를 첫 매개변수로 입력받습니다.
```
const link = document.getElementById('my-link')
link.addEventListener('click', event => {
  // link clicked
  })
```
이 객체에는 유용한 프로퍼티와 메소드가 많이 있습니다. 예를 들면
* target, 이벤트를 발생시킨 DOM 요소,
* type, 이벤트 타입
* stopPropagation(), DOM안에 이벤트가 그만 전파되길 원할 때 호출
다른 프로퍼티들은 이벤트의 종류에 따라 다릅니다. 이벤트가 서로 다른 인터페이스를 가지기 때문이죠.
* MouseEvent
* KeyboardEvent
* DragEvent
* FetchEvent ...and others

예를들어 키보드이벤트가 발생하면 key프로퍼티를 이용해 어떤 키가 눌려졌는데 확인할 수 있습니다.
```
window.addEvenntListener('keydown', event => {
  //key pressed
  console.log(event.key)
  })
```
마우스 클릭 이벤트 발생시 어떤 버튼이 눌렸는지 확인할 수 있습니다
```
const link = document.getElementById('my-link')
link.addEventListener('mousedown', event => {
  //mouse button pressed
  console.log(event.button) //0 = left, 2 = right
  })
```

### Event bubbling and event capturing
버블링과 캡쳐링은 이벤트 전달을 위한 두가지 모델입니다. 다음과 같은 DOM 구조가 있다고 가정합시다.
```
<div id="container">
  <button>Click me</button>
</div>
```
여러분은 사용자가 버튼을 클릭한 것을 추적하고 싶어하며 두개의 이벤트 리스너가 있습니다. 하나는 버튼에 있고 하나는 #container에 있습니다. 여러분이 전달을 멈추지 않는 이상 자식 요소에 대한 클릭은 항상 부모에게 전달된다는 것을 기억하세요

이런 이벤트 리스너들은 순서에 따라 호출될 것이고 이 순서는 이벤트 버블링/캡쳐링 모델에 따라 결정되게 됩니다. 버블링의 의미는 이벤트가 발생한 아이템에서 가장 가까운 부모의 트리로 계속 올라간다는 것입니다. 우리의 예제에서 버튼에 있는 핸들러는 #container핸들러 보다 먼저 호출될 것입니다.

캡쳐링은 반대입니다. 바깥의 이벤트 핸들러가 먼저 발생하게 됩니다. 기본적으로 모든 이벤트들은 버블링 모델입니다. 여러분은 addEventListener에 세번째 매개변수를 true로 하면 캡쳐링 모델을 적용할 수 있습니다.
```
document.getElementById('container').addEventListener(
  'click',
  () => {
    //window loaded
  },
  true
  )
```
캡쳐링 이벤트가 먼저 동작한다는 것을 기억하세요, 그리고 나서 버블링 이벤트가 동작합니다. 순서는 다음과 같은 원칙을 따릅니다. DOM이 window 객체부터 시작해서 모든 요소를 지나가면서 클릭된 아이템을 찾습니다. 이렇게 하면서 이벤트와 연관되어 있는 모든 이벤트 핸들러를 호출합니다(캡쳐링 모델) 만약 target에 도달하면 그다음 윈도우 객체까지 거슬러 올라가며 이벤트 핸들러를 호출합니다(버블링 모델)
### Stopping the propagation
DOM 요소의 이벤트는 멈추기 전까지는 모든 부모 트리에게 전달됩니다.
```
<html>
  <body>
    <section>
      <a id="my-link" ...>
```
a에서 발생한 이벤트가 section에서 body까지 전달됩니다. 이벤트에 stopPropagation()메소드를 호출해서 전파되는 것을 멈출 수 있으며 보통 이벤트 핸들러 끝에 작성합니다.
```
const link = document.getElementById('my-link')
link.addEventListener('mousedown', event => {
  // process the event
  // ...

  event.stopPropagation()
  })
```
### Popular events
다음은 여러분이 가장 자주 처리하는 이벤트들입니다.
#### Load
load는 window와 body 요소에서 발생하며 페이지 로딩이 끝났을 때입니다.
#### Mouse events
click은 마우스 버튼이 클릭되었을 때 발생합니다. dblclick은 마우스가 두번 클릭되었을 때 입니다. 물론 이 경우에도 click이 dblclick전에 호출됩니다. mousedown, mousemove, mouseupdms 드래그앤드롭 이벤트를 추적하기 위해 조합되어 사용됩니다. mousemove를 사용할 땐 주의하셔야 하는데 마우스가 움직일 때마다 호출되기 때문입니다.
#### Keyboard events
keydown은 키보드 버튼이 눌렸을 때 호출되며 키보드 버튼이 눌러져 있으면 계속 호출됩니다. keyup은 키보드 버튼이 떼어졌을 때 호출됩니다.
#### Scroll
scroll이벤트는 window에서 발생하며 페이지를 스크롤할 때마다 호출됩니다. 이벤트 핸들러 내부에서 window.scrolly를 이용해 현재 스크롤 위치를 확인할 수 있습니다. 이 이벤트는 일회성이 아니라는 것을 기억하세요. 스크롤링 시작과 끝말고도 스크롤링 중간에 많은 이벤트가 발생하기 때문에 핸들러 내부에서 많은 연산이나 조작을 하지 않아야 합니다. 그럴경우 대신 throttling을 사용하세요.
#### Throttling
위에서 잠시 언급한 것처럼 mousemove나 scroll은 이벤트 당 한번만 호출되는 것이 아니라 해당 행동이 지속되는 동안 계속해서 호출됩니다. 이렇게 해야 여러분이 무슨일이 일어나는지 추적할 수 있기 때문이죠. 만약 이벤트 핸들러에서 복잡한 연산을 수행한다면 성능에 영향을 줄 것이고 여러분의 사이트 사용자들은 버벅거리는 것을 경험하게 될겁니다.

<a href="https://lodash.com/docs/4.17.10#throttle">Loadsh</a>와 같은 throttling 라이브러리는 100줄 조금 넘는 코드로 가능한 모든 경우를 처리해줍니다. 이 문제를 해결하기 위한 간단하고 쉬운방법은 setTimout을 사용해서 100ms마다 스크롤 이벤트를 캐치하는 것입니다.
```
let cached = null
window.addEventListener('scroll', event => {
  if(!cahced) {
    setTImeout(() => {
      //원본 이벤트는 cached를 이용해 접근할 수 있습니다.
      cached = null
    }, 100)
  }
  cached = event
  })
```
