---
layout: post
title: Node.js Study (3)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (3)
## Where to host a Node.js app
Node.js 응용프로그램은 여러분의 필용에 따라 어디에서나 호스트될 수 있습니다. 아래는 여러분의 앱을 공개적으로 배포할 수 있는 대략적인 리스트 입니다.
### Simplest option ever: local tunnel
동적 IP거나 NAT환경이라도 여러분 컴퓨터의 로컬 터널을 이용해서 앱을 배포하고 요청을 처리할 수 있습니다. 이 옵션은 빠른 테스트나 제품 시연, 작은 그룹의 사람에게 공유할 목적으로 사용하기 적합합니다. 모든 플랫폼에서 동작하는 괜찮은 도구는 <a href="https://ngrok.com/">ngrok</a>입니다.

ngrok을 사용하려면 그냥 ngrok PORT라고 입력하시면 되고 여러분이 원하는 PORT가 인터넷에 노출됩니다. 여러분은 ngrok.io 도메인을 얻게 될 것입니다. 돈을 지불하면 커스텀 URL과 추가적인 보안 옵션을 가질 수 있습니다.(여러분의 컴퓨터가 공공 인터넷에 열려있는 것을 기억하세요.)

사용할 수 있는 다른 서비스로는 <a href="https://github.com/localtunnel/localtunnel">localtunnel</a>이 있습니다.

### Zero configuration deployments
#### Glitch
<a href="https://glitch.com/">Glitch</a>는 가장 빠르게 앱을 빌드할 수 있는 방법이자 놀이터입니다. 여러분의 프로그램을 glitch.com의 하위 도메인에서 볼 수 잇습니다. 현재 커스텀 도메인을 가질 수 없으며 제약사항이 있지만 프로토타입으로는 굉장히 좋습니다. 재밌어 보이고 낮은 환경이 아닙니다 - CDN, 인증서가 필요한 보안 저장소, GitHub 가져오기/내보내기, Node.js의 모든 것을 사용할 수 있습니다. FogBugz와 Trello 기업이 해당 서비스를 제공합니다. 저도 데모 목적으로 많이 씁니다.

#### Codepen
<a href="">Codepen</a>은 놀라운 플랫폼과 커뮤니티 입니다. 여러개의 파일로 프로젝트를 만들 수 있고 커스텀 도메인으로 배포할 수 있습니다.
#### Serverless
관리할 서버가 전혀 없는 방식으로 앱을 배포하는 것은 Serverless입니다. Serverless는 함수들로 여러분의 앱을 배포하는 패러다임이며 네트워크 엔드포인트에 응답을 합니다.(FAAS- Funtion As A Service라고 불립니다.) 매우 유명한 솔루션으로는
* <a href="https://serverless.com/framework/">Serverless Framework</a>
* <a href="https://stdlib.com/">Standard Library</a>
두가지 모두 AWS Lamda에 배포하기 위한 추상 레이어를 제공하며 다른 FAAS 솔루션은 구글 클라우드가 제공하는 Azure에 기반하고 있습니다.
#### PAAS
PAAS는 stands for Platform As A Service 입니다. 이런 플랫폼들은 응용프로그램을 배포할 때 다른 걱정거리를 모두 없애줍니다.
#### Zeit Now
<a href="https://zeit.co/now">Zeit</a>는 흥미로운 옵션입니다. 터미널에 now를 입력하면 여러분의 앱을 배포할 수 있도록 관리해줍니다. 무료버전은 제한이 있고 과금을 하면 더욱 강력해집니다. 여러분은 서버가 있다는 사실조차 잊어버리고 그냥 앱을 배포하면 됩니다.
#### Nanobox
<a href="https://nanobox.io/">Nanobox</a>
#### Heroku
<a href="https://www.heroku.com/">Heroku</a>는 정말 멋진 플랫폼입니다. 다음의 기사를 확인해 보세요<a href="https://devcenter.heroku.com/articles/getting-started-with-node">getting started with Node.js on Heroku</a>

#### Microsoft Azure
<a href="https://azure.microsoft.com/en-us/">Azure</a>는 마이크로소프트 클라우드에서 제공합니다. Azure에서 <a href="https://docs.microsoft.com/en-us/azure/app-service/app-service-web-get-started-node">어떻게 Node.js앱을 만드는지 확인</a>해보세요.
#### Google Cloud Platform
<a href="https://cloud.google.com/">Google Cloud</a>는 여러분의 앱을 위한 멋진 구조입니다. 또한 잘 작성된 <a href="https://cloud.google.com/node/">Node.js 문서화 영역</a>이 있습니다.
#### Virtual Private Server
이 영역에서 여러분들은 사용자 친화적인 것에서 그렇지 않은 순서로 되있다는 것을 유추하셨을 겁니다.
* <a href="https://www.digitalocean.com/">Digital Ocean</a>
* <a href="https://www.linode.com/">Linode</a>
* <a href="https://aws.amazon.com/">Amazone Web Services</a>, 특히 Amazon Elastic Beanstalk를 강조하고 싶습니다. AWS의 복잡도를 추상화로 조금 날려버렸습니다.

