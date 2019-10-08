---
layout: post
title: Node.js Study (2)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---

## Differences between Node.js and the Browser
Node.js에서 작성된 자바스크립트 프로그램과 브라우저 내에 웹에서 프로그래밍된 것은 어떻게 다를까요? 브라우저와 노드 둘다 자바스크립트를 프로그래밍 언어로 사용합니다. 웹에서 빌드된 앱은 Node.js에서 빌드된 응용프로그랩과 완전히 달라지게 됩니다.

모든 것이 자바스크립트라는 사실에도 불구하고 몇몇 사항들이 다르기 때문에 완전히 경험을 만들어 줍니다. 프론트엔드 개발자들은 Node.js로 앱을 만들면 커다란 장점이 있습니다. 언어가 여전히 동일하다는 것이죠.

우리는 프로그래밍 언어를 깊고 완벽하게 배우는게 얼마나 힘든지 알기 때문에 이것은 큰 장점입니다. 웹에서 클라이언트와 서버쪽의 코드가 동일한 언어라는 것은 매우 큰 이점이 될 것입니다.

다른 점은 환경입니다.

브라우저에서는 많은 시간동안 여러분이 하는 것은 DOM이나 쿠키와 같은 다른 웹플랫폼과 상호작용 하는 것입니다. 물론 그런것들은 Node.js에 없죠. 브라우저에서 제공하는 document, window와 같은 다른 객체도 없습니다.

브라우저에서는 Node.js에서 모듈로 제공하는 좋은 API들이 없습니다. 예를 들면 파일시스템 접근 같은 것들 말이죠.

다른 큰 차이점은 Node.js에서 여러분은 환경을 조정할 수 있다는 것입니다. 오픈소스로 누구나 어디에서 배포할 수 있는 응용프로그램을 만드는 것이 아니라면 여러분은 정확히 어떤 버전의 Node.js가 응용프로그램에서 사용되는지 알겁니다. 방문자가 어떤 브라우저를 사용할건지 선택하지 못하는 브라우저 환경과 달리 이것은 매우 편리합니다.

이 말은 여러분의 Node버전이 지원하는 모든 최신 자바스크립트를 사용할 수 있다는 것입니다.(ES6~ES9) 자바스크립트는 매우 빠르게 업그레이드 되지만 브라우저는 좀 느린편이고 사용자는 천천히 업그레이드 하죠. 때때로 웹에서 오래된 자바스크립트를 가지고 작업을 하는 것은 굉장히 골치아플 겁니다. 여러분의 코드를 브라우저에서 사용되기 전에 Babel을 이용해서 ES5에서 호환이 되도록 할 수도 있지만 Node.js에서는 그럴필요가 없습니다.

다른 차이점은 
## The V8 JavaScript Engine

### Other JS engines
### The quest for performance
### Compilation

## How to exit from a Node.js program

## How to read environment variables from Node.js
