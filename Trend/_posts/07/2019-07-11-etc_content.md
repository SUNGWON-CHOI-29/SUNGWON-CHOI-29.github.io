---
layout: post
title: Medium - Some tips on commit etiquette and best practices for junior developers
description: >
  <a href="https://hackernoon.com/git-it-together-some-tips-on-commit-etiquette-and-best-practices-for-junior-developers-1f147b8dfd56">원문 링크 - Jeremy Gunter</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - 신입을 위한 커밋 에티켓과 예제

![500x400](https://cdn-images-1.medium.com/max/2600/1*EU87xmcyUSWc2jEJNJ47Lg.jpeg)

제가 소프트웨어 엔지니어로 진로를 걷는 첫날에 깃-에티켓의 기본적인 것을 교육받은 것은 매우 행운이라고 생각합니다.

겉보기에는 개발자가 되는데 그리 중요하지 않은 개념처럼 생각되었습니다만 개발자로 나아가는데 매우 중요한 교육이었습니다.

놀랍게도 Git이나 문서에 익숙하지 않은 많은 개발자들이 있는 것으로 보입니다.

많은 프로그래머들이 Git을 직장생활을 통해 배우게 되며 좋은 예제를 통해 교육받지 못하고 그저 가벼운 기술이라는 생각으로 열악한 깃-에티켓을 사용하는 것 같습니다. 그럼에도 불구하고 개발자의 모든 기술역량과 관련있습니다.

그래도 걱정하지마세요, 해결책은 많은 시간을 필요로 하거나 당신의 작업방식을 바꾸는 것이 아닙니다. 사실 문제를 해결하는 법은 꽤 쉽습니다. 단지 이 가이드라인을 잘 준수하기만 하세요

그럼 기본적인 몇가지를 시작해봅시다. 이 개념들을 알고 구현하는 것은 깃-꿈나무들에게 깃-전문가가 되는 좋은 첫걸음이 될 것입니다.

## Use the CLI and and editor

git commit -m "Useless message here" 이렇게 쓰지 좀 마세요..

### 커밋 메시지는 시간을 좀 들여서 써야합니다.

당신은 하던 일을 멈추가 다른 사람에게 프로젝트에서 한 일에 대해 설명해야 할 겁니다. 그리고 당신 스스로도 변경점을 찾느라 시간을 허비하겠죠

### 잘 쓰여진 메시지는 당신이 무엇을 바꿨고 왜 그랬는지 잘 설명해주는 역사를 써내려 가는 것입니다.

커맨드라인에서 쓰는 것이 아니라 텍스트 에디터를 사용해서 메시지를 작성한다면 여유를 갖게 될 것이고 당신의 변경사항들에 확신을 주고 가치를 나누는 것이 될 겁니다. 그리고 왜 변경하게 되었는지 좀 더 잘 설명할 수 있게 할 것입니다.

### 에디터를 사용해서 메시지를 구성한다면 에러를 빨리 발견하는데 도움이 됩니다.

예를들어 저는 Oh-My-Zsh 라는 깃 별명을 작업에 사용합니다. <b>gc</b> 라는 명령어는 <b>git commit --verbose </b>의 확장으로 현재 변경사항들을 코멘트 형식으로 요약하여 당신의 기본 에디터를 열어서 띄워줍니다. 커밋메시지를 작성할 때 변경 사항들을 리뷰할 수 있게 해주는 것이죠.

메시지를 쓰기 전에 변경 점들을 읽는 것으로 코드 리뷰하기 전엔 대개 잡히지 않는 스펠링이 오류들을 잡아낼 수 있습니다.

## Follow proper commit message format

### 제목을 짓는 3가지 규칙

1. 제목은 대문자로 시작하고 50자 미만으로 작성하고 끝에 마침표를 찍지 마세요.
1. 명령투의 문장을 사용하세요 - Add new About Us Page or Refactor tests for the order model
1. 완벽한 문장을 이루도록 하세요

![500x800](https://cdn-images-1.medium.com/max/1600/1*byoD0nC4vSCqec_yNSPGWA.png)

### 본문

변경 사항들의 간략한 요약입니다. 만약 변경사항들이 매우 간단해서 제목으로 충분하다면 이 부분은 선택사항입니다. 자세한 추가 설명이 필요없는 것은 매우 좋은 예시 입니다.

본문은 당신이 '무엇'을 변경했고 '왜' 변경했는지가 설명되어야 합니다. '어떻게'는 필요가 없어요. 당신의 코드를 읽는 사람은 당신이 어떻게 구현했는지 읽게 된다면 당혹스러울 겁니다.

<b>Tip</b> - 만약 당신이 ticket 관리 시스템(Trello, Jira, etc) 등을 쓴다면 <b>이슈/카드에 대한 링크를 포함하세요</b> 같은 프로젝트에 일하는 사람이라도 당신이 처리하는 이슈는 잘모르니까 레퍼런스를 달아놓는 것은 코드리뷰하는 사람에게 매우 도움될 것입니다.

![500x400](https://cdn-images-1.medium.com/max/1600/1*TKnySRnLgu8PGgtLDEmcxA.png)

## Be atomic and keep changes together in related commits

![500x400](https://cdn-images-1.medium.com/max/1600/1*pYJKjPbc1y6g79UtB-B2EA.png)

### Group like changes together in the same commit

같은 커밋에 대해서 설정을 바꾸거나 새로운 CSS를 적용하지마세요.

![500x400](https://miro.medium.com/max/908/1*qkYgFRx4ZQUnWGosNFyqBQ.png)

당신의 커밋들은 진척도를 보여줍니다. 따라오기 쉽도록 스토리를 만드세요. 당장은 그게 중요하지 않은 것처럼 보일 지 몰라도 당신의 코드에 역사를 따라갈 수 있도록 하는 것은 당신이 논리적인 추론으로 회고를 할 수 있는데 도움을 줍니다.

![500x400](https://miro.medium.com/max/1400/1*VhwEIaGmQyHMxsnAZy7EaQ.png)

이런 것들은 당신이 깃을 완벽하게 쓰는데에는 의미 없는 것들이지만 빌드하는데 단단한 기반이 되는 것입니다.
당신이 쓰는 툴들에 대한 지식과 어떻게 쓰는 것이 가장 좋은 방법인지 아는 것은 좋은 개발자가 되는 한 면입니다.
이렇게 사소한 것에도 관심을 가지는 것이 더욱 생산성을 높여주고 일 하는 것을 즐겁게 만들어 줄 것입니다.

## Summary
* 깃 커밋을 할 때 여유를 가지고 잘 하자
* 요약회고가 가능하도록, 커밋 메시지들을 보고 히스토리를 유추할 수 있도록 메시지를 쓰자
* 좋은 개발자가 되는 것에는 문서를 잘 작성하는 것도 중요하다.
