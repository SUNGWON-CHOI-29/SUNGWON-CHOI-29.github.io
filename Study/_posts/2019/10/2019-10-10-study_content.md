---
layout: post
title: Node.js Study (4)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (4)

## Node.js, accept arguments from the command line
Node.js 응용프로그램에서 사용하는 매개변수들을 어떻게 커맨드 라인에서 넘겨줄 수 있을까요? 여러분은 Node.js 응용프로그램을 호출할 때 여러개의 매개변수를 전달할 수 있습니다.
```
node app.js
```
매개변수는 독립적이거나 키-밸류 형태입니다.
```
node app.js flavio
//or
node app.js name-flavio
```
이것은 여러분이 Node.js 코드에서 이 값들을 가져오는 방법을 바꿉니다. 해당 값을 가져오기 위해 Node.js에 내장된 process 객체를 사용합니다. 해당 객체에는 argv 프로퍼티가 있는데 이것은 커맨드 라인에서 입력된 매개변수들을 모두 가지고 있는 배열입니다.

첫번쨰 매개변수는 node명령어의 전체 경로입니다. 두번째는 실행될 파일의 전체 경로입니다. 세번쨰 부터는 추가적인 매개변수를 나타냅니다. 여러분은 반복문을 사용해서 모든 매개변수를 순회할 수 있습니다(node,file 경로 포함)
```
process.argv.forEach((val, index) => {
  console.log('{$index}: ${val}')
  })
```
여러분은 배열의 첫 두개 원소를 제거함으로써 추가적인 매개변수만 가지는 배열을 만들 수 있습니다.
```
const args = process.argv.slice(2)
```
다음과 같이 매개변수가 인덱스 이름이 없을 때는 다음과 같이 접근할 수 있습니다.
```
node app.js flavio

const args = process.argv.slice(2)
args[0] //'flavio'
```
다음과 같은 경우에는 매개변수에 키와 밸류가 함께 있으므로 파싱을 해야할 필요가 있습니다. 가장 좋은 방법은 매개변수에 minimist 라이브러리를 사용하는 것입니다.
```
node app.js name=flavio

const args = require('minimist')(process.argv.slice(2))
args['name'] //flavio
```

## Output to the command line using Node.js
어떻게 Node.js를 사용해서 커맨드라인 콘솔에 출력을 할 수 있을까요? 기본 console.log부터 더욱 복잡한 상황을 알아봅시다.
### Basic output using the console module
Node.js는 console 모듈을 통해 커맨드라인과 상호작용할 수 있는 유용한 방법을 많이 제공합니다. 기본적으로 브라우저에서 찾을 수 있는 console 객체와 같습니다.

가장 많이쓰이고 기본적인 메소드는 console.log()로써 콘솔에 넘겨준 문자열을 출력합니다. 객체를 넘겨도 문자열로 출력할 것입니다. console.log에 다음과 같이 여러개의 변수를 전달할 수 있습니다. 그러면 Node.js가 둘다 출력할 것입니다.
```
const x = 'x'
const y = 'y'
console.log(x, y)
```
또한 변수와 포맷 지정자를 전달하여 좀 더 예쁜 서식을 만들 수 있습니다.
```
console.log('My %s has %d years', 'cat', 2)
```

* %s는 변수를 문자열로 만듭니다
* %d, %i는 변수를 정수로 만듭니다
* %f는 변수를 부동소수점으로 만듭니다
* %O는 객체 표현을 출력하기 위해 사용됩니다.
```
console.log('%O', Number)
```

### Clear the console
console.clear()는 콘솔을 지웁니다.(이 동작은 사용되는 콘솔에 의존적입니다.)
### Counting elements
console.count()는 편리한 메소드 입니다. 코드를 보시죠

```
const x = 1
const y = 2
const z = 3
console.count(
  'THe value of x is ' + x + ' and has been checked .. how many times?'
  )
console.count(
  'The value of x is ' + x + 'and has been checked .. how many times?'
  )
console.count(
  'The value of y is ' + y + 'and has been checked .. how many times?'
  )
```
count는 문자열이 출력된 횟수를 세고 그 옆에 출력할 것입니다.
```
const oranges = ['orange', 'orange']
const apples = ['just one apple']
oranges.forEach(fruit => {
  console.count(fruit)
  })
apples.forEach(fruit => {
  console.count(fruit)
  })
```

### Print the stack trace
"코드에 해당 지점에 어떻게 도달했어요?"와 같은 질문에 답변을 하는데 함수의 콜스택 추적을 출력하는 게 매우 도움이 될 것입니다. console.trace()를 사용하면 됩니다.
```
const function2 = () => console.trace()
const function1 = () => function2()
function1()
```
이것은 스택 추적을 출력할 것이고 아래는 Node REPL에서 실행한 결과입니다.
```
Trace
    at function2 (repl:1:33)
    at function1 (repl:1:25)
    at repl:1:1
    at ContextifyScript.Script.runInThisContext (vm.js:44:33)
    at REPLServer.defaultEval (repl.js:239:29)
    at bound (domain.js:301:14)
    at REPLServer.runBound [as eval] (domain.js:314:12)
    at REPLServer.onLine (repl.js:440:10)
    at emitOne (events.js:120:20)
    at REPLServer.emit (events.js:210:7)

```

