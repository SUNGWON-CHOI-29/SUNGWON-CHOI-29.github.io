---
layout: post
title: Node.js Study (11)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (11)

## Asynchronous Programming and Callbacks
자바스크립트는 기본적으로 동기적이고 단일 스레드로 동작합니다. 이말은 코드가 새로운 쓰레드를 만들거나 병렬적으로 실행될 수 없다는 것입니다.
### Asynchronous in Programming Languages
컴퓨터는 비동기적으로 설계되었습니다. 비동기화의 의미는 하나의 주 프로그램 흐름과 독립적으로 작업이 수행될 수 있다는 것입니다. 현재 소비자 컴퓨터의 모든 프로그램은 특정 타임 슬롯에만 동작하고 해당 시간이 지나면 다른 프로그램이 실행될 수 있도록 멈춥니다. 이것은 알아차릴 수 없을만큼 빠른 속도로 순환되어 동작하며 우리는 컴퓨터가 동시에 여러개의 프로그램을 수행하는 것처럼 느껴지게 되비다. 그러나 이건 착각입니다.(멀티프로세서 머신은 예외입니다.)

프로그램은 내부적으로 인터럽트를 사용해서 프로세서가 시스템의 주목을 받아야하면 시그널을 발생시킵니다. 여기서 더욱 깊게 들어가고 싶지 않지만 그냥 일반적으로 프로그램은 비동기화되고 그들이 어텐션을 받기 전까지 중단되며 컴퓨터는 다른 것을 그 동안에 수행한다는 것입니다. 프로그램이 네트워크로부터 응답을 기다릴 때 해당 요청이 끝날 때까지 프로세스를 중단시킬 수 없습니다.

일반적으로 프로그래밍 언어는 동기적이며 몇몇은 비동기성을 관리하기 위한 방법을 라이브러리를 통해 제공합니다. 자바, C, C#, PHP, Go, Ruby, Swift, Python은 모두 동기화가 기본적이죠. 몇몇은 쓰레드를 사용해서 비동기를 처리하거나 새로운 프로세스로 확장할 수 있습니다.

### JavaScript
자바스크립트는 기본적으로 단일 쓰레드에 동기화입니다. 이 말은 코드가 새로운 스레드를 만들거나 병렬적으로 실행될 수 없다는 것입니다. 코드들은 순서대로 하나씩 실행됩니다.
```
const a = 1
const b = 2
const c = a * b
console.log(c)
doSomething()
```
그러나 자바스크립트는 브라우저 내부에서 탄생했습니다. 초기에 주요작업은 클릭이나 마우스오버, onChange, onSubmit과 같은 사용자 행동에 반응하기 위해서였죠. 어떻게 동기화 프로그래밍으로 이걸 할 수 있을까요?

해답은 자바스크립트의 환경입니다. 브라우저는 API들을 제공해서 이런 기능을 처리할 수 있도록 했습니다. 최근에 들어서 Node.js는 이러한 개념을 파일 접근, 네트워크 호출등에 확장시킨 논블로킹 I/O 환경을 제공합니다.

### Callbacks
여러분은 사용자가 버튼을 언제 누를지 알 수 없기 때문에 여러분이 해야할 일은 클릭 이벤트에 대한 이벤트 핸들러를 정의하는 것입니다. 이 이벤트 핸들러는 함수를 받아서 이벤트가 발생하면 그것을 호출합니다.

```
document.getElementByID('button').addEventListener('click', () => {
  // item clicked
  })
```
이것이 콜백이라는 것입니다.

콜백은 단순히 다른 함수에 값처럼 전달되는 함수로써 이벤트가 발생할 때만 실행될 것입니다. 이것을 사용할 수 있는 이유는 자바스크립트가 일급 클래스 함수를 가지고 있기 때문에 함수를 변수에 할당하거나 다른 함수에 전달할 수 있습니다. 클라이언트 코드를 window 객체에 load 이벤트 리스너로 감싸는 것은 일반적입니다. 페이지가 준비되었을 때 실행되는 콜백함수이죠.
```
window.addEventListener('load', () => {
  //window loaded
  //do what you want
  })
```
콜백은 DOM 이벤트들 뿐만아니라 어디서나 쓰입니다. 일반적으로 쓰이는 다른 예는 타이머 입니다.
```
setTimeout( () => {
  // runs after 2 seconds
  }, 2000)
```

