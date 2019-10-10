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
함수 내부의 구문이 한줄이라면 중괄호를 없애고 모든 것을 한줄에 작성할 수 있습니다.
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
이 짧은 문법 덕분에 화살표 함수는 작은 함수의 사용을 장려합니다.
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
```
const a = []
const a = [1,2,3]
const a = Array.of(1,2,3)
const a = Array(6).fill(1)
//타입이 있는 배열을 제외하고는 아래와 같은 예전 문법을 쓰지마세요
const a = new Array() //쓰지마세요
const a = new Array(1, 2, 3) //마찬가지입니다.
```

## Get length of the array
```
const l = a.length
```

## Iterating the array
### Every
```
a.every(f)
//f()가 false를 리턴할 때까지 순회합니다
```

### Some
```
a.some(f)
//f()가 true를 리턴할 때 까지 순회합니다.
```

### 배열을 순회하고 리턴된 함수의 결과를 가지는 새로운 배열을 리턴 (Map)
map()을 배열에다 호출하면 원본 배열의 모든 아이템에다 함수를 실행한 결과를 담은 새로운 배열을 만듭니다.
```
const a= [1, 2, 3]
const b = a.map((v, k) => v * k)
// b = [0, 2, 6]
// const b = a.map(f)
// a를 순회하며 a의 모든 원소에대한 f()의 결과를 담은 새로운 배열을 만듭니다.
```

### Filter an array
```
const b = a.filter(f)
//a를 순회하며 a의 모든 원소중 f()의 결과가 true인 원소를 담은 새로운 배열을 만듭니다.
```

### Reduce
```
a.reduce((accumulator, currentValue, currentIndex, array) => {
    //...
  }, initialValue)
```
reduce() 배열의 모든 원소에 대해 콜백 함수를 실행하고 점진적으로 결과를 계산합니다. 만약 초기값이 설정되어 있다면 처음 순회의 accumulator 값은 초기값과 똑같을 것입니다.

예제
```
;[1, 2, 3, 4].reduce((accumulator, currentValue, currentIndex, array) => {
  return accumulator * currentValue
  }, 1)
// iteration 1: 1 * 1 => return 1
// iteration 2: 1 * 2 => return 2
// iteration 3: 2 * 3 => return 6
// iteration 4: 6 * 4 => return 24

//return value is 24
```

### forEach
```
a.forEach(f)
// ES6
// a에 대해 순회를 함, 중단할 수 없음
a.forEach(v => {
  console.log(v)
  })
```

### for..of
```
for (let v of a) {
  console.log(v)
}
//ES6
```

### for
```
for (let i = 0; i < a.length; i += 1) {
  //a[i]
}
//a를 순회하지만 return이나 break로 중단할 수 있고 continue를 사용해 다음 순회로 넘어갈 수 있습니다.
```

### @@iterator
* ES6, 배열에서 값들을 리턴하는 순회자를 가져옵니다.

```
const a = [1, 2, 3]
let it = a[Symbol.iterator]()

console.log(it.next().value) //1
console.log(it.next().value) //2
console.log(it.next().value) //3
```

* entries() 키/밸류 한쌍의 순회자를 리턴합니다

```
let it = a.entries()

console.log(it.next().value) //[0, 1]
console.log(it.next().value) //[1, 2]
console.log(it.next().value) //[2. 3]
```

* keys()는 키 값에 대한 순회를 허용합니다

```
let it = a.keys()

console.log(it.next().value) //0
console.log(it.next().value) //1
console.log(it.next().value) //2
```

next()는 배열이 끝날 때 undefined를 리턴합니다. 또한 it.next()가 value, done 쌍을 리턴할 때도 배열이 끝이난 것입니다. done은 마지막 원소 전까지는 항상 false이다가 마지막에 true를 리턴합니다.

## Adding to an array
### Add at the end
```
a.push(4)
```

### Add at the begining
```
a.unshift(0)
a.unshift(-2, -1)
```

## Removing an item from an array
### From the end
```
a.pop()
```

### From the beginning
```
a.shift()
```

