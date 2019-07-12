---
layout: post
title: Medium - Why use RxSwift
description: >
  <a href="https://medium.com/@leandromperez/why-use-rxswift-a176b553a705">원문 링크 - Leandro Perez</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - RxSwift를 왜 쓰는 것일까

![500x400](https://cdn-images-1.medium.com/max/2600/1*Bu7T6ff5SJbeOuvUZimJCA.jpeg)

누군가 이런 질문을 한 적이 있다.
> 왜 RxSwift를 쓰나요?

> RxSwift는 모든 프로젝트에 좋나요? 아니면 쓰지 않는 것이 좋을 때가 있나요?

첫 번째 질문에 대한 답은 비동기적인 문제를 해결하기 편하기 때문이다.

그리고 비동기성과 RxSwift의 주요 장점을 정리해보고 위의 질문에 대해 답변하겠다.

* 비동기성은 선언형 코드로 단순화 될 수 있다.
* 멀티쓰레딩이 단순화된다
* 보다 깔끔한 코드와 구조
* 다양한 컴포넌트 구성가능
* 멀티플랫폼

### 1. Asynchrony is simplified with Declarative Code.

비동기적 작업흐름은 이해하기는 쉽지만 코딩하기에는 매우 어렵다. 회원가입 Use case의 경우를 예로 들자면 여러 과정이 엮여있는 복잡한 작업흐름이다. 유저의 입력을 검증하고 API 응답을 체크하고 에셋을 로딩하는 것 등등, 상위 레벨 추상화에서는 이런 흐름이 전혀 어렵지 않다. 그러나 실제로 코드를 쓰다보면 알겠지만 전혀 쉽지 않다.

전통적이고 위엄있는 OOP Style의 코드들은 객체를 여러 계층으로 퍼트린다. 중첩된 콜백, 대표자, 알림, 등등 코드는 따라가기 어렵고 전체 그림을 이해하기 어려워 진다.

Rx는 이런 비동기적인 이벤트를 스트림으로 바꿔준다. 이벤트를 집어넣고 잊어버리면 된다.
채널을 구독하고 계속해서 옵저브하면 이벤트가 발생했을 때 값이 자동적으로 바뀌기 때문이다.

아래의 예는 깃허브에 로그인하는 Rxswift의 예제이다.

~~~Swift
let validatedUsername = input.username
    .flatMapLatest { username in
        return validationService.validateUsername(username)
    }

let validatedPassword = input.password
    .map { password in
        return validationService.validatePassword(password)
    }

let usernameAndPassword = Driver.combineLatest(input.username, input.password) { ($0, $1) }
~~~

Reactive 프로그래밍은 코드의 추상화를 높여주며 당신은 비즈니스 로직에 정의된 이벤트에

더욱 집중할 수 있다. RP의 코드는 더욱 간결하다 -
<a href="https://gist.github.com/staltz/868e7e9bc2a7b8c1f754">RP you've been missing 서문<\a>

### 2. Multi-threading is simplified.

멀티쓰레딩을 써야 할 상황들이 있다. 기본적으로 좋은 UX를 위해서 로딩작업들은 모두

백그라운드에서 실행되고 진척도를 메인 쓰레드에서 보여준다. 이것을 구현하기 위해

당신은 쓰레드를 안전하게 써야하고 그러기 위해 Mutex, Patch 큐, 쓰레드 풀 같은

코드가 필요하다.

RxSwift를 쓰면 코드도 짧고 복잡도도 낮으며 버그도 적다. 메인 쓰레드에 리스너를 달아놓고

백그라운드에 반응하면 된다. 아래의 간단한 예를 참고해보라.

~~~Swift
channel
  .observeOn(backgroundScheduler)
  .map { n in
      print("This is performed on the background scheduler")
  }
  .observeOn(MainScheduler.instance)
  .map { n in
      print("This is performed on the main scheduler")
  }
~~~
### 3. Cleaner Code & Architectures.

RP를 쓴다면 간결한 코드를 작성할 수 있다고 꽤나 여러번 말했다.

이벤트에 대해 선언적인 방식으로 처리할 수 있기 때문에 중첩된 콜백 등 복잡한 접근을 피할 수 있다.

게다가 Rx의 스트림은 변경할 수 없기 때문에 확장에는 열려있고 변경에는 닫혀있는 객체를 만들 수 있다.

이러한 데이터 흐름은 깔끔한 구조와 의존도 규칙과 호환된다.

MVVM에서 Rx를 쓴다면 적은 코드, 낮은 컴포넌트 결합, 우려사항 분산 등 보다 좋은 구조를 만들 수가 있다.

### 4. Composable Components.

Rx는 보다 향상되고 체계적인 표준 집합으로 observer 패턴을 쓰는 것이다.

이벤트를 발표하고 그 이벤트를 어떻게 처리하는 방법에 대한 표준이라고 본다.

그것은 정보를 운반하고 수정에 대한 구와 동작을 제공한다.

그렇기 때문에 사용자들이 어떠한 작업을 하더라도 모두 동일한 구조와 동작을 사용할 수 있다는 것이다.

이러한 표준 구조와 동작 때문에 컴포넌트를 다른 컴포넌트와 쉽게 구성할 수 있다.

### 5. Multi-platform.

RP는 작업 방식이고 디자인 패턴이기 때문에 재사용 가능한 컴퓨넌트를 만들 수 있다.

그렇기 때문에 스위프트에서 RP를 배운다면 당신은 그것을 다른 플랫폼과 언어에 적용할 수 있다.

## Summary
* 비동기적인 문제를 쉽고 간편하게 해결할 수 있다
* 어떤 도구나 마찬가지로 적합한 문제에만 이것을 쓰는게 좋다
* 배우는데 두렵겠지만 많은 장점이 있다.