XHR requests 또한 콜백을 받는 데 이 예제에서는 특정 이벤트가 발생했을 때 호출되도록 함수를 프로퍼티에 할당할 것입니다.
```
const xhr = new XMLHttpRequest()
xhr.onreadystatechange = () => {
  if (xhr.readyState === 4) {
    xhr.status === 200 ? console.log(xhr.responseText) :
    console.error('error')
  }
}
xhr.open('GET', 'https://yoursite.com')
xhr.send()
```

### Handling errors in callbacks
콜백에서 에러처리는 어떻게 할까요? 가장 일반적인 방법이 Node.js에 적용되었습니다. 콜백함 수의 첫 매개변수를 에러 오브젝트로 받는 것입니다 - error-first callbacks

만약 에러가 없다면 해당 객체는 null일 것입니다. 에러가 있다면 에러와 다른 정보를 가지고 있을겁니다.
```
fs.readFile('/file.json', (err,data) => {
  if(err !== null) {
    //handle error
    console.log(err)
    return
  }

  //no errors, process data
  console.log(data)
  })
```

### The problem with callbacks
콜백은 간단한 경우에는 매우 좋습니다. 그러나 모든 콜백은 중첩레벨을 추가합니다. 많은 콜백을 추가한다면 코드는 급격하게 복잡해질 것입니다.
```
window.addEventListener('load', () => {
  document.getElementById('button').addEventListener('click', () => {
    setTimeout( () = > {
      items.forEach(item => {
        //your code here
        })
      }, 2000)
    })
  })
```
이것은 단순히 4단계의 코드이지만 더욱 중첩도가 높은 코드도 본 적이 있습니다. 그건 재밌지 않죠. 이 문제를 어떻게 해결할 수 있을까요?
### Alternatives to callbacks
ES6에서 자바스크립트는 비동기화 코드를 작성할 때 콜백을 사용하지 않아도 되도록 도와주는 피쳐들을 소개했습니다.
* Promises (ES6)
* Async/Await (ES8)

## Promises
프로미스는 자바스크립트에서 비동기화 코드를 처리하는 한 방법입니다. 코드에서 많은 콜백을 작성하지 않고 말이죠.
### Introduction to promises
프로미스는 일반적으로 <b>결국에는 사용가능하게 될 proxy 값으로 정의됩니다.</b> ES2015에서는 표준이 되었지만 ES2017에서 비동기 함수들에게 자리를 내주게 되었습니다. 비동기 함수는 프로미스 API들을 빌딩블록으로 사용하기 때문에 프로미스에 대한 이해는 프로미스 대신에 비동기 함수를 사용하더라도 필수적입니다.
### How promises work, in brief
프로미스가 한번 불리면 pending 상태에서 시작합니다. 이 말은 콜러 함수가 실행을 계속하며 프로미스는 자체적인 프로세싱이 끝날 때까지 기다리고 콜러 함수는 피드백을 받게 됩니다. 이 시점에서 콜러 함수는 프로미스가 resolved state/rejected state 둘 중 하나를 리턴받습니다. 그러나 알다시피 자바스크립트는 비동기적이기 때문에 함수는 프로미스가 동작하는 동안 계속해서 실행될 것입니다.

### Which JS API use promises?
프로미스는 다음과 같은 모던 웹 API들에서 사용됩니다.
* the Battery API
* the Fetch API
* Service Workers
모던 자바스크립트에서는 프로미스를 사용하지 않는 것과는 좀 상반됩니다.

### Creating a promise
프로미스 API는 프로미스 생산자를 통해 초기화 할 수 있습니다.
```
let done = true

const isItDoneYet = new Promise(
  (reslove, reject) => {
    if (done) {
      const workDone = 'Here is the thing I built'
      resolve(workDone)
    } else {
      const why = 'still working on something else'
      reject(why)
    }
  }
)
```
프로미스는 done 글로벌 상수를 체크하고 true라면 resolved 프로미스를 아니면 rejected 프로미스를 리턴합니다. resolve와 reject를 사용하면서 우리는 과거의 값과 통신할 수 있으며 위에서는 단순히 문자열을 리턴했지만 객체가 될 수도 있습니다.

