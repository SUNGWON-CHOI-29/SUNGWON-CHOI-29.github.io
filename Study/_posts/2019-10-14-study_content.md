---
layout: post
title: Node.js Study (8)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (8)

## npm dependencies and devDependencies
패키지 의존성이 언제 dependencies/devDependencies로 나뉠까요? <b>npm install <package-name></b>으로 설치한다면 dependencies로 설치를 한 것입니다.

패키지는 자동적으로 package.json 파일의 dependencies 리스트에 나열될 것입니다.(npm5에서는 수동으로 --save를 지정해야 합니다.)

여러분이 -D, --save-dev 플래그를 추가하면 개발 위존성에 설치하는 것으로 devDependencies 리스트에 추가됩니다. Development dependencies는 개발 전영 패키지로 production에는 필요없습니다. 예를들어 테스팅 패키지, 웹팩, 바벨 같은 것이죠.

여러분이 prodcution 단계에서 npm install을 입력하고 폴더가 package.json 파일을 가지고 있으면 npm은 이것이 개발 배포인 것으로 간주하고 그것들은 설치됩니다.

--production 플래그를 설정해서 개발 의존성에 설치하는 것을 피할 수 있습니다.

## The npx Node Package Runner
npx는 유용한 기능을 다수 제공하며 Node.js 코드를 멋지게 실행하는 방법입니다. 이 영역에서 저는 npm 5.2부터 사용가능한 npx라는 강력한 명령어에 대해 알려드리고 싶습니다. npm을 설치하고 싶지 않다면 독립적인 패키지로 npx를 설치할 수 있습니다. npx는 Node.js로 빌드된 코드를 실행시켜주며 npm 등록소를 통해 배포할 수 있게해줍니다.

### Easily run local commands
Node.js 개발자들은 실행가능한 다수의 명령어를 글로벌 패키지로 배포하여 그들이 즉시 실행할 수 있도록 합니다. 이것은 같은 명령의 여러가지 버전을 설치할 일이 없으므로 매우 일반적이었습니다.

npx commandname을 실행하는 것은 자동적으로 프로젝트의 node_modules 폴더 내에 일치하는 레퍼런스를 찾아서 실행합니다. 정확한 path를 알거나 패키지가 사용자의 경로에 전역으로 설치될 필요가 없습니다.
### Installation-less command execution
npm보다 더욱 나은 장점은 처음 설치하지 않고 명령어를 실행할 수 있게해준다는 것입니다. 이것은 꽤나 유용한데 왜냐면
1. 여러분은 아무것도 설치할 필요가 없고
1. 같은 명령어를 \@version 문법을 사용해서 다른 버전으로 실행할 수 있기 때문입니다.

고전적인 npx 시연은 cowsay 명령어를 사용하는 것입니다. cowsay는 여러분이 작성한 명령어를 소가 말하는 것으로 출력합니다. 다음의 예제를 보시죠
```
_______
< Hello >
 -------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
이제 여러분이 cowsay 명령어를 npm에서 전역으로 설치했다면 위의 결과를 볼것이고 아니면 에러가 나올 것입니다. npx는 npm명령어를 지역적으로 설치하지 않고도 실행할 수 있게 해줍니다.
```
npx cowsay "Hello"
```
다음의 명령어들은 그냥 쓸모없는 재밌는 경우이죠
* vue CLI를 실행하여 응용프로그램을 만들고 실행하는 경우: npx vue create my-vue-app
* create-react-app을 사용하여 새로운 리액트 앱을 만드는 경우: npx create-react-app my-react-app

등등이 있습니다. 한번 다운로드되고 나면 다운로드된 코드들은 지워질 것입니다.

### Run some code using a different Node.js version
\@ 표기를 사용해서 버전을 지정할 수 있고 node와 조합해서 사용할 수 있습니다.
```
npx node@6 -v #v6.14.3
npx node@8 -v #v8.11.3
```
이것은 npm이나 다른 node 버전 관리 도구를 피하는데 도움이 됩니다.
### Run arbitrary code snippets directly from a URL
npx는 npm 등록소에 배포된 패키지만으로 여러분을 제한하지 않습니다. Github gist에 있는 코드를 실행할 수 있습니다.
```
npx https://gist.github.com/zkat/4bc19503fe9e9309e2bfaa2c58074d32
```

물론 여러분이 제어할 수 없는 코드를 실행할 때는 매우 주의해야 합니다. 막강한 힘에는 그만한 책임이 뒤따르니까요.
