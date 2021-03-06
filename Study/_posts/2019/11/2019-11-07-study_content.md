---
layout: post
title: Node.js 교과서 학습 정리 (1)
description: >
  Node.js 교과서(조현영) 책을 바탕으로 학습 내용을 정리한 포스팅 입니다.
author: author
comments: true
---

Node.js 교과서 학습 정리 (1)

## 1장 노드 시작하기

1. 핵심 개념 이해하기
1. 서버로서의 노드
1. 서버 외의 노드
1. 함께 보면 좋은 자료

### 핵심 개념 이해하기

* Node.js는 크롬 V8 자바스크립트 엔진으로 빌드된 자바스크립트 런타임입니다. Node.js는 **이벤트 기반, 논블로킹 I/O 모델 을 사용** 해서 가볍고 효율적입니다. Node.js의 패키지 생태계인 npm은 세계에서 가장 큰 오픈 소스 라이브러리 생태계이기도 합니다.
* 노드는 서버로만 사용되는 것이 아닙니다. 자바스크립트 프로그램을 운영하는 런타임으로도 사용할 수 있습니다.

#### 서버와 런타임

* 서버란 네트워크를 통해 클라이언트에 정보나 서비스를 제공하는 컴퓨터, 프로그램을 말합니다.
* 노드는 자바스크립트 응용프로그램이 서버로서 기능하기 위한 도구를 제공합니다.
* 런타임은 특정 언어로 만든 프로그램들을 실행할 수 있는 환경입니다.
* 크롬의 v8엔진이 매우 빨랐기 때문에 브라우저 외의 환경에서 자바스크립트를 실행할 수 있게 되었습니다.

노드는 V8과 더불어 libuv라는 라이브러리를 사용하는데 해당 라이브러리는 노드의 특성인 이벤트 기반, 논블로킹 I/O 모델을 구현하고 있습니다.

#### 이벤트 기반과 논블로킹 I/O 모델

* 이벤트 기반이란 이벤트가 발생할 때 미리 지정해둔 작업을 수행하는 방식입니다.
* 이벤트 리스너에 콜백 함수를 등록함으로써 사용합니다.
* 이벤트 루프를 통해 동시에 발생한 이벤트를 순서대로 처리합니다.
* 태스크 큐는 이벤트 발생 후 호출되어야 할 콜백 함수들이 기다리는 공간입니다.
* 백그라운드는 타이머나 I/O 작업 콜백, 이벤트 리스너들이 대기하는 곳입니다.
* 논블로킹이란 이전 작업이 완료될 때까지 멈추지 않고 다음 작업을 수행함을 뜻합니다. **자바스크립트는 싱글 스레드이므로 I/O 작업 외에 모든 코드가 시간적 이득을 볼 수 있는 것은 아닙니다.**
* 노드는 스레드를 늘리는 대신 프로세스 자체를 복사해 여러 작업을 처리하는 멀티 프로세싱 방식을 채택했습니다.
* cluster 모듈과 pm2 패키지를 활용해 멀티 프로세싱을 수행합니다.

### 서버로서의 노드

* 노드 서버는 단일 스레드이기 때문에 컴퓨터 자원을 적게사용 하지만 CPU 코어를 하나밖에 사용하지 못합니다.
* I/O가 많은 작업에 적합합니다만 CPU 부하가 큰 작업에는 적합하지 않습니다.
* 멀티 스레드 방식보다 프로그래밍이 쉽습니다. 그러나 단일 스레드가 에러로 멈추지 않도록 잘 관리해야 합니다.
* 노드는 개수는 많지만 크기가 작은 데이터를 실시간으로 주고 받는데 적합합니다. **실시간 채팅 앱, JSON 데이터를 제공하는 API 서버에 적합합니다.**
* 이미지, 비디오, 대규모 데이터 처리와 같이 CPU를 많이 사용하는 작업을 위한 서버로는 부적합

### 서버 외의 노드

* 노드의 사용 범위가 늘어나 웹, 모바일, 데스크톱 앱 개발에도 쓰이고 있습니다.
* 대표적인 웹 프레임워크로 Angular, React, Vue, Meteor가 있습니다.

### 함께보면 좋은 자료

* <a href="https://nodejs.org/en/guides"> 노드 공식사이트의 가이드 </a>
* <a href="https://latentflip.com/loupe"> 이벤트 루프에 대한 시각적 설명 </a>
* <a href="https://nodejs.org/ko/docs/guides/event-loop-timers-and-nexttick"> 이벤트 루프에 대한 설명 </a>