### Consuming a promise
마지막 영역에서는 어떻게 프로미스가 생성되는지 봤습니다. 이제 프로미스가 어떻게 사용되고 소비되는지 알아봅시다.
```
const isItDoneYet = new Promise(
  //...
  )
const checkIfItsDone = () => {
  isItDoneYet
    .then((ok) => {
    console.log(ok)
    })
    .catch((err) => {
      console.error(err)
    })
}
```
checkIfItsDone()을 실행하면 isItDoneYet() 프로미스를 실행하고 then 콜백을 사용해서 resolve가 될 때까지 기다릴 것입니다. 만약 에러가 있다면 catch 콜백에서 프로미스가 처리될 것입니다.
### Chaining promises
프로미스는 프로미스 체인을 만들며 또다른 프로미스를 리턴할 수 있습니다. 가장 좋은 예는 Fetch API입니다. XMLHttpRequest API의 상위 레이어에서 자원을 가져올 때 사용하며 자원이 가져와지면 체인 프로미스를 실행합니다. Fetch API는 프로미스 기반의 메커니즘으로 fetch()는 new Promise()와 동일합니다.

### Example of chaining promises
```
const status = (response) => {
  if (response.status >= 200 && response.status < 300) {
    return Promise.resolve(response)
  }
  return Promise.reject(new Error(response.statusText))
}

const json = (response) => response.json()

fetch('/todos.json')
  .then(status)
  .then(json)
  .then((data) => { console.log('Request succeeded with JSON response', data)
  })
  .catch((error) => { console.log('Request failed', error) })
```
이 예제에서 fetch()는 TODO 아이템의 리스트를 todos.json 파일에서부터 가져옵니다. fetch()는 많은 프로퍼티들을 가지고 있는 response를 리턴하며 내부에서 우리는 다음과 같은 것을 조회할 수 있습니다.
* status, HTTP 상태 코드를 나타내는 숫자값
* statusText, 리퀘스트가 성공적이었다면 OK를 리턴함

response는 json()메소드를 가지고 있어서 body의 내용을 JSON 형태로 변환하여 resolve로 리턴할 것입니다. 그래서 주어진 프로미스들은 이런일이 발생합니다. 우리가 정의한 함수안에 첫 프로미스는 status()를 호출하고 response status를 체크하여 성공적이지 않다면 reject promise를 리턴합니다.

이렇게 되면 연결된 프로미스들의 리스트를 모두 건너뛰고 바로 catch()구문이 있는 아래로 내려가게 되고 Request failed 텍스트를 남기게 됩니다.

성공적이었다면 우리가 정의한 json함수를 호출합니다. 이전의 프로미스가 성공할 때마다 우리는 두번째 프로미스의 입력으로 넣어줍니다. 이 경우에 JSON 처리된 데이터를 받게되고 세번째 프로미스는 JSON을 바로 받게 됩니다.
```
.then((data) => {
  console.log('Request succeeded with JSON response', data)
  })
```
### Handling errors
이전에서 프로미스 체인 뒤에 catch를 붙여놨습니다. 프로미스 체인에서 하나라도 실패하거나 에러가 발생하면 컨트롤은 가장 근처에 있는 catch()구문으로 갑니다.
```
new Promise((resolve, reject) => {
  throw new Error('Error')
  })
  .catch(err) => { console.error(err)}

//or

new Promise((resolve, reject) => {
  reject('Error')
  })
  .catch((err) => { console.error(err) })
```
### Cascading errors
catch()구문 안에서 에러가 발생한다면 두번째 catch()를 추가해서 처리할 수 있습니다.
```
new Promise((resolve, reject) => {
  throw new Error('Error')
  })
  .catch((err) => { throw new Error('Error') })
  .catch((err) => { console.error(err) })
```