## At a random position
```
a.splice(0, 2) // 0부터 2개의 아이템을 가져옵니다.
a.splice(3, 2) // 시작에서 인덱스 3만큼 떨어진 위치에서부터 2개의 아이템을 가져옵니다.
```

뒤에 undefined 밸류가 남아있으므로 remove()를 사용하지 마세요.
## Remove and insert in place
```
a.splice(2, 3, 2, 'a', 'b')
// index2부터 3개의 아이템을 삭제하고 2개의 아이템을 더합니다.
// 여전히 index 2부터 시작합니다.
```

## Join mutiple arrays
```
const a = [1, 2]
const b = [3, 4]
a.concat(b) // 1, 2, 3, 4
```

## Lookup the array for a specific element
### ES5
```
a.indexOf()
//처음으로 일치하는 아이템의 인덱스를 리턴합니다, 찾지못한 경우 -1을 리턴합니다.
a.lastIndexOf()
//마지막으로 일치하는 아이템의 인덱스를 리턴합니다, 찾지못한 경우 -1을 리턴합니다.
```

### ES2015
```
a.find((element, index, array) => {
  //true/false를 리턴
  })
//return true일 때 처음으로 매치하는 아이템을 리턴합니다. 찾지못한 경우 undefined를 리턴합니다.
// 일반적으로 쓰이는 문법은 다음과 같습니다
a.find(x => x.id === my_id)
//위의 라인은 배열에서 id === my_id와 일치하는 첫 원소를 리턴합니다
//findIndex는 true일 때 처음으로 일치하는 아이템의 인덱스를 일치하며 찾지 못한경우 undefined를 리턴합니다.
a.findexIndex((element, index, array) => {
  //return true/false
  })
```

### ES2016
```
a.includes(value)
//a가 value를 가지고 있는 경우 true를 리턴합니다.
a.includes(value, i)
i위치에 value를 가지고 있는 경우 true를 리턴합니다.
```

## Get a portion of an array
```
a.slice()
```

## Sort the array
알파벳 순으로 정렬을 합니다 (ASCII value - 0-9A-Za-z)
```
const a = [1, 2, 3, 10, 11]
a.sort() // 10, 10, 11, 2, 3

const b = [1, 'a', 'Z', 3, 2, 11]
b = b.sort() // 1, 11, 2, 3, Z, a
//사용자 정의 함수로 정렬
const c = [1, 10, 3, 2, 11]
c.sort((a, b) => a - b) //1, 2, 3, 10, 11
//배열의 역순으로 정렬
a.reverse()
```

## Get a string representation of an array
```
a.toString() // 배열을 대표하는 문자열을 리턴합니다.
a.join() // 배열의 원소를 이어붙인 문자열을 리턴합니다.
a.join(', ') //사용자 정의 구분자를 매개변수로 넘겨줍니다.
```

## Copy an existing array by value
```
const b = Array.from(a)
const b = Array.of(...a)
```

## Copy just some values from an existing array
const b = Array.from(a, x => x % 2 == 0)
## Copy portions of an array into the array itself, in other positions
```
const a = [1, 2, 3, 4]
a.copyWithin(0, 2) //[3, 4, 3, 4]
const b = [1, 2, 3, 4, 5]
b.copyWithin(0, 2) // [3, 4, 5, 4, 5]
//0은 복사를 넣을 위치이고 2는 복사를 시작하는 위치입니다.
const c = [1, 2, 3, 4, 5]
c.copyWithin(0, 2, 4) // [3, 4, 3, 4, 5]
//4는 끝나는 인덱스를 말합니다.
```