AWS는 여러분이 작업할 수 있는 비어있는 리눅스 머신을 제공하지만 이것을 위한 특정 튜토리얼이 없습니다. 이 외에도 VPS 영역의 선택지는 더욱 많지만 딱 제가 써보고 추천하는 것들만 적어놨습니다.

#### Bare metal
또 다른 솔루션은<a href="">bare metal server</a>를 얻어서 리눅스를 설치하고 인터넷에 연결하는 것입니다.(혹은 Vultr Bare Metal 서비스와 같이 한달 주기로 빌릴 수도 있습니다.)
## How to use the Node.js REPL
REPL은 Read-Evaluate-Print-Loop로서 Node.js의 피처를 빠르게 알아볼 수 있는 좋은 방법입니다. node 커맨드는 우리의 Node.js 스크립트를 실행하는 명령어 중 하나입니다.
```
node script.js
```
우리가 파일명을 생략하면 우리는 REPL 모드에 들어갑니다.
```
node
```
만약 여러분이 터미널에서 실행해 본다면 다음과 같은 일이 일어납니다.
```
❯ node
>
```
위의 명령어는 대기 상태로 머무르게 되며 우리가 뭔가를 입력하길 기다립니다. REPL은 우리가 자바스크립트 코드를 입력하길 기다립니다. 간단히 시작해봅시다.
```
> console.log('test')
test
undefined
>
```
첫번째 값인 value는 콘솔에게 우리가 출력하라고 한 것이고 그 다음 undefined는 console.log() 실행의 리턴 값 입니다. 이제부터 새로운 자바스크립트 코드를 입력할 수 있습니다.
### Use the tab to autocomplete
REPL에 대한 멋진 기능 중 하나는 상호작용 한다는 것입니다. 코드를 작성할 때 tab키를 누르면 REPL이 여러분이 이전에 작성한 변수나 사전에 정의된 것으로 자동완성 해줍니다.
### Exploring JavaScript objects
Number와 같이 자바스크립트 클래스 이름을 입력할 때 점을 추가하고 탭을 누르세요. REPL은 해당 클래스에서 접근가능한 모든 프로퍼티와 메소드들을 출력할 것입니다.
<center>
<img src="https://miro.medium.com/max/2188/1*K2DrlIf5O2cto445HS5eVg.png">
</center>

### Explore global objects
global. 이라고 타이핑하고 탭을 눌러서 여러분이 접근할 수 있는 global에 대해 조사할 수 있습니다.
<center>
<img src="https://miro.medium.com/max/2188/1*wr71LKOT7LM4RsVK80knoQ.png">
</center>

### The _ special variable
어떤 코드 뒤에 언더바(\_)를 입력하면 마지막 연산의 결과를 출력할 것입니다.
### Dot commands
REPL은 마침표로 시작하는 특별한 명령들이 있습니다.
* .help: 마침표 명령어의 도움말을 보여줍니다.
* .editor: 에디터 모드를 켜서 쉽게 여러 줄의 자바스크립트 코드를 작성할 수 있게 해줍니다. 한번 이 모드에 들어가면 ctrl+d를 입력해서 작성한 코드를 실행할 수 있습니다.
* .break: 여러 줄의 expression을 입력할 때 .break를 입력하면 이전의 입력을 중단시킬 것입니다. ctrl+c와 동일합니다.
* .clear: REPL 내용을 리셋하여 빈 오브젝트로 만들고 현재 입력되고 있는 멀티라인 expression을 초기화 합니다.
* .load: 현재 작업 디렉토리와 연관되어 있는 곳에서 자바스크립트 파일을 읽어들입니다.
* .save: REPL 연결에 입력된 모든 것을 파일로 저장합니다.(파일이름을 지정합니다.)
* .exit: REPL을 종료합니다(ctrl+c를 두번 누른 것과 동일합니다.)

REPL은 여러분이 .editor를 입력하지 않아도 여러줄의 구문을 입력하는 것을 알고 있습니다. 예를 들어 다음과 같은 반복문을 입력했다고 가정합시다.
```
[1, 2, 3].forEach(num => {
```
그리고 여러분이 엔터를 누르게 되면 REPL은 여러분이 해당 블록에서 계속 작업한다는 것을 알려주기 위해 3개의 마침표로 새로운 라인을 시작하게 될 것입니다.
```
... console.log(num)
... })
```
