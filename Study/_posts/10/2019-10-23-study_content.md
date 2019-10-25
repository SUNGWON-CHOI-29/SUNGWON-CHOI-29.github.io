---
layout: post
title: Node.js Study (17)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (17)

## The Node.js fs module
fs모듈은 파일시스템에 접근하고 상호작용 할 수 있는 유용한 기능들을 많이 제공합니다. 그것은 Node.js의 코어이기 때문에 설치할 필요가 없고 간단히 require을 통해 사용할 수 있습니다.
```
const fs = require('fs')
```
한번 그렇게 하면 fs모듈의 모든 메소드들에 접근할 수 있습니다.
* fs.access() : 파일이 존재하는지 Node가 접근할 수 있는 권한이 있는지 확인합니다.
* fs.appendFile(): 파일에 데이터를 추가합니다. 파일이 없다면 생성합니다.
* fs.chmod(): 파일 이름을 넘겨주어 해당 파일의 권한을 변경합니다. 비슷한걸로 fs.lchmod(), fs.fchmode()가 있습니다.
* fs.chown(): 파일 이름을 넘겨주어 파일의 그룹과 소유자를 변경합니다. 연관된걸로 fs.fchown(), fs.lchown()이 있습니다.
* fs.close(): 파일 디스크립터를 닫습니다.
* fs.copyFile(): 파일을 복사합니다.
* fs.createReadStream(): 읽을 수 있는 파일 스트림을 만듭니다.
* fs.createWriteStream(): 쓰기작업을 할 수 있는 파일 스트림을 만듭니다.
* fs.link(): 파일에 새로운 하드링크를 만듭니다.
* fs.mkdir(): 새로운 폴더를 만듭니다.
* fs.mkdtemp(): 임시 디렉토리를 만듭니다.
* fs.open(): 파일 모드를 설정합니다.
* fs.readdir(): 디렉토리의 내용을 읽어옵니다.
* fs.readFile(): 파일의 내용을 읽어옵니다. 비슷한 걸로 fs.read가 있습니다.
* fs.readLink(): 파일의 상대 경로를 이용해 절대 경로를 계산합니다.
* fs.rename(): 파일이나 폴더의 이름을 변경합니다.
* fs.rmdir(): 폴더를 제거합니다.
* fs.stat(): 파일 이름을 넘겨받아 파일을 식별할 수 있는 정보를 리턴합니다. 비슷한걸로 fs.fstat(), fs.lstat()이 있습니다.
* fs.symlink(): 파일에 새로운 심볼릭링크를 만듭니다.
* fs.truncate(): 파일 이름을 넘겨받아 지정된 길이로 파일 식별자를 자릅니다. 비슷한걸로 fs.ftruncate()가 있습니다.
* fs.unlink(): 파일이나 심볼릭링크를 제거합니다.
* fs.unwatchFile(): 파일의 변화를 모니터링하지 않습니다.
* fs.utimes(): 파일 이름을 넘겨받아 파일 식별자의 타임스탬프를 변경합니다. 비슷한걸로 fs.futimes()가 있습니다.
* fs.watchFile(): 파일의 변경을 모니터링하기 시작합니다. 비슷한걸로 fs.watch()가 있습니다.
* fs.writeFile(): 파일에 데이터를 씁니다. 연관된 걸로 fs.write()가 있습니다.

fs모듈의 특이한 점은 모든 메소드가 기본적으로 비동기화라는 것이며 뒤에 Sync를 붙이면 동기화되이 동작합니다. 이것들은 여러분의 응용프로그램 플로우에서 큰 차이점을 만들어 냅니다. fs.rename() 메소드를 가지고 시험해 봅시다.
```
const fs = require('fs')

fs.rename('before.json', 'after.json', (err) => {
  if (err) {
    return console.error(err)
  }

  //done
  })
```
동기화 API는 에러 처리를 하는 try/catch 블록과 함께 다음처럼 쓰일 수 있습니다.
```
const fs = require('fs')

try {
  fs.renameSync('before.json', 'after.json')
  //done
} catch (err) {
  console.error(err)
}
```
가장 큰 차이점은 두번째 예제에서는 여러분의 코드가 파일 동작이 성공할 때까지 멈춘다는 것입니다.

