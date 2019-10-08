---
layout: post
title: Node.js Study (1)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---

## Node.js frameworks and tools
Node.js는 저수준 플랫폼 입니다. 개발자들이 더욱 재밌고 쉽게 개발하기 위해서 수천개의 라이브러리들이 내장되어 있습니다.

많은 것들은 시간이 지나면서 인기있는 옵션으로 인정되었습니다. 다음은 제가 개인적으로 배우는게 가치가 있다고 생각하는 리스트들입니다.
* <a href="https://expressjs.com/">Express</a> - 웹서버를 만드는데 가장 강력하고 쉬운 방법 중 하나 입니다. 서버의 핵심기능에 집중하고 최소화된 접근방식으로 성공을 했죠
* <a href="https://flaviocopes.com/meteor/">Meteor</a> - 매우 강력한 풀스택 프레임워크로서 클라이언트와 서버의 자바스크립트 코드를 공유하며 앱을 만들 수 있게 해줍니다. 모든 것을 제공했던 이 도구는 이제 React, Vue, Angular 같은 프론트엔드 라이브러리와 통합됩니다. Meteor는 모바일 앱을 만드는 데도 사용될 수 있습니다.
* <a href="http://koajs.com/">Koa</a> - Express 개발진에서 만들었으며 Koa는 더욱 쉽고 작게 앱을만드 최상의 지식을 구축했습니다. 이 프로젝트는 기존의 커뮤니티를 방해하지 않으면서 호환되지 않는 변경사항을 만들기 위해 시작되었습니다.
* <a href="https://flaviocopes.com/nextjs/">Next.js</a> - 리액트 어플리케이션을 서버 사이드에서 렌더하는 프레임워크 입니다.
* <a href="https://github.com/zeit/micro">Micro</a> - 비동기 HTTP 마이크로 서비스를 만드는 아주 가벼운 서버입니다.
* <a href="https://socket.io/">Socket.io</a> - 네트워크 응용프로그램을 만드는 실시간 통신 엔진입니다.

## A brief history of Node.js
### 2009년에서 오늘까지 돌아보는 Node.js의 역사
믿기지 않으실 수도 있는데 Node.js는 이제 9살이 되었습니다.

자바스크립트가 23살이고 우리가 알고 있는 웹(Mosaic)은 25살이죠.

기술의 영역에서 9년은 매우 짧은 기간이지만 Node.js는 영원히 곁에 있어왔습니다.

저는 운이 좋게도 Node.js가 2살쯤 된 초기에 작업을 하게 되었고 사용할 수 있는 정보가 적었음에도 불구하고 여러분은 Node.js가 아주 큰 녀석이라는 것을 이미 느끼셨을 겁니다.

이 영역에서는 Node.js의 역사를 관통하는 큰 그림을 그려보겠습니다.

### A little bit of history
자바스크립트는 Netscape에서 Netscape Navigator 브라우저 냉에 웹 페이지를 조작하는 스크립팅 툴 언어입니다.

넷스케이프의 비즈니스 모델 중 일부는 웹 서버를 파는 것이었고 Netscape LiveWire라는 환경이 포함되어 있었고 서버쪽에서 자바스크립트를 이용해 동적 페이지들을 만들 수 있었습니다. 그래서 서버쪽에서 자바스크립트를 쓰는 아이디어는 Node.js에서 처음 쓰는게 아니라 자바스크립트 만큼 오래된 것입니다. 다만 그때는 성공하지 못했죠.

Node.js의 부흥을 이끈 요소중에 하나는 타이밍 입니다. 몇년전 자바스크립트는 중요한 언어로 고려되기 시작했고 Web 2.0 응용프로그램이 웹에서 할 수 있는 최신 경험을 보여줬기 때문입니다(구글맵이나 Gmail을 생각해보세요)

자바스크립트 엔진의 성능은 브라우저 경쟁으로 인해 엄청나게 상승했고 아직도 좋아지고 있습니다. 각 주요 브라우저의 개발팀은 우리에게 더욱 향상된 성능을 제공하기 위해서 매일같이 노력을 하고 있으며 자바스크립트 플랫폼에서는 매우 큰 이익인 것이죠. Node.js에서 쓰는 크롬 V8엔진이 그 중 하나이며 크롬 자바스크립트 엔진입니다.

