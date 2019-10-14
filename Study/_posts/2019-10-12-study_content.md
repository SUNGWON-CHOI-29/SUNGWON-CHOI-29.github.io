---
layout: post
title: Node.js Study (6)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (6)

## The package.json guide
package.json 파일은 Node.js 생태계를 기반으로하는 많은 응용프로그램 코드의 핵심입니다. 자바스크립트로 작업을하셨거나 Node.js 혹은 프론트엔드 프로젝트같은 자바스크립트 프로젝트를 사용해보셨다면 장담컨데 package.json 파일을 보셨을 겁니다.

그것은 뭘 하는걸까요? 왜 그것을 알아야 하고 그것으로 여러분이 어떤 멋진 일을 할 수 있을까요? package.json파일은 프로젝트의 매니페스트 같은 것입니다. 연관되어있지 않은 정말 많은 것을 할 수 있습니다. 해당 파일은 도구를 설정하는 중앙 저장소며 npm/yarn 이 설치할 패키지 이름과 버전을 저장합니다.
### The file structure
다음은 package.json 파일구조입니다.
```
{

}
```
비어있죠! 해당 파일ㅇ에는 고정된 요구사항이 없습니다. 유일한 요구사항은 JSON 포맷을 준수해야합니다. 그렇지 않으면 프로그램이 읽을 수 없어서 프로그래밍적으로 프로퍼티에 접근할 수 없습니다. 여러분이 Node.js 패키지를 만든다면 npm의 급격한 변화에 변함없는 기여를 하고 싶다면 다른 사람들이 사용하는데 도움이 되는 프로퍼티 집합을 가져야 합니다. 이것은 나중에 살펴보겠습니다. 다음은 또다른 package.json 입니다.
```
{
  "name": "test-project"
}
```
위에서는 name프로퍼티를 정의하여 앱이나 패키지의 이름을 구분합니다. 다음은 더욱 복잡한 예제입니다. 이것은 Vue.js 응용프로그램에서 가져온 것입니다.
```
{
  "name": "test-project",
  "version": "1.0.0",
  "description": "A Vue.js project",
  "main": "src/main.js",
  "private": true,
  "scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "test": "npm run unit",
    "lint": "eslint --ext .js,.vue src test/unit",
    "build": "node build/build.js"
  },
  "dependencies": {
    "vue": "^2.5.2"
  },
  "devDependencies": {
    "autoprefixer": "^7.1.2",
    "babel-core": "^6.22.1",
    "babel-eslint": "^8.2.1",
    "babel-helper-vue-jsx-merge-props": "^2.0.3",
    "babel-jest": "^21.0.2",
    "babel-loader": "^7.1.1",
    "babel-plugin-dynamic-import-node": "^1.2.0",
    "babel-plugin-syntax-jsx": "^6.18.0",
    "babel-plugin-transform-es2015-modules-commonjs": "^6.26.0",
    "babel-plugin-transform-runtime": "^6.22.0",
    "babel-plugin-transform-vue-jsx": "^3.5.0",
    "babel-preset-env": "^1.3.2",
    "babel-preset-stage-2": "^6.22.0",
    "chalk": "^2.0.1",
    "copy-webpack-plugin": "^4.0.1",
    "css-loader": "^0.28.0",
    "eslint": "^4.15.0",
    "eslint-config-airbnb-base": "^11.3.0",
    "eslint-friendly-formatter": "^3.0.0",
    "eslint-import-resolver-webpack": "^0.8.3",
    "eslint-loader": "^1.7.1",
    "eslint-plugin-import": "^2.7.0",
    "eslint-plugin-vue": "^4.0.0",
    "extract-text-webpack-plugin": "^3.0.0",
    "file-loader": "^1.1.4",
    "friendly-errors-webpack-plugin": "^1.6.1",
    "html-webpack-plugin": "^2.30.1",
    "jest": "^22.0.4",
    "jest-serializer-vue": "^0.3.0",
    "node-notifier": "^5.1.2",
    "optimize-css-assets-webpack-plugin": "^3.2.0",
    "ora": "^1.2.0",
    "portfinder": "^1.0.13",
    "postcss-import": "^11.0.0",
    "postcss-loader": "^2.0.8",
    "postcss-url": "^7.2.1",
    "rimraf": "^2.6.0",
    "semver": "^5.3.0",
    "shelljs": "^0.7.6",
    "uglifyjs-webpack-plugin": "^1.1.1",
    "url-loader": "^0.5.8",
    "vue-jest": "^1.0.2",
    "vue-loader": "^13.3.0",
    "vue-style-loader": "^3.0.1",
    "vue-template-compiler": "^2.5.2",
    "webpack": "^3.6.0",
    "webpack-bundle-analyzer": "^2.9.0",
    "webpack-dev-server": "^2.9.1",
    "webpack-merge": "^4.1.0"
  },
  "engines": {
    "node": ">= 6.0.0",
    "npm": ">= 3.0.0"
  },
  "browserslist": [
    "> 1%",
    "last 2 versions",
    "not ie <= 8"
  ]
}
```