## The Node.js path module
path 모듈은 파일시스템에 접근하고 상호작용하는데 유용한 많은 기능을 제공합니다. 설치할 필요가 없고 node.js의 코어라서 바로 require를 사용하면 됩니다.
```
const path = require('path')
```
이 모듈은 경로 세그먼트 분할자라는 path.sep를 제공합니다.(윈도우에서는 \\, 리눅스나 맥에서는 /입니다), 그리고 경로구분자인 path.delimiter를 제공합니다. (윈도우에서는 ;, 리눅스, 맥에서는 :)

다음은 path의 메소드 들입니다.

### path.basename()
경로의 마지막 부분을 리턴합니다. 두번째 매개변수는 파일 확장자를 필터링 하는데 사용할 수 있습니다.
```
require('path').basename('/test/something') //something
require('path').basename('/test/something.txt') //something.txt
require('path').basename('/test/something.txt', '.txt') //something
```

### path.dirname()
경로의 디렉토리 부분을 리턴합니다.
```
require('path').dirname('/test/something') // /test
require('path').dirname('/test/something/file.txt') // /test/something
```

### path.extname()
경로의 확장자 부분을 리턴합니다.
```
require('path').dirname('/test/something') // ''
require('path').dirname('/test/something/file.txt') // '.txt'
```

### path.isAbsolute()
절대 경로라면 true를 리턴합니다.
```
require('path').isAbsolute('/test/something') // true
require('path').isAbsolute('./test/something') // false
```

### path.join()
두개 이상의 경로의 부분을 합칩니다.
```
const name = 'flavio'
require('path').join('/', 'users', name, 'notes.txt') //'/users/flavio/notes.txt'
```

### path.normalize()
경로에 상대경로가 있는 경우 실제 경로로 계산합니다.
```
require('path').normalize('/users/flavio/..//test.txt') ///users/test.txt
```

### path.parse()
경로를 구성하는 요소로 분리하여 객체로 만듭니다.

* root: 루트
* dir: 루트로부터 시작하는 폴더 경로
* base: 파일이름 + 확장자
* name: 파일이름
* ext: 파일 확장자

```
require('path').parse('/users/test.txt')

//result
//{
//  root: '/',
//  dir: '/users',
//  base: 'test.txt',
//  ext: '.txt',
//  name: 'test'
//}
```

### path.relative()
두개의 경로를 매개변수로 받습니다. 현재 작업 디렉토리를 기준으로 해서 첫번째 경로에서 두번째 경로로가는 상대경로를 리턴합니다
```
require('path').relative('/Users/flavio', '/Users/flavio/test.txt') //'test.txt'
require('path').relative('/Users/flavio', '/Users/flavio/something/test.txt') //'something/test.txt'
```

### path.resolve()
상대경로를 넘겨주면 절대경로를 리턴합니다.
```
path.resolve('flavio.txt')
//'/Users/flavio/flavio.txt' if run from my home folder
```
두번째 매개변수를 지정하면 첫번째 매개변수를 두번째 매개변수의 base로 사용합니다,
```
path.resolve('tmp', 'flavio.txt')
//'/Users/flavio/tmp/flavio.txt' if run from my home folder
```
첫번째 매개변수가 /로 시작하면 절대경로를 의미합니다.
```
path.resolve('/etc', 'flavio.txt')
//'/etc/flavio.txt'
```

## The Node.js os module
이 모듈은 여러분이 OS, 프로그램이 돌고 있는 컴퓨터에 대한 정보를 가져오고 상호작용 할 수 있는 많은 함수를 제공합니다.
```
const os = require('os')
```
파일 처리와 관련된 중요한 것들을 우리에게 알려주는 유용한 프로퍼티들이 있습니다. <b>os.EOL</b>은 개행자를 전달합니다. 리눅스나 맥에서는 \\n이고 윈도우즈에서는 \\r\\n입니다. 제가 리눅스나 맥이라고 말할 때는 POSIX 플랫폼이라는 것입니다. 단순하게 하기위해 노드가 돌아갈 수 있는 덜 유명한 운영체제는 제외했습니다.

os.constants.signals는 프로세스 시그널을 처리할 수 있는 상수를 알려줍니다. SIGHUP, SIGKILL 같은 것들 말이죠.

os.constants.errno는 에러 러포팅에 설정되는 상수들입니다. EADDRINUSE, EOVERFLOW 등이 있습니다. 다음은 os가 제공하는 주요 메소드 들입니다.

