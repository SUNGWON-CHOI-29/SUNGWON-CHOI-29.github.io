---
layout: post
title: Basic of the JavaScript (2)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
<a href="https://flaviocopes.com/javascript-arrow-functions/">JavaScript Arrow Functions</a>
화살표 함수는 ES6에서 소개되었고 그 이후로 영원히 자바스크립트 코드의 외양과 동작을 바꿔버렸습니다. 제 의견에 이 변화는 아주 반길만합니다. 여러분이 현대 코드베이스에서는 거의 function 키워드를 볼일이 없기 때문이죠. 물론 여전히 function이 쓰이는 곳은 있습니다.

시각적으로도 간단하고 반길만한 변화입니다. 왜냐하면 함수를 더욱 짧게 작성할 수 있는 문법을 제공하기 때문입니다.
```
const myFunction = function() {
  //...
}
//to
const myFunction = () => {
  //..
}
```
함수 내부의 구문ㅇ이 한줄이라면 중괄호를 없애고 모든 것을 한줄에 작성할 수 있습니다.
```
const myFunction = () => doSomething()
```
전달되는 매개변수들은 괄호안에 있습니다
```
const myFunction = (param1, param2) => doSomething(param1, param2)
```
만약 매개변수가 오직 하나라면 괄호를 완전히 생략할 수 있습니다
```
const myFunction = param => doSomething(param)
```
이 짧은 문법 덕분에 화솔표 함수는 작은 함수의 사용을 장려합니다.
## Implicit return
화살표 함수는 암시적인 리턴을 허용합니다. return 키워드가 없어도 값이 리턴됩니다. 이것은 함수 내에 구문이 오직 한줄일 때 동작합니다.
```
const myFunction = () => 'test'
myFunction() //`test`
```
또 다른 에제는 객체를 리턴할 때인데, 함수의 내용을 감싸는 괄호처럼 간주되는 것을 피하기 위해 중괄호로 감싸는 것을 기억하세요
```
const myFunction = () => ({ value: 'test '})
myFunction() //{value: 'test'}
```
## How this works in arrow functions
this의 개념은 확실히 이해하기 복잡할 수 있습니다. 컨텍스트에 따라 다양해지고 자바스크립트 모드에 따라 달라지기 때문입니다. this의 개념을 확실하게 하는 것이 중요한 것은 화살표 함수의 동작이 정규 함수들과 비교했을 때 매우 다르기 때문입니다.

객체의 메소드를 정의할 때 정규표현에서 this는 객체를 가리킵니다.
```
const car = {
  model: 'Fiesta',
  manufacturer: 'Ford',
  fullName: function() {
    return `${this.manufacturer} ${this.model}`
  }
}
```
car.fullName을 호출하면 "Ford Fiesta"가 리턴됩니다. 화살표 함수에서 this의 스코프는 실행 컨텍스트에서 상속됩니다. 화살표 함수는 this를 전혀 연결하지 않기 때문에 해당 값은 스택을 호출해서 찾게 될 것입니다. 그래서 애로우 함수의 car.fullName()은 동작하지 않고 "undefined undefined"를 리턴할 것입니다.
```
const car = {
  model: 'Fiesta',
  manufacturer: 'Ford',
  fullName: () => {
    return `${this.manufacturer} ${this.model}`
  }
}
```
이 때문에 화살표 함수는 객체의 메소드에는 적합하지 않습니다. 화살표 함수는 생성자로도 사용할 수 없으며 초기화 시에 TypeError를 일으킵니다. 여기서 동적 컨텍스트가 필요하지 않은 정규 함수가 사용되어야 합니다.