* name은 응용프로그램/패키지 이름의 집합입니다.
* version은 현재 버전을 나타냅니다
* description은 앱과 패키지의 요약정보 입니다
* main은 응용프로그램의 시작지점입니다
* private가 true일 경우 npm에 배포되는 것을 금지합니다
* scripts는 여러분이 실행할 수 있는 node scripts 를 정의합니다
* dependencies는 의존성으로 설치되는 npm 패키지의 리스트들입니다.
* devDependencies는 개발의존성으로 설치되는 npm 패키지 리스트입니다.
* engines는 앱/패키지가 돌아가는 Node의 버전입니다
* browserlist는 여러분이 지원하고 싶은 브라우저들과 버전들을 나타내는 데 사용합니다.

위의 모든 프로퍼티는 npm이나 다른 도구에서 사용할 수 있습니다.
### Properties breakdown
해당 영역에서는 여러분이 사용할 수 있는 프로퍼티를 자세히 뜯어보겠습니다. 패키지를 언급하겠지만 패키지로 사용하지 않는 로컬 응용프로그램에도 똑같이 적용됩니다. 대부분의 프로퍼티는 npm 웹사이트에서 사용되는 것이고 나머지는 여러분의 코드와 상호작용하는 다른 스크립트들입니다.
#### name
패키지의 이름입니다
```
"name": "test-project"
```
이름은 214캐릭터보다 짧아야하며 공백이 있으면 안됩니다. 소문자만 포함할 수 있으며 하이픈(-)과 언더바(\_)가 사용가능합니다. 이것은 패키지가 npm에 배포될 때 자체 URL을 name프로퍼티를 기반으로 가져오기 때문입니다. 만약 패키지를 깃헙에 배포한다면 깃헙 저장소 이름을 name의 값으로 하면 좋을 것입니다.
#### author
패키지 저자의 이름 리스트입니다.
```
{
  "author": "Flavio Copes <flavio@flaviocopes.com> (https://flaviocopes.com)"
}
```
다음과 같은 형태로도 작성할 수 있습니다.
```
{
  "author": {
    "name": "Flavio Copes",
    "email": "flavio@flaviocopes.com",
    "url": "https://flaviocopes.com"
  }
}
```
#### contributors
작성자와 마찬가지로 프로젝트는 하나 이상의 기여자를 가질 수 있습니다. 이 프로퍼티는 리스트를 가지는 배열입니다.
```
{
  "contributors": [
    "Flavio Copes <flavio@flaviocopes.com> (https://flaviocopes.com)"
  ]
}
```
다음 형태도 가능합니다.
```
{
  "contributors": [
    {
      "name": "Flavio Copes",
      "email": "flavio@flaviocopes.com",
      "url": "https://flaviocopes.com"
    }
  ]
}
```
#### bugs
패키지 이슈 트래커의 링크입니다. 대개 깃허브 이슈페이지입니다.
```
{
  "bugs": "https://github.com/flaviocopes/package/issues"
}
```

#### homepage
패키지 홈페이지를 설정합니다.
```
{
  "homepage": "https://flaviocopes.com/package"
}
```

#### version
패키지의 현재버전을 나타냅니다.
```
"version": "1.0.0"
```
이 프로퍼티는 versioning notation을 문법적으로 준수하며 항상 3개의 숫자로 표현되야 합니다. (x.x.x) 처음 숫자는 주요 버전이며 두번째는 마이너버전, 세번째는 패치버전입니다.

이 버전에는 의미가 있습니다. 버그를 수정한 릴리즈는 패치 릴리즈이며 백워드 호환이 바뀐것을 나타내는 릴리즈는 마이너 릴리즈이고 매이저 릴리즈는 breaking changes를 가질 수 있습니다.
#### license
패키지의 라이센스를 나타냅니다.
```
"license": "MIT"
```