<a href="https://flaviocopes.com/javascript-template-literals/">JavaScript Template Literals</a>
## Introduction to Template Literals
템플릿 리터럴은 ES2015/ES6의 새로운 피처로 ES5와 비교하여 문자열로 혁신적으로 작업할 수 있도록 해줍니다. 문법을 처음 힐끗보면 매우 간단해 보입니다. 따옴표나 쌍따옴표 대신에 그냥 backticks를 사용하면 됩니다.
```
const a_string = `something`
```
이것이 특별한 이유는 그냥 따옴표로 묶어진 보통 문자열은 할 수 없는 많은 기능들을 제공하기 때문입니다.
* 멀티라인 문자열을 정의할 때 굉장한 문법을 제공합니다
* 문자열 내부에서 변수와 expression을 해석하는데 쉬운 방법을 제공합니다
* DSLs를 만들 때 템플릿 태그를 허용합니다. (DSL은 도메인 특정 언어로 리액트에서 쓰이는 Styled Components;(컴포넌트를 위한 CSS)를 말합니다)
더욱 자세히 알아봅시다!

## Multiline strings
ES6 이전에는 2줄 이상의 라인을 만들 때 해당 라인의 뒤에다가 \\캐릭터를 넣어야만 했습니다.
```
const string =
  'first part \
  second part'
```
이것은 두 라인에 걸쳐져 있지만 한줄처럼 표시되죠.
<b>fist part second part</b>
만약 두 줄로 표현되길 원한다면 추가적으로 개행문자를 추가해야 했습니다.
```
const string =
  'first line\n \
  second line'
//or
const string = 'first line\n' + 'second line'
```
템플릿 리터럴은 멀티라인 문자열을 훨씬 쉽게 만들어줍니다. 한번 백틱으로 템플릿 리터럴이 시작되면 그냥 엔터를 입력하면 개행이 됩니다. 그리고 그대로 렌더링이 됩니다.
```
const string = `Hey
this

strings
is awesome!`
```
공백이 의미를 가진다는 것을 주의하세요
```
const string = `First
                Second`
//First
//                Second
```
이 문제를 해결하기 위한 간단한 방법은 첫줄을 비우고 backtick 후에 바로 trim()메소드를 사용하는 것입니다. 그러면 첫번 째 문자열 이전에 어떤 공백이라도 제거할 것입니다.
```
const string = `
First
Second`.trim()
```

## Interpolation
템플릿 리터럴은 변수나 expression을 문자열 내부에서 쉽게 해석될 수 있도록 해줍니다. 단지 ${...}문법만 사용하시면 됩니다.
```
const myVariable = 'test'
const string = `something ${myVariable}` //something test
```
${} 내부에는 expressions를 포함하여 어떤 것이든 추가할 수 있습니다
```
const string = `something ${1 + 2 + 3}`
const string2 = `something ${doSomething() ? 'x' : 'y'}`
```

## Template tags
태그된 템플릿은 처음에는 별로 도움되지 않는 기능같지만 Styled Components나 Apollo, GraphQL 클라이언트/서버 라이브러리 같은 인기있는 라이브러리에서 실제로 사용하는 것입니다. 그러니까 그것들이 어떻게 동작하는지 알기 위해서는 필수적인 것이죠.

Styled Components 템플릿 태그는 CSS 문자열을 정의하는데 쓰입니다.
```
const Button = styled.button`
  fonst-size: 1.5em;
  background-color: black;
  color: white;
`
//아폴로 템플릿 태그는 GraphQL 쿼리 스키마를 정의하는데 사용됩니다.
const query = gql`
  query {
    ...
  }
`
```
styled.button과 gql 템플릿 태그가 강조되는 예제는 함수입니다.
```
function gql(literals, ...expressions) {}
```
이 함수는 모든 종류의 연산 결과를 문자열로 리턴합니다. literals는 expression이 토큰화 되어 삽입되어 있는 템플릿 리터럴의 배열을 가지고 있습니다. expressions는 모든 Interpolation을 가지고 있습니다.
```
const string `something ${1 + 2 + 3}`
```
여기서 리터럴은 두 개의아이템을 가진 배열입니다. 처음은 something 이고 첫번째 Interpolation전까지 두번째는 빈 문자열입니다. expressions는 6이라는 하나의 아이템을 가진 배열입니다. 더욱 복잡한 예제를 봅시다.
```
const string = `something
ansother ${'x'}
new line ${1 + 2 + 3}
test`
```
이 경우에 lterals 배열의 첫번 쨰 아이템은 다음과 같습니다.
```
;`something
another `
```
두번째는 다음과 같습니다.
```
;`
new line`
```
세번째는 다음과 같습니다.
```
;`
test`
```
expression의 배열은 이 경우 x와 6 두개의 아이템을 가지고 있습니다. 위의 값들이 전달된 function은 무엇이든 할 수 있으며 굉장히 강력한 특징입니다.

