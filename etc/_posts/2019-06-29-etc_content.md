---
layout: post
title: Medium - Functional Programming
description: >
  <a href="https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53">원문 링크 - Charles Scalfani</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - 객체지향 언어의 도태

![500x400](https://cdn-images-1.medium.com/max/800/1*cBFSQ9Ytv_D0jwGtpuL5WA.png)


객체지향 언어는 상속과 캡슐화, 다향성을 특징으로 가지며 추상화를 통한 재사용성에 있어서

프로그래밍에 있어 큰 가치가 있었다.

그러나 The Diamond Problem, Banana Monkey Problem 등, 객체지향 언어에도 문제점은 있고

보다 진보된 함수형 언어를 사용해야 하는 필요성에 대해 간단히 정리한다.


## Inheritance, the First Pillar to Fall
![800x400](https://cdn-images-1.medium.com/max/800/1*T2x8IApyIXIs4nNexGryEw.png)

> 상속의 문제점 - 계층 구조의 단점

객체지향 언어의 문제점은 그들이 내재된 모든 환경을 함꼐 가져오는 것입니다.

당신이 바나나를 원했지만 당신 손에 쥐어진 것은 바나나를 든 고릴라와 정글 전체입니다.

- Joe Armstrong, The creator of Erlang

Categorical Hierarchy는 제대로 동작하지 않는다.

계층구조는 Containment를 위한 것이다.

## Encapsulation, the Second Pillar to Fall
![800x400](https://cdn-images-1.medium.com/max/800/1*ta9gcTzwC_RxZxvD7EhlAw.png)

> 캡슐화의 문제점

캡슐화는 둘째가라면 서러울 객체지향 언어의 분명한 장점이었다.

그러나 Reference Problem을 통해 문제가 드러나기 시작했다.

효율성을 위해 객체는 함수에게 값을 전달해 주는 것이 아닌 참조를 이용한다.

정확히 말하면 함수가 객체를 받는 것이 아닌 객체의 주소나 참조를 전달받는 다는 것이다.



## Polymorphism, the Third Pillar to Fall
![800x400](https://cdn-images-1.medium.com/max/800/1*PgDq0T-0PpSd-huvTaZxkw.png)

> 객체지향 기반 다형성의 불필요함

Interface를 사용하면 객체지향 언어를 사용하지 않고도 훨씬 자유로운 다형성을 사용할 수 있다.

## Summary

* 객체지향 언어는 많은 장점을 보장했지만 이제는 낙후되었다.
* 상속보다는 Contain과 Delegate를 사용하자
* 모든 객체지향 언어는 캡슐화 부분에서 Reference Problem이 있다.
* 객체지향의 다형성 보다는 인터페이스를 통한 다형성을 쓰자.
