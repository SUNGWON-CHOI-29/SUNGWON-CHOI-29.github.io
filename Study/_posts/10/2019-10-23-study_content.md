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

## The Node.js events module