물론 Node.js가 단지 운이 좋거나 타이밍이 좋기 때문에 인기를 얻은 것은 아닙니다. 자바스크립트로 서버를 프로그램하는 데에 있어서 많은 혁신적인 생각을 제시했습니다.

### 2009
Node.js 탄생, npm의 첫 형태가 만들어짐

### 2010
Express와 Socket.io가 탄생

### 2011
npm 1.0 도달

링크드인, 우버같은 큰 회사가 노드를 채택하기 시작함

Hapi가 탄생

### 2012
Node.js 채택이 가파르게 상승함

### 2013
처음으로 대형 블로그 플랫폼인 고스트에서 Node.js를 사용함

Koa의 탄생

### 2014
IO.js는 Node.js의 주요 fork이며 ES6 지원을 달성과 더욱 빨라짐

### 2015
Node.js Foundation 탄생

IO.js가 Node.js로 다시 통합됨

npm이 비공개 모듈을 소개함

Node 4가 출시됨

### 2016
Node6에서 Yarn이 탄생

<a href="https://blog.npmjs.org/post/141577284765/kik-left-pad-and-npm">leftpad 사건</a>

### 2017
Node8에서 npm이 더욱 보안에 초점을 맞춤

HTTP/2 탄생

V8에서 노드를 테스트에 포함시키고 크롬에 추가되는 자바스크립트 엔진으로 Node를 공인함

매주마다 3억회의 다운로드가 npm에서 발생

### 2018
Node 10 탄생,

ES modules 탄생

mjs 실험적 지원

## How to install Node.js
Node.js를 여러분에 시스템에 설치하는 방법에는 패키지 매니저, 공식 웹사이트 인스톨러, nvm이 있습니다. Node.js가 다양한 방식으로 설치될 수 있기 때문에 여기서는 가장 일반적이고 편한 방법에 집중하겠습니다.

Node.js를 설치하는 가장ㅇ 쉬운 방법은 패키지 매니저를 사용하는 것입니다. macOS에서 홈브루는 de-facto 표준이며 설치 후 다음 명령어로 Node.js를 쉽게 설치할 수 있습니다.

```
brew install node
```

nvm은 노드를 실행시키는 유명한 방법입니다. Node.js의 버전을 쉽게 바꿀 수 있고 새로운 버전을 설치하고 뭔가 안될 경우 쉽게 롤백할 수 있습니다. 오래된 Node.js버전에서 여러분의 코드를 테스트 할 때도 매우 유용합니다.

## How much javaScript do you need to know to use Node.js?
여러분이 자바스크립트를 막 시작했다면 얼마나 깊게 알아야 할까요?

입문자라면 여러분의 프로그래밍 능력이 충분한 지점이 어딘지 알기 어렵습니다.

코딩을 하다보면 어디에서 자바스크립트가 끝나고 Node.js가 시작되는지 혼란스러울 수 있습니다.

Node.js를 시작하기 전에 다음과 같은 자바스크립트의 주요 개념을 확실히 익히시길 추천드립니다.
* Lexical Structure
* Expressions
* Types
* Variables
* Functions
* this
* Arrow Functions
* Loops
* Loops and Scope
* Arrays
* Template Literals
* Semicolons
* Strict modules
* ES6
이정도 개념이 머리속에 잡힌다면 숙련된 자바스크립트 개발자가 되는 길을 잘 가고 계신겁니다.

다음의 컨셉은 비동기 프로그래밍을 익히는 주요한 개념이며 Node.js의 기본 중 하나입니다
* Asynchronous programming and callbacks
* Timers
* Promises
* Async and Await
* Closures
* The Event Loop

다행히 제가 위의 모든 주제를 다루는 <a href="https://flaviocopes.com/javascript/">JavaScript Fundamentals.</a> 무료 이북을 저서했습니다.

(위의 내용을 먼저 숙지하고 Node.js 학습을 계속 진행하겠습니다.)