문자열 삽입이 수행하는일을 따라하는 가장 쉬운 예제는 literals와 expressions를 합치는 것입니다.
```
const interpolated = interpolated `I paid ${10}€`
```
그리고 interpolate가 동작하는 것은 다음과 같습니다.
```
function interpolate(literals, ...expressions) {
  let string = ``
  for (const [i, val] of expressions.entries()) {
    string += literals[i] + val
  }
  string += literals[literals.length - 1]
  return string
}
```

<a href="https://flaviocopes.com/javascript-automatic-semicolon-insertion/">JavaScript Semicolons</a>

커뮤니티에서 자바스크립트의 세미콜론은 커뮤니티를 나눕니다. 누구는 항상 사용하길 선호하고 누구는 상관하지 않죠. 다른사람들은 최대한 안쓰려고 합니다. 세미콜론을 항상 써오다가 2017년 가을에 저는 최대한 안쓰기로 했죠 그리고 저는 Prettier를 설정해서 자동적으로 코드에 세미콜론을 지우도록 했습니다 그러나 특정 코드들은 세미콜론을 필요로 합니다.

저는 이제 자연스럽게 세미콜론을 안쓰게 되었고 코드도 더욱 쉽게 읽히는것 같습니다. 이것은 모두 자바스크립트가 세미콜론을 엄격하게 요구하지 않기 때문입니다. 만약 세미콜론이 필요한 자리라면 알아서 추가해줍니다. 강력한 세미콜론의 규칙을 아는 것은 중요합니다. 왜냐하면 여러분이 작성한 코드에서 의도하지 않은 버그가 생길 수도 있기 때문이죠.
## The rules of JavaScript Automatic Semicolon Insertion
자바스크립트 파서는 소스코드를 파싱하면서 특정 경우에 자동적으로 세미콜론을 추가합니다.
1. 다음 줄의 코드가 현재의 코드를 멈추면서 시작할 때 (코드는 여러줄로 쓰일 수 있습니다.)
1. 다음 코드 라인이 블록을 닫는 중괄호 } 로 시작될 때
1. 소스 코드의 끝에 도달했을 때
1. 해당 라인에서 return 구문을 만났을 때
1. 해당 라인에서 break 구문을 만났을 때
1. 해당 라인에서 throw 구문을 만났을 때
1. 해당 라인에서 continue 구문을 만났을 때

## Examples of code that does not do what you think
위의 규칙들을 기반으로 아래에 몇몇 예제들을 확인해 봅시다.
```
const hey = 'hey'
const you = 'hey'
const heyYou = hey + ' ' + you

['h', 'e', 'y'].forEach((letter) => console.log(letter))
```
여러분은 Uncaught TypeError: Cannot read property 'forEach' of undefined를 확인하시게 될겁니다. 왜냐면 위의 1의 규칙에 따라 자바스크립트는 코드를 다음과 같이 해석합니다.
```
const hey = 'hey';
const you = 'hey';
const heyYou = hey + ' ' + you['h', 'e', 'y'].forEach((letter) =>
console.log(letter))
```
```
(1 + 2).toString() //"3"

const a = 1
const b = 2
const c = a + b
(a + b).toString() //TypeError: b is not a function
// const a = 1;
// const b = 2;
// const c = a + b(a+b).toString()
```
규칙 4를 기반으로 하는 다른 예제입니다.
```
(() => {
  return
  {
    color: 'white'
  }
  })()
```
여러분은 IIFE가 color 프로퍼티를 가지고 있는 객체를 리턴하길 바라겠지만 그렇지 않습니다. 대신에 undefined가 리턴되는데 그 결과는 자바스크립트가 return 다음에 세미콜론을 추가하기 때문입니다. 그래서 retrun 다음에 바로 여는 괄호를 추가해야 합니다.
```
(() => {
  return {
    color: 'white'
  }
  })()
```
```
1 + 1
-1 + 1 === 0 ? alert(0) : alert(2)
```
위의 코드는 0을 alert에 넣는다고 생각하시겠지만 2가 대신 보여집니다. 왜냐면 규칙 1때문에 다음과 같이 해석됩니다.
```
1 + 1 -1 + 1 === 0 ? alert(0) : alert(2)
```