#### keywords
이 프로퍼티는 여러분의 패키지가 하는 일과 연관된 키워드를 가진 배열입니다.
```
"keywords": [
  "email",
  "machine learning",
  "ai"
]
```
이것은 여러분의 패키지를 사람들이 찾는데 도움이 되며 비슷한 패키지를 찾거나 npm 웹사이트에서 탐색할 때 나타납니다.
#### description
이 프로퍼티는 패키지의 짧은 설명을 포함합니다.
```
"description": "A package to work with strings"
```
이것은 특별히 여러분이 npm에 패키지를 배포할 때 유용한데 사람들이 해당 패키지가 뭘하는지 알 수 있기 때문입니다.
#### repository
이 프로퍼티는 패키지저장소의 위치를 나타냅니다.
```
"repository": "github:flaviocopes/testing",
```
github 접두어를 기억하세요, 다음과 같은 서비스도 가능합니다.
```
"repository": "gitlab:flaviocopes/testing",
"repository": "bitbucket:flaviocopes/testing",
```
다음과 같이 버전 컨트롤 시스템도 지정할 수 있습니다.
```
"repository": {
  "type": "git",
  "url": "https://github.com/flaviocopes/testing.git"
}
```
다른 종류의 버전 컨트롤 시스템도 사용할 수 있습니다.
```
"repository": {
  "type": "svn",
  "url": "..."
}
```
#### main
패키지의 시작점을 설정합니다. 응용프로그램에서 패키지를 import하면 해당지점이 module exports를 위해 응용프로그램이 검색을 할 지점입니다.
```
"main": "src/main.js"
```

#### private
true로 설정할 경우 app/package가 npm에 배포되는 것을 막을 수 있습니다.
```
"private": true
```

#### scripts
여러분이 실행할 node scripts를 정의합니다.
```
"scripts": {
  "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
  "start": "npm run dev",
  "unit": "jest --config test/unit/jest.conf.js --coverage",
  "test": "npm run unit",
  "lint": "eslint --ext .js,.vue src test/unit",
  "build": "node build/build.js"
}
```
스크립트들은 응용프로그램의 명렁어 한줄입니다. 해당 스크립트들을 npm run XXXX나 yarn XXXX로 호출해 동작시킬 수 있으며 XXXX는 명령어 이름입니다.
```
npm run dev
```
명령어로 원하는 어떤 이름도 사용할 수 있으며 스크립트는 말 그대로 여러분이 원하는 모든 것을 수행할 것입니다.
#### dependencies
의존성으로 설치될 npm 패키지 리스트입니다. npm이나 yarn으로 다음과 같이 패키지를 설치한다면
```
npm install <packageName>
yarn add <packageName>
```
해당 패키지는 자동적으로 이 리스트에 추가될 것입니다.
```
"dependencies": {
  "vue": "^2.5.2"
}
```

#### devDependencies
개발 의존성으로 설치된 npm 패키지들의 리스트입니다. dependencies와 다른점은 개발환경에서만 설치된다는 것이며 production 코드에서는 필요하지 않습니다.
```
npm install --dev <PACKAGENAME>
yarn add --dev <PACKAGENAME>
```
위의 명령어를 통해 해당 프로퍼티의 리스트에 패키지들이 자동적으로 추가됩니다.
```
"devDependencies": {
  "autoprefixer": "^7.1.2",
  "babel-core": "^6.22.1"
}
```

#### engines
해당 패키지와 앱이 Node.js/명령어를 어떤 버전으로 실행할지 설정합니다.
```
"engines": {
  "node": ">= 6.0.0",
  "npm": ">= 3.0.0",
  "yarn": "^0.13.0"
}
```

#### browserslist
여러분이 지원하고 싶은 브라우저를 구분하는데 사용됩니다. 오직 여러분이 목표로하는 브라우저에만 polyfills와 fallbacks을 추가하기 위해 필요하며 Babel, Autoprefixer이나 다른 도구들에 의해 조회됩니다.
```
"browserslist": [
  "> 1%",
  "last 2 versions",
  "not ie <= 8"
]
```
이 설정의 의미는 최소 1%의 사용을 보이는 모든 브라우저에서 마지막 2개의 주요버전만 지원하겠다는 것입니다. IE8과 그 이하의 버전만 제외하구요.
### Command-specific properties
package.json 파일은 호스트 명령 지정 설정을 할 수 있습니다. 예를들어 Babel, ESlint 등등 말이죠. 각각은 eslintConfig, babel과 같은 특정 프로퍼티가 있습니다. 이런것들은 command-specific으로 어떻게 사용하는지는 command/project 문서에서 확인하실 수 있습니다.
### Package versions
위의 설명에서 버전 숫자가 다음과 같은 걸 보셨을 겁니다:<b>~3.0.0 or ^0.13.0</b>. 이것이 의미하는 것은 무엇이고 여러분이 사용할 수 있는 다른 버전 지정자는 뭐가 있을까요? 해당 심볼은 해당 의존성에서 여러분의 패키지가 어떤 업데이트를 수용할지 지정합니다.