### Calculate the time spent
time()과 timeEnd()를 사용하면 함수가 동작하는데 얼마나 걸렸는지 쉽게 계산할 수 있습니다.
```
const doSomething = () => console.log('test')
const measureDoingSomething = () => {
  console.time('doSomething()')
  doSomething()
  console.timeEnd('doSomething()')
}
measureDoingSomething()
```

### stdout and stderr
우리는 console.log가 콘솔에서 메시지를 출력하는데 매우 좋다는 것을 살펴봤습니다. 이것은 standard output, stdout이라고 불립니다. console.error은 stderr 스트림에 출력합니다. 콘솔에는 나타나지 않지만 에러로그에 나타납니다.
### Color the output
escape sequence를 사용하여 콘솔에 출력되는 텍스트의 색상을 지정할 수 있습니다. escape sequence는 색을 지정하는 문자들의 집합입니다.
```
console.log('\x1b[33m%s\x1b[0m', 'hi!')
```
Node REPL에서 입력을 하면 hi!가 노란색으로 출력될 것입니다. 그러나 이것은 저수준의 방법입니다. 콘솔 출력에 색상을 입히는 가장 쉬운 방법은 라이브러리를 쓰는 것입니다. <a href="https://github.com/chalk/chalk">Chalk</a>같은 라이브러리는 색상을 입히는 것 외에도 텍스트를 굵게 표현하거나 밑줄, 기울이기 등을 표현하는데 도움이 됩니다.

npm install chalk를 통해 설치할 수 있습니다.
```
const chalk = require('chalk')
console.log(chalk.yellow('hi!'))
```
chalk.yellow를 사용하는 것은 이스케이프 코드를 기억하는 것보다 훨씬 편리하고 가독성도 좋습니다.
### Create a progress bar
<a href="https://www.npmjs.com/package/progress">Progress</a>는 콘솔에 프로그레스 바를 만드는 멋진 패키지 입니다. npm install progress를 통해 설치할 수 있습니다. 아래의 짧은 코드는 10단계의 프로그레스 바를 만들고 매 100ms 마다 한 단계씩 완료됩니다. 바가 모두 채워지면 인터벌을 날립니다.
```
const ProgressBar = require('progress')

const bar = new ProgressBar(':bar', { total: 10 })
const timer = setInterval(() => {
  bar.tick()
  if (bar.complete) {
    clearInterval(timer)
  }
  },100)
```

## Accept input from the command line in Node.js
인터랙티브한 Node.js CLI 프로그램을 어떻게 만들까요? Node 버전 7 이후로 readline 모듈을 통해 이것을 수행합니다. process.stdin 스트림과 같이 Node 프로그램이 실행되는 동안 한번에 한줄 씩 터미널에서 입력을 받는 읽기 가능한 스트림에서 입력을 가져옵니다.
```
const readline = require('readline').createInterface({
  input: process.stdin,
  output: process.stdout
  })
readline.question(\`What's your name?\`, (name) => {
  console.log(\`Hi ${name}!\`)
  readline.close()
  })
```
이 코드는 사용자 이름을 물어보고 텍스트가 입력되고 사용자가 엔터를 치면 인사를 보냅니다. question메소드는 첫번째 질문을 보여주고 사용자 입력을 기다립니다. 엔터가 눌려지면 콜백함수를 호출합니다. 콜백 함수에서 우리는 readline 인터페이스를 닫습니다. readline은 다른 메소드도 여러개 제공하며 위에 링크된 패키지 문서에서 확인할 수 있습니다.

패스워드를 요청할 때는 입력 받은 것을 \*심볼로 대체하여 출력하는 것이 좋습니다. 가장 쉽게 이것을 구현하는 방법은 API 관점에서 매우 비슷한 readline-sync 패키지를 사용하여 바로 처리하는 것입니다. 더욱 완벽하고 추상화 솔루션을 제공하는 것은 <a href="https://github.com/SBoudrias/Inquirer.js">Inquirer.js 패키지</a> 입니다.

npm install inquirer를 통해 설치할 수 있으며 위의 코드와 같은 것을 아래처럼 구현할 수 있습니다.
```
const inquirer = require('inquirer')

var questions = [{
  type: 'input',
  name: 'name',
  message: "What's your name?",
  }]
inquirer.prompt(questions).then(answers => {
  console.log(\`Hi {answers['name']}!\`)
  })
```
Inquirer.js는 여러 선택지를 요청하거나 라디오 버튼, 승인과 같은 다른 것들도 할 수 잇습니다. Node.js에서 제공하는 기본 라이브러리의 대안들을 아는 것은 가치가 있습니다. 그러나 CLI 입력을 다음단계로 가져갈 계획이라면 Inquirer.js는 최선의 선택이 될 것입니다.