## Conclusion
주의하세요 어떤 사람은 세미콜론 사용에 매우 완고합니다. 솔직히 저는 별로 상관하지 않습니다, 도구의 옵션에서 사용하지 않음으로 하면 세미콜론을 지워주니까요.

저는 어떤 것도 추천하지 않고 여러분이 스스로 결정을 내리시길 바랍니다.
* return 구문에서 항상 주의하세요, 어떤 것을 리턴할 때 같은 라인에 return을 추가하세요 (break, throw, continue도 마찬가지 입니다.)
* 괄호로 라인을 시작하지마세요, 이전 라인의 함수 호출형태로 연결될 수 있거나 배열의 요소로 조회될 수 있습니다.

그리고 궁극적으로 항상 코드를 테스트 하는 것이 여러분의 의도대로 코드가 동작하는지 확실할 수 있게 해줄 것입니다.

<a href="https://flaviocopes.com/javascript-strict-mode/">Strict Mode</a>

Strict 모드는 ES5의 피처로 자바스크립트가 더욱 나은 방식으로 동작하게 만듭니다. 그리고 또한 다른 방식으로 동작하게 만드는데 Strict Mode를 사용하게 되면 자바스크립트 언어의 문법이 바뀌게 됩니다. 가장 중요한 것은 자바스크립트 코드의 strict 모드와 일반 모드(sloppy mode)의 주요 차이점을 아는 것입니다. Strict 모드는 대개 ES3에서 가능했던 함수들과 ES5이후로 deprecated된 함수를 제거합니다
## How to enable Strict Mode
strict 모드는 선택사항 입니다. 모든 자바스크립트의 주요 변경사항을 언어의 기본 동작으로 바꿀 수 없습니다. 왜냐하면 매우 많은 자바스크립트가 동작하지 않을 것이고 1996년의 자바스크립트 코드가 여전히 동작하도록 많은 노력을 기울이기 때문입니다. 또한 그것이 자바스크립트의 성공의 요인이기도 했구요. 그래서 'use strict'문구를 사용해야 strict 모드를 사용할 수 있습니다. 파일의 시작에 추가할 수 있으며 해당 파일에 있는 모든 코드에 적용됩니다.
```
'use strict'

const name = 'Flavio'
const hello = () => 'hey'

//...
```
여러분은 함수마다 Strict 모드를 설정할 수 있으며 함수 본문의 시작에 'use strict'를 추가하면 됩니다.
```
function hello() {
  'use strict'

  return 'hey'
}
```
이것은 레거시 코드를 동작시킬 때 유용한데 여러분이 테스트할 시간이 없거나 파일 전체에서 strict 모드가 사용가능한지 확신이 없을 때 쓰일 수 있습니다.
## What changed in Strict Mode
### Accidental global variables
정의되지 않은 변수에 값을 추가하면 자바스크립트는 기본적으로 전역 객체에 해당 변수를 추가합니다.
```
;(function() {
  variable = 'hey'
  })()( () => {
    name = 'Flavio'
    })()
variable //'hey'
name //'Flavio'
```
Strict 모드로 변경하면 위의 코드가 에러를 불러 일으킵니다.
```
;(function() {
  'use strict'
  variable = 'hey'
  })()( () => {
    'use strict'
    name = 'Flavio'
    })()
variable //'hey'
name //'Flavio'
```
<center>
<img src= "https://flaviocopes.com/javascript-strict-mode/error-variable-not-defined.png"/>
</center>