주어진 semver은 3개의 숫자를 사용하며 첫 숫자는 메이저 릴리즈, 두번째는 마이너 릴리즈, 세번째는 패치릴리즈입니다.
* ~: 만약 <b>~0.13.0</b>이라고 사용한다면 여러분은 패치 릴리즈만 업데이트하길 원하는 것입니다. 0.13.1은 되지만 0.14.0은 안되는 거죠
* ^: 이것은 패치와 마이너 릴리즈만 원하는 것입니다. 0.13.1, 0.14.0이 가능한 것이죠
* \*: 이것은 메이저 업데이트를 포함하여 모든 업데이트를 수용하는 것입니다.
* >: 여러분이 지정한 버전보다 높은 것만 수용합니다.
* >=: 여러분이 지정한 버전과 같거나 높은 것을 수용합니다.
* \<=: 여러분이 저장한 버전과 같거나 낮은 것을 수용합니다.
* \<: 여러분이 지정한 버전보다 낮은 것만 수용합니다.

다른 규칙들도 있습니다.
* no symbol: 여러분이 지정한 버전만 수용합니다.
* latest: 최신버전을 사용하길 원하는 것입니다.

그리고 위의 범위를 다음과 같이 조합해서 사용할 수도 있습니다.:<b>1.0.0 || >=1.1.0 <1.2.0</b>이것은 1.0.0을 사용하거나 1.1.0보다 높고 1.2.0보다 낮은 것을 의미합니다.

## The package-lock.json file
package-lock.json 파일은 node 패키지들을 설치하면 자동적으로 생성되는 파일입니다. version5에서 npm은 package-lock.json 파일을 소개했습니다. 아마 package.json 파일은 아시겠지만 package-lock.json은 대체 무엇일까요?

이 파일의 목적은 모든 패키지의 정확한 버전을 추적하여 유지보수 관리자에 의해 패키지가 업데이트되어도 제품을 100% 같은 형태로 설치할 수 있도록 하는 것입니다. 이것은 package.json 파일에 남아있었던 풀지못한 문제들을 해결했습니다. package.json 에서는 semver 표기법을 사용해서 여러분이 업그레이드 하길 원하는 버전을 설정할 수 있었습니다.
* 만약 ~0.13.0 이라고 적으면 패치릴리즈만 업데이트 하길 원하는 것이죠.

여러분은 node_modules 폴더를 커밋하지 않기 때문에 프로젝트를 다른 기계에서 복사할 경우 npm install 명령어를 사용합니다. 만약 <b>0.13.0</b>과 같이 정확한 버전을 명시한다면 문제가 되지 않지만 그렇지 않을 경우 다른사람이 npm install을 사용하면서 프로젝트를 초기화 하게 됩니다.

그러니까 원본 프로젝트와 새롭게 초기화된 프로젝트는 실제적으로 다른 것이죠. 심지어 패치/마니어 릴리즈가 breaking changes를 소개하지 않았더라도 버그가 들어갈 수 있는 것이죠.

package-lock.json은 설치된 각 패키지의 버전들을 고정시킵니다. 그래서 npm install을 실행했을 때 npm은 정확한 버전들을 사용할 것입니다. 이러한 개념은 새로운 것이 아니고 PHP의 Composer와 같이 다른 프로그래밍 언어의 패키지 매니저에서는 이미 사용해 오던 것입니다.

package-lock.json 파일은 여러분의 깃저장소에 커밋되야 할 필요가 있으며 다른사람들에 의해 가져오기 할 수 있어야 합니다. 프로젝트가 공개되어 있거나 공동작업자가 있거나 깃을 배포의 소스로 사용하는 경우에 말이죠.

