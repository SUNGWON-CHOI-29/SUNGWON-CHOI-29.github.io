---
layout: post
title: Node.js Study (5)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (5)

## Expose functionality from a Node.js file using exports
여러분의 응용프로그램의 다른 파일이나 다른 응용프로그램에 데이터를 노출시키는 module.exports API를 어떻게 사용할까요? Node.js에는 내장 모듈 시스템이 있습니다. Node.js 파일은 import되어 기능적으로 다른 Node.js 파일들에 노출될 수 있습니다. import를 하고 싶을 때는 다음과 같이 하면 됩니다.
```
const library = require('./library')
```
이 파일 안에 기능들은 다른 파일에 import 되기 전에 노출될 것입니다. 파일 내에 정의된 다른 객체나 변수들은 기본적으로 비공개로 바깥 세상에 노출되지 않을 것입니다. 이것이 module 시스템에 의해 module.export API가 우리에게 제공하는 것입니다.

여러분이 export 프로퍼티로 새로운 객체나 함수를 할당하면 그것도 노출될 것입니다. 그 결과로 여러분의 앱이나 다른 앱에 import될 수 있습니다. 이렇게 하는 데에는 두가지 방법이 있습니다.

첫번째 방법은 module.export에 모듈 시스템에 의해 외부로 전달될 객체를 할당하여 여러분의 파일ㅇ이 해당 오브젝트만 export하게 되는 것입니다.
```
const car = {
  brand: 'Ford',
  model: 'Fiesta'
}

module.exports = car

//.. in the other file

const car = require('./car')
```

두번째 방법은 exports의 프로퍼티로 export될 객체를 추가하는 것입니다. 이것은 여러분에게 다수의 함수, 데이터, 객체를 export할 수 있게 해줍니다.
```
const car = {
  brand: 'Ford',
  model: 'Fiesta'
}

exports.car = car
//or directly

exports.car = {
  brand: 'Ford',
  model: 'Fiesta'
}
```
그리고 다른 파일에서는 import한 프로퍼티를 조회하여 사용할 수 있습니다.
```
const items = require('./items')
items.car
//or
const car = require('/.items').car
```
module.exports와 exports의 차이점은 무엇일까요? 전자는 가리키는 객체를 노출시키는 것이고 후자는 객체의 프로퍼티들을 노출시키는 것입니다.

## Introduction to npm
npm은 node package manager입니다. 2017년 1월 35만개의 패키지들이 npm등록소에 리스트되어 있고 세상에서 가장 큰 단일 언어 코드 저장소이며 거기에 있는 모든 패키지를 사용할 수 있습니다.

처음에는 Node.js 패키지의 의존성을 관리하고 다운로드하는 데 사용되었습니다만 지금은 자바스크립트 프론트엔드 개발자들이 사용하는 도구가 되었습니다. npm이 하는 일들은 꽤나 많습니다.
### Downloads
npm은 여러분의 프로젝의 의존성 다운로드를 관리합니다.
### Installing all dependencies
프로젝트에 packages.json 파일이 있다면 npm install을 실행하여 프로젝트가 필요한 모든 것을 node_modules 폴더에 설치할 것입니다. 만약 해당 폴더가 없다면 생성합니다.
### Installing a single package
특정 패키지는 npm install <package-name> 을통해 설치할 수 있으며 다음과 같은 플래그를 추가할 수 있습니다.
* --save : 설치를 하고 package.json 의존성에 추가합니다.
* --save-dev : 설치를 하고 package.json 파일의 dev의존성에 추가합니다.

큰 차이점은 devDependencies는 테스트 라이브러리 같은 개발도구에 사용되며 dependencies는 제품의 번들이라는 것입니다.
### Updating packages
업데이트 또한 npm update 명령어를 통해 쉽게 수행할 수 있습니다. npm은 모든 패키지에 대해서 새로운 버전이 있는지 검사합니다. 특정 패키지의 업데이트 또한 npm update <package-name> 을 통해 수행할 수 있습니다.
### Versioning
일반 다운로드 외에도 npm은 versioning을 지원하기 때문에 패키지의 특정 버전을 설치하거나 여러분이 원하는 버전보다 높거나 낮도록 요청할 수 있습니다.

