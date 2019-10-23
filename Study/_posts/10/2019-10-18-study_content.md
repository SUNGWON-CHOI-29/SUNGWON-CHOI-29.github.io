---
layout: post
title: Node.js Study (12)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (12)

## Orchestrating promises
다른 프로미스들이 동기화될 필요가 있다면 Promise.all()이 프로미스 리스트를 정의하는 데 도움이 될 것입니다. 그렇게하면 리스트된 프로미스들이 모두 resolved되었을 때 뭔가를 실행할 수 있습니다.

```
const f1 = fetch('/something.json')
const f2 = fetch('/something2.json')

Promise.all([f1,f2]).then((res) => {
  console.log('Array of results', res)
  })
  .catch((err) => {
    console.error(err)
    })
```
<a href="https://flaviocopes.com/ecmascript/#destructuring-assignments">ES2015의 destructing assignment</a>문법도 사용할 수 있습니다.
```
Promise.all([f1, f2]).then(([res1, res2]) => {
  console.log('Results', res1, res2)
  })
```
물론 fetch에만 해당되는 것이 아니라 모든 프로미스에 사용할 수 있습니다.

<b>Promise.race()</b>는 처음으로 resolve된 프로미스가 전달되며 처음 프로미스의 결과로 부착된 콜백이 한번만 실행됩니다.

```
const first = new Promise((resolve, reject) => {
  setTimeout(resolve, 500, 'first')
  })
const second = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'second')
  })
Promise.race([first, second]).then((result) => {
  console.log(result) //second
  })
```

### Common error, Uncaught TypeError: undefined is not a promise
<b>Uncaught TypeError: undefined is not a promise</b>에러가 콘솔에서 발생했다면 <b>new Promise()</b>대신에 Promise()를 사용한 것은 아닌지 확인해보세요.

## Async and Await
자바스크립트에서 현대적인 비동기 함수 접근법에 대해 알아봅시다.

자바스크립트는 짧은 시간에 콜백에서 프로미스로(ES2015), 그리고 ES2017에서 자바스크립트 비동기화는 async/await 문법으로 더욱 간단해졌습니다.

비동기 함수들은 프로미스들과 생성자들의 조합이며 기본적으로 프로미스의 상위수준 추상화입니다. 다시한번 말씀드리지만 async/await는 프로미스를 기반으로 만들어졌습니다.

### Why were async/await introduced?
프로미스의 불필요한 부분을 줄이고 중간에 체인을 끊지못하는 프로미스 체이닝 제한을 없앴습니다.

프로미스가 ES2015에서 소개되었을 때 비동기화 코드의 문제점을 해결하려고 나왔지만 2년 뒤 ES2015와 ES2017에서 분리되었을 때 프로미스가 최종 솔루션이 될 수 없다는 것이 명백해졌습니다.

프로미스는 유명한 콜백 지옥 문제를 해결하기 위해 소개되었지만 자체적인 프로미스 복잡성과 문법 복잡도가 있었습니다. 좋은 기본형이기 때문에 더욱 나은 문법으로 개발자들에게 보여질 수 있었고 그래서 비동기 함수들이 나오게 되었습니다.

비동기 함수들은 동기된 것처럼 보이지만 비동기화 되어있고 논블로킹 입니다.

### How it works?
<b>async</b> 함수는 프로미스를 리턴합니다. 예제를 봅시다.
```
const doSomethingAsync = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve('I did something'), 3000)
    })
}
```
이 함수를 호출하고 싶다면 앞에 <b>await</b>를 붙여야 합니다. 그리고 호출하는 코드는 프로미스가 resolve/reject될 때까지 멈추게 될 것입니다. 클라이언트 함수는 반드시 <b>async</b>로 정의되어야 합니다. 다음은 사용예입니다.
```
const doSomething = async () => {
  console.log(await doSomethingAsync())
}
```
### A quick example
다음은 async/await 예제로써 함수를 비동기적으로 실행합니다.
```
const doSomethingAsync = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve('I did something'), 3000)
    })
}

const doSomething = async () => {
  console.log(await doSomethingAsync())
}

console.log('Before')
doSomething()
console.log('After')

//output
//Before
//After
//I did something //3초후
```

### Promise all the things
async 키워드를 함수 앞에 붙이는 의미는 함수가 프로미스를 리턴할 것이라는 것입니다. 명시적으로 되어있지 않아도 내부적으로는 프로미스를 리턴합니다. 따라서 다음과 같은 코드가 가능합니다.
```
const aFunction = async () => {
  return 'test'
}

aFunction().then(alert)
```
위의 코드는 다음과 같습니다.
```
const aFunction = async () => {
  return Promise.resolve('test')
}

aFunction().then(alert)
```

### The code is simpler to read
위의 예제에서 보다싶이 코드는 매우 간단해 보입니다. 체이닝을 사용한 프로미스나 콜백함수들과 비교해보세요. 예제는 매우 간단하지만 코드가 더욱 복잡해지게 되면 큰 장점이 부각될 것입니다. 예를 들어 다음은 JSON 리소스를 가져와서 파싱하는 것으로 프로미스를 사용합니다.
```
const getFirstUserData = () => {
  return fetch('/users.json') // get users list
    .then(response => response.json()) // parse JSON
    .then(users => users[0]) // pick first user
    .then(user => fetch(\`users/${user.name}\`)) // get user data
    .then(userResponse => response.json()) // parse JSON
}

getFirstUserData()
```

다음은 await/async를 사용해서 동일한 기능을 제공합니다.
```
const getFirstUserData = async () => {
  const response = await fetch('/users.json') // get users list
  const users = await response.json() // parse JSON
  const user = users[0] // pick first user
  const userResponse = await fetch(\`/users/${user.name}\`) // get user data
  const userData = await user.json
  return userData
}

getFirstUserData()
```

### Multiple async functions in series
async 함수들은 매우 쉽게 체인될 수 있고 문법도 일반적인 프로미스보다 더욱 읽기 쉽습니다.
```
const promiseToDoSomething = () => {
  return new Promise(resolve => {
    setTimeout(() => resolve('I did something'), 10000)
    })
}

const watchOverSomeoneDoingSomething = async () => {
  const something = await promiseToDoSomething()
  return something + ' and I wathced'
}

const watchOverSomeoneWatchingSomeoneDoingSomething = async () => {
  const something = await watchOverSomeoneDoingSomething()
  return something + ' and I watched as well'
}

watchOverSomeoneWatchingSomeoneDoingSomething().then((res) => {
  console.log(res)
  })

//output
//I did something and I watched and I watched as well
```
### Easier debugging
프로미스를 디버깅 하는 것은 디버거가 비동기화 코드에서 넘어가지 않기 때문에 어렵습니다. async/await는 컴파일러에게 동기화 코드처럼 취급되기 때문에 디버깅이 쉽게 됩니다.
