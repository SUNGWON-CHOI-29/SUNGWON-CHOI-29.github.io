---
layout: post
title: Node.js 교과서 학습 정리 (5)
description: >
  Node.js 교과서(조현영) 책을 바탕으로 학습 내용을 정리한 포스팅 입니다.
author: author
comments: true
---

Node.js 교과서 학습 정리 (5)

노드만을 사용하여 웹 서버를 만들기에는 코드가 깔끔하지 못하고 확장성도 떨어지기 때문에 편의 기능을 추가한 웹 서버 프레임워크가 있다. 대표적인 것이 익스프레스며 koa, hapi같은 것도 있다.

## 익스프레스 웹 서버 만들기

### Express-generator로 빠르게 설치하기

* 익스프레스 프레임워크는 다른 패키지도 많이 사용하므로 필요한 패키지만 찾아서 설치하기 까다롭다. 그래서 Express-generator 패키지를 사용하면 쉽게 설치할 수 있다.

* `express <프로젝트 명>` 으로 새로운 익스프레스 프로젝트를 만들 수 있고 해당 프로젝트로 이동하여 `npm start` 명령어를 이용해 익스프레스를 실행할 수 있다. localhost:3000 으로 접속하면 확인할 수 있다.

### 익스프레스 구조 이해하기

* 익스프레스는 코드가 여러 개의 파일로 분리되어 있는데 각 부분마다 맡은 역할이 나누어져 있어서 관리하기 편하다.
* bin/www - http 모듈에 express를 연결하고 포트를 지정하는 부분이다.
* app.js - 익스프레스의 핵심이라고 할 수 있는 미들웨어로 요청과 응답의 중간에 위치한다. 라우터와 에러 핸들러 또한 미들웨어의 일종이다.

### 미들웨어

* 미들웨어 - 서버가 받은 요청은 미들웨어를 타고 라우터까지 전달되며 미들웨어 안에서 next()를 호출해야 다음 미들웨어로 넘어갑니다.
* morgan - 요청에 대한 정보르르 콘솔에 기록해주는 미들웨어 입니다.
* body-parser - 요청의 본문을 해석해주는 미들웨어 입니다.
* cookie-parser - 해당 미들웨어는 요청에 들어있는 쿠키를 해석해 줍니다.
* static - 해당 미들웨어는 정적인 파일들을 제공합니다.
* express-session - 세션 관리용 미들웨어로 세션을 구현할 때 유용합니다.
* connect-flash - 일회성 메시지들을 웹 브라우저에 나타낼 수 있는 미들웨어입니다.

### Router 객체로 라우팅 분리하기

* 익스프레스를 사용하는 이유 중 하나가 바로 라우팅을 깔끔하게 관리할 수 있기 때문이다. 라우터에서는 반드시 요청에 대한 응답을 보내거나 에러 핸들러로 요청을 넘겨야 합니다. 응답을 보내지 않으면 브라우저는 계속 응답을 기다립니다.

* 라우터 주소에는 특수한 패턴을 사용할 수 있는데 **:id** 형태가 있습니다. 이 부분에는 다른 값을 넣을 수 있는 것으로 /user/1, /user/123의 요청도 해당 라우터에 걸립니다. 해당 데이터는 req.params 객체 안에 들어있습니다. 쿼리 스트링의 경우 req.query 객체 안에 들어있습니다.

### 템플릿 엔진 사용하기

* HTML은 정적인 언어입니다. 템플릿 엔진은 자바스크립트를 사용해서 HTML을 렌더링할 수 있게 해줍니다. 대표적인 템플릿 엔진으로 Pug와 EJS가 있습니다.
* Pug - 예전 이름은 Jade이며 문법이 간단하여 코드의 양이 줄어드는 장점이 있습니다.
* EJS - HTML 문법을 그대로 사용하되 추가로 자바스크립트 문법을 사용할 수 있습니다.

### 함께 보면 좋은 자료

* <a href="http://expressjs.com">Express 공식 홈페이지 </a>
* <a href="https://pugjs.org">Pug 공식 홈페이지 </a>
* <a href="http://ejs.co">EJS 공식 홈페이지 </a>