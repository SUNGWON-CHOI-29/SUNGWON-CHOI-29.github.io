---
layout: post
title: Node.js 교과서 학습 정리 (2)
description: >
  Node.js 교과서(조현영) 책을 바탕으로 학습 내용을 정리한 포스팅 입니다.
author: author
comments: true
---

Node.js 교과서 학습 정리 (2)

## 알아두어야 할 자바스크립트

1. ES2015+  
1. 함께 보면 좋은 자료

### ES2015+

* ES2015 이상의 자바스크립트 버전부터 다른 언어의 장점을 본딴 편리한 기능이 많이 추가되었다
* var의 경우 블록스코프가 아닌 함수스코프였기 때문에 문제가 발생했다. 웬만하면 const로 변수를 선언하는 것이 좋다. 가변적일 경우 let
* 화살표 함수의 경우 편리하게 사용할 수 있으나 this의 스코프가 다르다. 객체의 메소드로써 사용하기에는 부적절하다
* 비구조화 할당은 const [node, obj, , bool] = array 와 같이 한번에 구조화된 데이터들을 따로 담는 것이다
* 콜백 문제를 해결하기 위한 프로미스와 프로미스의 사용성을 향상시킨 async/await 키워드가 추가되었다.

### 함께 보면 좋은 자료

* <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/New_in_JavaScript/ECMAScript_6_support_in_Moazilla">ES2015 설명</a>
* <a href="http://kangax.github.io/compat-table/es6">EC2015+ 브라우저/서버 호환 여부</a>
* <a href="http://node.green">노드 버전별 ECMAScript 스펙</a>
* <a href="https://developer.mozilla.org/ko/docs/Web/Guide/AJAX">AJAX 설명</a>
* <a href="http://eslint.org">ESLint 툴</a>
* <a href="https://github.com/airbnb/js/javascript">Airbnb 코딩 스타일</a>

## 노드 기능 알아보기

1. REPL, JS 파일 사용하기
1. 모듈로 만들기
1. 노드 내장 객체 알아보기
1. 노드 내장 모듈 사용하기
1. 파일 시스템 접근하기
1. 이벤트 이해하기
1. 예외 처리하기
1. 함께 보면 좋은 자료

### REPL, JS 파일 사용하기

자바스크립트는 스크리븥 언어이므로 미리 컴파일을 하지않고 한줄 한줄 코드를 해석하여 실행한다. REPL(read eval print loop)의 축약어로 노드에서 제공하는 콘솔입니다. 터미널에서 node를 입력하면 사용할 수 있습니다. **한두 줄짜리 코드를 테스트하기엔 좋지만 여러줄의 코드를 실행하기에는 불편합니다** REPL에 직접 코드를 입력하는 대신 자바스크립트로 파일을 만들어 실행할 수 있습니다. JS 파일 실행은 **node [자바스크립트 파일 경로]** 를 사용해서 할 수 있습니다.

### 모듈로 만들기

* 모듈이란 특정한 기능을 하는 함수나 변수들의 집합입니다.
* 자체로도 하나의 프로그램이면서 다른 프로그램의 부품으로 사용할 수도 있습니다.
* 보통 파일 하나가 모듈 하나가되며 모듈화를 통해 재사용성을 올릴 수 있습니다.

### 노드 내장 객체 알아보기

* global - 전역 객체로서 모든 파일에서 접근할 수 있습니다. 파일이 많아질 수록 전역 스코프에 해당하는 변수나 객체를 관리하기 어려우므로 전역 스코프는 남용하지 않는 것이 좋습니다.
* console - 디버깅을 위해 사용되며 .log 메소드가 일반적으로 쓰입니다. 시간측정을 위한 .time 메소드와 객체를 표시하기 좋은 .dir 메소드가 있습니다.
* process.env - 환경 변수를 나타내는 것으로 서비스의 중요한 키를 저장하는 공간으로도 사용됩니다.

### 노드 내장 모듈 사용하기

* os - 운영체제의 정보를 가지고 있는 모듈입니다.
* crypto - 다양한 방식의 암호화를 도와주는 모듈입니다.

### 파일 시스템 접근하기

* 파일시스템 접근에는 동기 메소드와 비동기 메소드가 있습니다. 동기로 파일처리를 하면 매우 시간이 낭비됩니다.
* 비동기 처리를 동기처리 하는 것처럼 동작하고 싶다면 콜백이나 promise, async/await를 사용하면 됩니다.
* 파일을 읽을 때 한번에 파일크기 만큼 읽어들이는 것이 버퍼입니다.
* 반면 스트림은 파일을 청크로 쪼개어 청크가 준비가 되면 바로바로 보내줍니다. 버퍼를 작게 만들어 여러번 보내는 개념입니다.

### 함께 보면 좋은 자료

* <a href="https://nodejs.org/dist/latest-v10.x/docs/api">노드 공식 문서</a>
* <a href="https://nodejs.org/dist/latest-v10.x/docs/api/process.html#process_event_uncaughtexception">uncaughtException</a>
* <a href="https://nodejs.org/dist/latest-v10.x/docs/api/fs.html#fs_fs_promises_api">fs 프로미스</a>
