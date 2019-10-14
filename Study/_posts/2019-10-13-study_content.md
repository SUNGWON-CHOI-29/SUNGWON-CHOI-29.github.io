---
layout: post
title: Node.js Study (7)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (7)

## Find the installed version of an npm package
설치된 npm 패키지들의 최신버전을 보기위해서는 <b>npm list</b>라고 입력하시면 됩니다.
```
❯ npm list
/Users/flavio/dev/node/cowsay
└─┬ cowsay@1.3.1
  ├── get-stdin@5.0.1
  ├─┬ optimist@0.6.1
  │ ├── minimist@0.0.10
  │ └── wordwrap@0.0.3
  ├─┬ string-width@2.1.1
  │ ├── is-fullwidth-code-point@2.0.0
  │ └─┬ strip-ansi@4.0.0
  │   └── ansi-regex@3.0.0
  └── strip-eof@1.0.0
```
그냥 package-lock.json 파일을 열어서 볼 수도 있지만 이건 시각적으로도 보여주죠. <b>npm list -g</b>도 동일한데 전역으로 설치된 패키지를 보여줍니다. top-level의 패키지만 확인하고 싶다면(package.json에 있는 것입니다.) <b>npm list --depth=0</b>을 입력하세요
```
❯ npm list --depth=0
/Users/flavio/dev/node/cowsay
└── cowsay@1.3.1

```
이름을 지정하는 것으로 특정 패키지의 버전을 확인할 수 있습니다.
```
❯ npm list cowsay
/Users/flavio/dev/node/cowsay
└── cowsay@1.3.1
```
이것은 여러분이 설치한 패키지의 의존성에 대해서도 동작합니다.
```
❯ npm list minimist
/Users/flavio/dev/node/cowsay
└─┬ cowsay@1.3.1
  └─┬ optimist@0.6.1
    └── minimist@0.0.10
```
만약 여러분이 npm 저장소에 패키지의 최신버전이 어떤 것인지 확인하고 싶다면 <b>npm view [package_name] version</b>을 통해 확인할 수 있습니다.
```
❯ npm view cowsay version
1.3.1
```

## Install an older version of an npm package
이전 버전의 npm패키지를 설치하는 것이 때로는 호환성 문제를 해결하는 해답이 될 수도 있습니다. '@'문법을 사용해서 이전버전의 패키지를 설치할 수 있습니다.
```
npm install <package>@<version>
```
예를 들어 그냥 <b>npm install cowsay</b>는 1.3.1을 설치하지만 <b>npm install cowsay@1.2.0</b>은 1.2.0버전을 설치하게 됩니다. -g플래그를 통해 전역 패키지에도 동일하게 수행될 수 있습니다. 만약 여러분이 패키지의 이전 버전들을 모두 보고싶다면 <b>npm view <package> versions</b>를 통해 확인할 수 있습니다.
```
❯ npm view cowsay versions
[ '1.0.0',
  '1.0.1',
  '1.0.2',
  '1.0.3',
  '1.1.0',
  '1.1.1',
  '1.1.2',
  '1.1.3',
  '1.1.4',
  '1.1.5',
  '1.1.6',
  '1.1.7',
  '1.1.8',
  '1.1.9',
  '1.2.0',
  '1.2.1',
  '1.3.0',
  '1.3.1' ]
```

## Update all the Node dependencies to their latest version
여러분이 <b>npm install <packagename></b>을 통해 패키지를 설치하면 패키지의 사용가능한 최신머전이 다운로드 되고 node_modules 폴더에 놓여지게 됩니다. 그리고 일치하는 엔트리가 package.json 파일과 package-lock.json 파일에 추가됩니다.

<b>npm sintall cowsay</b>를 실행하면 package.json 파일에 이 엔트리가 추가될 것입니다.
```
{
  "dependencies": {
    "cowsay": "^1.3.1"
  }
}
```
그리고 다음은 package-lock.json 파일에서 추출한 것입니다.
```
{
  "requires": true,
  "lockfileVersion": 1,
  "dependencies": {
    "cowsay": {
      "version": "1.3.1",
      "resolved": "https://registry.npmjs.org/cowsay/-/cowsay-1.3.1.tgz",
      "integrity": "sha512-3PVFe6FePVtPj1HTeLin9v8WyLl+VmM1l1H/5P+BTTDkMAjufp+0F9eLjzRnOHzVAYeIYFF5po5NjRrgefnRMQ==",
      "requires": {
        "get-stdin": "^5.0.1",
        "optimist": "~0.6.1",
        "string-width": "~2.1.1",
        "strip-eof": "^1.0.0"
      }
    }
  }
}
```
이제 위의 두 파일은 우리가 1.3.1 버전의 cowsay가 설치되었다는 것을 알려주고 우리의 업데이트 규칙이 \^1.3.1이기 때문에 패치와 마이너 릴리즈만 업데이트 할 것입니다. 만약 새로운 마이너,패치 릴리즈가 있을 경우 npm update 명령어를 통해 설치된 버전이 업데이트 될 것이고 pacakge-lock.json 파일도 새로운 버전으로 업데이트 될 것입니다.

package.json은 변하지 않은채로 남아있게됩니다. 새롭게 릴리즈된 패키지가 있는지 알아보기 위해서는 npm outdated를 입력하면 됩니다. 다음은 제가 업데이트를 하지 않아서 업데이트 할 것이 남아있는 패키지들의 리스트입니다.
<center>
<img src="https://miro.medium.com/max/1726/1*6Wdzb40QXmTCLYDOekL1Kg.png"/>
</center>
몇몇은 메이저 릴리즈들이기 때문에 npm upddate를 사용해도 업데이트 되지 않을 것입니다. 이 방법으로는 변경사항이 문제를 일으킬 수도 있기 때문에 메이저 릴리즈는 절대 설치되지 않을 것입니다.

메이저 릴리즈를 설치하기 위해서는 npm-check-updates 패키지를 전역으로 설치해야 합니다.
```
npm install -g npm-check-updates
```
실행을 하기 위해서는 <b>ncu -u</b>를 입력하면 됩니다. 이것은 package.json 파일의 모든 버전 hints를 업데이트 하여 dependencies와 devDependencies에 적용하고 그래서 npm이 새로운 메이저 버전을 설치할 수 있게 됩니다. 이제 여러분은 <b>npm update</b>를 통해 업데이트를 할 수 있습니다. 만약 node_modules 의존성없이 프로젝트를 설치했고 여러분이 반짝이는 새로운 버전을 설치하고 싶다면 <b>npm install</b>을 실행하시면 됩니다.
## Semantic Versioning using npm
Semantic Versioning은 version에 손쉽게 의미를 제공하는데 사용됩니다. 만약 Node.js 패키지에 하나의 위대한 것이 있다면 모두가 그들의 버전 넘버링에 Semantic Versioning을 사용하는 것을 꼽을 것입니다. Semantic Versioning의 개념은 꽤나 간단합니다; 모든 버전이 3개의 숫자를 가지고 있습니다: <b>x.y.z</b>
* 첫번째 숫자는 메이저 버전을 말합니다
* 두번째 숫자는 마이너 버전입니다
* 세번째 숫자는 패치 버전입니다.

여러분이 새로운
## Uninstalling npm packages locally or globally

## npm global or local packages
