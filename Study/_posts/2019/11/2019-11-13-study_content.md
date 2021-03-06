---
layout: post
title: Node.js 교과서 학습 정리 (4)
description: >
  Node.js 교과서(조현영) 책을 바탕으로 학습 내용을 정리한 포스팅 입니다.
author: author
comments: true
---

Node.js 교과서 학습 정리 (4)

## 패키지 매니저

npm 서버는 오픈소스 자바스크립트 코드가 공개되어 있습니다. npm을 사용해서 다른 사람이 만들어둔 코드를 사용하거나 자신의 코드를 배포할 수 있습니다.

### npm 알아보기

npm은 Node Package Manager의 약자로 약 60만개의 패키지가 등록되어 있습니다. 이러한 많은 패키지덕에 노드와 자바스크립트의 생태계가 풍부해지고 있습니다.

### package.json으로 패키지 관리하기

같은 패키지라도 버전별로 기능이 다를 수 있으므로 많은 패키지별로 버전 관리가 필요합니다. 이를 수행해주는 것이 package.json 파일입니다. **npm init** 명령어를 사용하여 package.json 파일을 만들 수 있습니다. 버전관리 외에도 scripts 부분을 이용해 npm 명령어를 저장해 둘 수 있습니다. 패키지를 설치하면 node_modules 폴더에 해당 패키지가 설치됩니다. 패키지별 의존성은 dependencies 속성에서 확인할 수 있습니다.

### 패키지 버전 이해하기

노드 패키지들의 버전은 Semantic Versioning으로 항상 세자리로 이루어져 있습니다. 앞부분부터 메이저, 마이너, 패치로 구분합니다.

* 메이저 - 하위호환이 되지 않는 변경사항
* 마이너 - 하위호환이 되는 변경 사항
* 패치 - 간단한 버그 수정

### 기타 npm 명령어

* npm outdated - 업데이트 할 수 있는 패키지가 이쓴지 확인합니다.
* npm update - 해당 명령어를 통해 업데이트 가능한 모든 패키지가 Wanted에 적힌 버전으로 업데이트 됩니다.
* npm publish - 자신이 만든 패키지를 배포할 때 사용합니다.

### 패키지 배포하기

* npm에 배포할 때는 항상 신준해야합니다. 여러분의 민감정보가 코드에 있는지 확인하여 공개된 곳에 비밀키가 들어가지 않도록 주의해주세요.

### 함께보면 좋은 자료

* <a href="https://npmjs.com">npm 공식 웹 사이트</a>
* <a href="https://docs.npmjs.com/cli">npm 명령어 설명서</a>
* <a href="https://npmcompare.com">패키지 간 비교 사이트</a>
* <a href="https://docs.npmjs.com/misc/scope">패키지명에 네임사이트 설정하기</a>