* os.arch() - arm, x64와 같은 구조에 대한 식별자를 문자열 형태로 리턴합니다.
* os.cpus() - 시스템에 CPU 사용 정보를 리턴합니다
* os.endianness() - Node.js가 Big Edian / Little Edian 중 어느 것으로 컴파일 되었는지 BE/LE로 리턴합니다.
* os.freemem() - 시스템에 사용가능한 메모리를 바이트단위로 리턴합니다.
* os.homedir() - 현재 사용자의 홈 디렉토리 경로를 리턴합니다.
* os.hostname() - 호스트이름을 리턴합니다.
* os.loadavg() - 운영체제의 load average를 계산해서 리턴합니다. 이 값은 리눅스와 맥에서만 의미있는 값을 리턴합니다.
* os.networkInterfaces() - 시스템에 사용가능한 네트워크 인터페이스들의 자세한 정보를 리턴합니다.
* os.platform() - Node.js가 컴파일된 플랫폼을 리턴합니다.
* os.release() - 운영체제의 릴리즈 넘버 식별자를 문자열 형태로 리턴합니다.
* os.tmpdir() - temp 폴더에 할당된 경로를 리턴합니다.
* os.totalmem() - 시스템에 사용가능한 전체 메모리를 바이트 형태로 리턴합니다
* os.type() - 운영체제의 식별자를 리턴합니다 (Linux, Darwin, Windows_NT 등)
* os.uptime() - 컴퓨터가 부팅된 이후로 흘러간 시간을 초단위로 리턴합니다.

## The Node.js events module
events 모듈은 Node.js에서 이벤트로 작업할 때 핵심이 되는 EventEmitter 클래스를 제공합니다. 다음과 같이 EventEmitter를 사용할 수 있습니다.
```
const EventEmitter = require('events')
const door = new EventEmitter()
```
이벤트 리스너는 스스로 이벤트를 삼켜서 아래의 이런 이벤트들을 실행합니다.
* newListener - 리스너가 추가되었을 떄
* removeListener - 리스너가 제거되었을 때

다음은 가장 유용한 메소드들의 자세한 내용입니다.
* emitter.addListener() - emitter.on()의 별칭입니다.
* emitter.emit() - 이벤트를 뱉어냅니다. 모든 이벤트 리스너들을 등록된 순서대로 동기화되게 호출합니다.
* emitter.eventNames() - 현재 이벤트 리스너에 등록된 이벤트들을 문자열 형태로 배열에 담아 리턴합니다.
* emitter.getMaxListeners() - 하나의 이벤트리스너 객체에 최대로 추가할 수 있는 리스너의 수를 가져옵니다. 기본으로 10으로 설정되어 있지만 setMaxListeners()를 이용해서 늘리거나 줄일 수 있습니다.
* emitter.listenerCount() - 매개변수로 넘겨준 이벤트의 리스너 수를 가져옵니다
* emitter.listeners() - 매개변수로 넘겨진 이벤트의 리스너들을 배열로 가져옵니다.
* emitter.off() - Node10에서 추가된 emitter.removeListener()의 별칭입니다.
* emitter.once() - 이벤트가 등록된 이후 처음으로 뱉어질 때 호출되는 콜백을 추가합니다. 한번 이 콜백이 호출되면 절대 다시 호출되지 않습니다.
* emitter.prependListener() - on/addListener을 사용해서 리스너를 추가하면 리스너의 큐에 마지막으로 들어가고 마지막으로 호출됩니다. prependListener를 사용해서 추가하면 다른 리스너들보다 먼저 호출됩니다.
* emitter.prependOnceListener() - once를 사용해서 리스너를 추가하면 리스너 큐에 마지막에 추가되고 마지막에 호출됩니다. prependOnceListener로 추가하면 다른리스너들 보다 먼저 추가되고 호출됩니다.
* emitter.removeAllListeners() - 특정 이벤트를 대기하고 있는 EventEmitter의 모든 리스너를 삭제합니다.
* emitter.removeListener() - 특정 리스너를 삭제합니다. 추가할 때 변수에 콜백함 수를 저장해서 나중에 조회할 수 있습니다.
* emitter.setMaxListeners() - 이벤트 리스너 객체에 추가할 수 있는 리스너의 최대 수를 설정합니다. 10이 기본이지만 늘리거나 줄일 수 있습니다.