이것은 이벤트를 처리할 때도 문제가 됩니다. DOM 이벤트 리스너는 this를 목표 요소로 설정하기 때문에 이벤트 핸들러에서 this를 사용하고 싶다면 정규 함수가 필요합니다.
```
const link = document.querySelector('#link')
link.addEventListener('click', () => {
  // this === window
  })

const link = document.querySelector('#link')
link.addEventListener('click', function() {
  // this === link
  })
```
<a href="https://flaviocopes.com/javascript-loops/">JavaScript Loops</a>
## Introduction
자바스크립트는 루프를 순회하는 다양한 방법을 제공합니다. 이 예제들은 각각의 간단한 예제와 주요 프로퍼티를 설명할 겁니다.
## For
```
const list = ['a', 'b', 'c']
for (let i = 0; i < list.length; i++) {
  console.log(list[i]) //value
  console.log(i) //index
}
```
* for 루프는 break로 중단할 수 있습니다.
* for 루프는 continue를 통해 다음 순회로 건너뛸 수 있습니다.
## forEach
ES5에서 소개되었으며 배열을 전달하면 list.forEach() 프로퍼티를 사용하며 순회할 수 있습니다.
```
const list = ['a', 'b', 'c']
list.forEach((item, index) => {
  console.log(item) //value
  console.log(index) //index
  })

//index는 선택사항입니다
list.forEach(item => console.log(item))
```
불행히도 여러분은 이 루프를 중단할 수 없습니다.
## do...while
```
const list = ['a', 'b', 'c']
let i = 0
do {
  console.log(list[i]) //value
  console.log(i) //index
  i = i + 1
} while (i < list.length)
```
break를 사용해서 while 루프를 중단할 수 있습니다.
```
do {
  if (something) break
} while (true)
```
그리고 continue를 이용해 다음 순회로 넘어갈 수 있습니다.
```
do {
  if (something) continue

  //do something else
} while (true)
```
## while
```
const list = ['a', 'b', 'c']
let i = 0
while (i < list.length) {
  console.log(list[i]) //value
  console.log(i) //index
  i = i +1
}
```
break를 사용해 루프를 중단하거나 continue를 사용해 다음 순회로 넘어갈 수 있습니다.
```
while (true) {
  if (something) break
}

while (true) {
  if (something) continue

  //do something else
}
```
do...while과의 차이점은 do...while은 최소한 한번 사이클을 실행한다는 것입니다.
## for...in
프로퍼티의 이름을 전달하면 객체의 열거가능한 모든 프로퍼티를 순회합니다.
```
for (let property in object) {
  console.log(property) // property name
  console.log(object[property]) //property value
}
```
## for...of
ES6에서 소개된 for...of 루프는 forEach에 break 기능이 추가된 것입니다.
```
//iterate over the value
for (const value of ['a', 'b', 'c']) {
  console.log(value) // 값
}
//entries()를 사용하여 인덱스도 가져오기
for (const [index, value] of ['a', 'b', 'c'].entries()) {
  console.log(index) //index
  console.log(value) //value
}
```
const의 사용에 주목하세요. 각 루프는 매 순회마다 새로운 스코프를 만들기 때문에 안전하게 let 대신에 const를 사용했습니다.
## for...in vs for...of
for...in은 프로퍼티의 이름을 순회하는 반면 for...of는 프로퍼티의 값을 순회합니다.
<a href="https://flaviocopes.com/javascript-loops-and-scope/">JavaScript Loops and Scope</a>
자바스크립트의 특징 중 개발자들에게 두통을 일으키는 것이 있습니다. 바로 루프와 스코핑입니다. 예제를 보시죠.
```
const operations = []

for (var i = 0; i < 5; i ++) {
  operations.push(() => {
    console.log(i)
    })
}
for (const operation of operations) {
  operation()
}
```
기본적으로 5번 순회하며 함수에 operations 라는 배열에 함수를 추가합니다. 이 함수의 콘솔로그는 루프 인덱스 변수인 i입니다. 나중에 이 함수들을 실행해보면 예상되는 결과는 다음과 같을 것입니다.
```
0
1
2
3
4
```
그러나 실제 결과는 다음과 같습니다.
```
5
5
5
5
5
```
왜 이런 결과가 생겼을까요? 바로 var를 썼기 때문입니다. var의 정의는 상위로 끌어올려지기 때문에 위의 코드는 다음과 같습니다.
```
var i;
const operations = []

for (i = 0; i < 5; i++) {
  operations.push(() => {
    console.log(i)
    })
}

for (const operation of operations) {
  operation()
}
```
그래서 for-of 루프에서 여전히 i가 사용가능해서 5가 되며 함수에서 i를 참조할 때마다 이 값을 사용하게 됩니다. 그러면 우리가 원하는 대로 동작하게 할려면 어떻게 해야 할까요? 간단한 방법은 let 정의를 사용하는 것입니다. ES^에서 소개된 let은 var 정의와 관련된 이상한 것들을 피하는데 큰 도움이 됩니다. 루프내의 var를 let으로 바꾸면 잘 동작하게 됩니다.

```
const operatios = []

for (let i = 0; i < 5; i++) {
  operations.push(() => {
    console.log(i)
    })
}

for (const operation of operations) {
  operation()
}
```
결과는 다음과 같습니다
```
0
1
2
3
4
```
어떻게 이렇게 된걸까요? 이 경우에서는 매 루프마다 i가 새롭게 만들어지고 operations에 추가된 모든 함수는 자기 자신의 i를 가지게 됩니다. 이경우에 const를 사용할 수 없는 것을 기억하세요, 왜냐하면 for가 두 번째에 새로운 순회의 값을 할당하는 순간 에러가 발생합니다.

이 문제를 해결하는 다른 방법은 IIFE를 사용하는 것입니다. 이경우에 함수 전체를 i와 연결할 수 있습니다. 이 방법은 함수를 만들고 바로 사용하는 것이지만 새로운 함수를 리턴받게 되므로 나중에 실행할 수 있습니다.
```
const operations = []

for (var i = 0; i < 5; i++) {
  operations.push(((j) => {
    return () => console.log(j)
    })(i))
}

for (const operation of operations) {
  operation()
}
```
<a href="https://flaviocopes.com/javascript-array/">JavaScript Arrays</a>
자바스크립트의 배열은 시간이 지나면서 많은 피처를 갖게 되었고 때로는 어떤 생성자를 사용해야되는지 헷갈립니다. 이 포스트는 최근 자바스크립트에서 써야하는 것에 대해 설명하는데 중점을 두겠습니다.
## Initialize array

## Get length of the array

## Iterating the array
### Every
### Some
### 배열을 순회하고 리턴된 함수의 결과를 가지는 새로운 배열을 리턴 (Map)
### Filter an array
### Reduce
### forEacch
### for..of
### for
### @@iterator

## Adding to an array
### Add at the end
### Add at the begining

## Removing an item from an array
### From the end
### From the beginning
### At a random position

## Remove and insert in place
## Join mutiple arrays

## Lookup the array for a specific element
### ES5
### ES2015

### ES2016
## Get a portion of an array
## Sort the array
## Get a string representation of an array
## Copy an existing array by value
## Copy just some values from an existing array
## Copy portions of an array into the array itself, in other positions
<a href="https://flaviocopes.com/javascript-template-literals/">JavaScript Template Literals</a>

<a href="https://flaviocopes.com/javascript-automatic-semicolon-insertion/">JavaScript Semicolons</a>

<a href="https://flaviocopes.com/javascript-strict-mode/">Strict Mode</a>