여러분은 라이브러리가 또다른 주요라이브러리의 특정 버전에만 호환이되는 걸 여러번 보셨을 겁니다. 아니면 최신 릴리즈의 lib에 버그가 있거나 아직 고쳐지지 않았거나 하는 것이 문제를 발생시키게 됩니다. 암시적으로 라이브러리 버전을 지정하는 것도 같은 버전의 패키지를 사용하는 많은 사람들에게 도움이 될 수 있습니다. 그래서 전체 팀이 package.json이 업데이트 되기 전까지 같은 버전을 실행할 수 있게 하는거죠.

모든 경우에 versioning은 많은 도움이 되며 npm은 versioning(semver) 표준을 따릅니다.
### Running Tasks
package.json 파일은 실행될 때 사용할 수 있는 커맨드 명령 작업을 지정하는 포맷을 지원합니다.
```
npm <task-name>
//for example
{
  "scripts": {
    "start-dev": "node lib/server-development",
    "start": "node lib/server-production"
  }
}
```
일반적으로 이 기능을 사용해서 웹팩을 실행합니다.
{
  "scripts": {
    "watch": "webpack --watch --progress --colors --config webpack.conf.js",
    "dev": "webpack --progress --colors --config webpack.conf.js",
    "prod": "NODE_ENV=production webpack -p --config webpack.conf.js",
  }
}
그래서 잊어버리기도 쉽고 잘못입력할 수도 있는 저런 긴 명령어 대신에 다음과 같이 짧게 실행할 수 있습니다.
```
$ npm watch
$ npm dev
$ npm prod
```

## Where does npm install the packages?
npm(or yarn)을 이용해서 패키지를 설치할 때 여러분은 두가지 종류의 설치를 수행할 수 있습니다.
* 로컬 설치
* 글로벌 설치
기본적으로 <b>npm install</b> 명령어는 다음과 같습니다. <b>npm install loadsh</b> 패키지는 현재 파일트리에 <b>node_module</b> 하위파일 내에 설치됩니다. 이 과정에서 npm은 현재 폴더에있는 package.json 파일의 dependecies 프로퍼티에 loadsh 엔트리를 추가합니다.

global 설치는 -g 플래그를 사용해서 수행할 수 있습니다.
```
npm install -g loadsh
```
이 과정에서 npm은 로컬 폴더에 패키지를 설치하는 대신에 전역 로케이션에 설치할 것입니다. 정확히 어디일까요? <b>npm root -g</b>명령어가 정확한 위치를 알려줄 것입니다. macOS나 리눅스에서는 아마 <b>/usr/local/lib/node_modules</b> 디렉토리 일 것입니다. 윈도우에서는 <b>C:\\Users\\YOU\\AppData\\Roaming\\npm\\node_modules</b> 경로가 될 것입니다.

Node.js 버전 관리를 위해서 nvm을 사용하고 있다면 해당 경로는 다를 수 있습니다.

## How to use or execute a package installed using npm
### How to include and use in your code a package installed in your node_modules folder
npm을 사용해서 로컬 node_modules 폴더나 전역 경로에 설치했다면 여러분의 Node 코드에서 어떻게 사용할 수 있을까요? <b>npm install lodash</b>를 사용해서 유명한 자바스크립트 유틸리티 라이브러리를 통해 알아봅시다.

이 명령어는 로컬 node_modules 폴더에 해당 패키지를 설치할 것입니다. 여러분의 코드에서 사용하기 위해서는 require를 이용해서 여러분의 코드에 import를 하면 됩니다.
```
const _ = require('lodash')
```
여러분의 패키지가 실행가능하다면 어떻게 해야할 까요? 이 경우에는 ndoe_modules/.bin/폴더에 실행가능한 파일을 넣어두면 됩니다. 이것을 시연해 볼수 있는 쉬운 방법중 하나는 <a href="https://www.npmjs.com/package/cowsay">cowsay</a>입니다.

cowsay 패키지는 무언가를 말하는 소를 만드는 실행 가능한 커맨드 라인 프로그램을 제공합니다. <b>npm install cowsay</b>를 통해 패키지를 설치하면 node_modules 폴더에 몇가지 의존성을 설치할 것입니다. 거기에 숨겨진 .bin 폴더가 있는데 cowsay 바이너리의 심볼릭 링크를 가지고 있습니다. 어떻게 그것들을 실행할까요?

당연히 <b>./node_modules/.bin/cowsay</b>를 통해 실행할 수 있고 동작할 것입니다. 5.2 이후의 npm에 포함된 npx에서는 더 간단합니다. 그냥 <b>npx cowsay</b>라고 입력하면 npx가 패키지 경로를 찾을 것입니다.