의존성 버전은 여러분이 npm update를 할 경우에만 package-lock.json에 반영될 것입니다.
### An example
다음은 비어있는 폴더에 npm install cowsay를 실행할 경우 package-lock.json 파일의 구조입니다.
```
{
  "requires": true,
  "lockfileVersion": 1,
  "dependencies": {
    "ansi-regex": {
      "version": "3.0.0",
      "resolved": "https://registry.npmjs.org/ansi-regex/-/ansi-regex-3.
0.0.tgz",
      "integrity": "sha1-7QMXwyIGT3lGbAKWa922Bas32Zg="
    },
    "cowsay": {
      "version": "1.3.1",
      "resolved": "https://registry.npmjs.org/cowsay/-/cowsay-1.3.1.tgz"
,
      "integrity": "sha512-3PVFe6FePVtPj1HTeLin9v8WyLl+VmM1l1H/5P+BTTDkM
Ajufp+0F9eLjzRnOHzVAYeIYFF5po5NjRrgefnRMQ==",
      "requires": {
        "get-stdin": "^5.0.1",
        "optimist": "~0.6.1",
        "string-width": "~2.1.1",
        "strip-eof": "^1.0.0"
      }
    },
    "get-stdin": {
      "version": "5.0.1",
      "resolved": "https://registry.npmjs.org/get-stdin/-/get-stdin-5.0.
1.tgz",
      "integrity": "sha1-Ei4WFZHiH/TFJTAwVpPyDmOTo5g="
    },
    "is-fullwidth-code-point": {
      "version": "2.0.0",
      "resolved": "https://registry.npmjs.org/is-fullwidth-code-point/-/
is-fullwidth-code-point-2.0.0.tgz",
      "integrity": "sha1-o7MKXE8ZkYMWeqq5O+764937ZU8="
    },
    "minimist": {
      "version": "0.0.10",
      "resolved": "https://registry.npmjs.org/minimist/-/minimist-0.0.10
.tgz",
      "integrity": "sha1-3j+YVD2/lggr5IrRoMfNqDYwHc8="
    },
    "optimist": {
      "version": "0.6.1",
      "resolved": "https://registry.npmjs.org/optimist/-/optimist-0.6.1.tgz",
      "integrity": "sha1-2j6nRob6IaGaERwybpDrFaAZZoY=",
      "requires": {
        "minimist": "~0.0.1",
        "wordwrap": "~0.0.2"
      }
    },
    "string-width": {
      "version": "2.1.1",
      "resolved": "https://registry.npmjs.org/string-width/-/string-width-2.1.1.tgz",
      "integrity": "sha512-nOqH59deCq9SRHlxq1Aw85Jnt4w6KvLKqWVik6oA9ZklXLNIOlqg4F2yrT1MVaTjAqvVwdfeZ7w7aCvJD7ugkw==",
      "requires": {
        "is-fullwidth-code-point": "^2.0.0",
        "strip-ansi": "^4.0.0"
      }
    },
    "strip-ansi": {
      "version": "4.0.0",
      "resolved": "https://registry.npmjs.org/strip-ansi/-/strip-ansi-4.0.0.tgz",
      "integrity": "sha1-qEeQIusaw2iocTibY1JixQXuNo8=",
      "requires": {
        "ansi-regex": "^3.0.0"
      }
    },
    "strip-eof": {
      "version": "1.0.0",
      "resolved": "https://registry.npmjs.org/strip-eof/-/strip-eof-1.0.0.tgz",
      "integrity": "sha1-u0P/VZim6wXYm1n80SnJgzE2Br8="
    },
    "wordwrap": {
      "version": "0.0.3",
      "resolved": "https://registry.npmjs.org/wordwrap/-/wordwrap-0.0.3.tgz",
      "integrity": "sha1-o9XabNXAvAAI03I0u68b7WMFkQc="
    }
  }
}
```
우리가 설치한 cowsay는 다음과 같은 의존성을 가집니다.
* get-stdin
* optimist
* string-width
* strip-eof

결국 위의 패키지들은 다른 패키지를 요구하게되고 requires 프로퍼티에 다음과 같은 것을 볼 수 있습니다.
* ansi-regex
* is-fullwidth-code-point
* minimist
* wordwrap
* strip-eof

파일에 알파벳순으로 추가가 되며 각각에는 version 필드가 있고 resolved필드가 있어서 패키지의 위치를 지정합니다. 그리고 integrity 문자열은 우리가 패키지를 검증하는 데 사용됩니다.