### Assignment errors
자바스크립트는 컨버전 에러를 조용하게 처리합니다. Strict 모드에서는 조용했던 에러가 이슈를 발생시킵니다.
```
const undefined = 1(() => {
  'use strict'
  undefined = 1
  })()
```
<center>
<img src= "https://flaviocopes.com/javascript-strict-mode/assignment-errors.png"/>
</center>

무한,NaN, eval, argument 등등에 대해서도 같은 일이 발생합니다.

자바스크립트에서 쓰기가 안되도록 객체의 프로퍼티를 정의할 수 있습니다.
```
const car = {}
  Object.defineProperty(car, 'color', {value: 'blue', writable: false })
```
일반 모드에서는 덮어쓰기가 되지만 strict 모드에서는 에러가 발생합니다.
<center>
<img src= "https://flaviocopes.com/javascript-strict-mode/read-only-property.png"/>
</center>
getter에서도 동일하게 동작합니다.
```
const car = {
  get color() {
    return 'blue'
  }
}
car color = 'red' (
  //ok

  () => {
    'use strict'
    car.color = 'yellow' //TypeError: Cannot set property color of #<object> which has only a getter
  }
)()
```
일반 모드는 확장 불가능한 객체도 확장을 허용합니다.
```
const car = { color : 'blue' }
Object.preventExtensions(car)
car.model = 'Fiesta'(
  //ok

  () => {
    'use strict'
    car.owner = 'Flavio' //TypeError: Cannot add property owner, object is not extensible
  }
)()
```
또한 일반모드에서는 기본 값에 프로퍼티를 설정하는 것이 가능합니다.
```
true.false = ''(
  //''
  1
).name =
  'xxx' //'xxx'
var test = 'test' //undefined
test.testing = true //true
test.testing //undefined
```
Strict 모드에서는 모든 경우에 대해 실패합니다.
```
;(() => {
  'use strict'
  true.false = ''(
    //TypeError: Cannot create property 'false' on boolean 'true'
    1
  ).name =
    'xxx' //TypeError: Cannot create property 'name' on number '1'
  'test'.testing = true //TypeError: Cannot create property 'testing' on string 'test'
})()
```

### Deletion errors
일반 모드에서 삭제할 수 없는 프로퍼티를 삭제할 경우 false를 리턴하지만 Strict 모드에서는 타입에러가 발생합니다.
```
delete Object.prototype(
  //false

  () => {
    'use strict'
    delete Object.prototype //TypeError: Cannot delete property 'prototype' of function Object() { [native code] }
  }
)()
```

### Function arguments with the same name
일반 함수에서는 중복된 파라미터 이름을 가질 수 있습니다.
```
(function(a, a, b) {
  console.log(a, b)
})(1, 2, 3)
//2 3


(function(a, a, b) {
  'use strict'
  console.log(a, b)
})(1, 2, 3)
//Uncaught SyntaxError: Duplicate parameter name not allowed in this context
```
화살표 함수에서는 이경우에 대해 항상 신택스 에러를 발생시키는 것을 기억하세요.
```
((a, a, b) => {
  console.log(a, b)
})(1, 2, 3)
//Uncaught SyntaxError: Duplicate parameter name not allowed in this context
```

### Octal syntax
8진법 문법은 Strict모드에서 사용할 수 없습니다. 기본적으로 숫자앞에 0을 붙임으로써 8진법 숫자 표현과 호환되게 되며 8진법 숫자로 표현되게 됩니다.
```
(() => {
  console.log(010)
})()
//8

(() => {
  'use strict'
  console.log(010)
})()
//Uncaught SyntaxError: Octal literals are not allowed in strict mode.
```
대신에 0oXX문법을 통해 Strict문법에서 8진수를 사용할 수 있습니다.
```
;(() => {
  'use strict'
  console.log(0o10)
})()
//8
```
### Removed with
Strict 모드에서는 with 키워드가 사용불가합니다. 컴파일러 수준에서 더욱 최적화를 하기위해 일부 예외 케이스들을 제거하기 위함입니다.

## Summary
* 자바스크립트 기본 문법 번역 및 정리
