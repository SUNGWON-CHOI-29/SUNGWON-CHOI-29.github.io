---
layout: post
title: Node.js Study (16)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (16)

## Node.js file stats
모든 파일은 Node.js를 사용해서 조사할 수 있는 정보들이 있습니다. fs 모듈이 제공하는 stat()메소드를 사용할 수 있습니다. 파일 경로를 넘겨서 호출할 수 있으며 Node.js가 한번 파일의 디테일을 받으면 콜백함수는 2개의 매개변수를 전달해 줄겁니다. 에러메시지와 파일 정보들 입니다
```
const fs = require('fs')
fs.stat('/Users/flavio/test.txt', (err, stats) => {
  if (err) {
    console.error(err)
    return
  }
  //이제부터 stats에 있는 파일 정보에 접근할 수 있습니다.
  })
```
Node.js는 동기 메소드를 지원하므로 파일 정보가 준비될 때까지 스레드를 멈추가 됩니다.
```
const fs = require('fs')
try {
  const stats = fs.stat('/Users/flavio/test.txt')
} catch (err) {
  console.error(err)
}
```
파일 정보는 파일 stats 변수에 포함되어 있습니다. 어떤 정보들이 stata에서 추출될 수 있을까요? 아주 많이 있지만 그 중에 일부를 소개해 드리겠습니다.
* 파일이 디렉토리거나 파일일 때 stats.isFile(), stats.isDirectory()를 사용하세요
* 파일이 심볼릭 링크라면 stats.isSymbolicLick()를 사용하세요
* 파일 사이즈는 stats.size에 바이트 단위로 있습니다.

더욱 많은 고급 메소드가 있지만 여러분이 날마다 프로그래밍을 하면서 사용하게 되는 것들은 이런 것입니다.
```
const fs = require('fs')
fs.stat('/Users/flavio/test.txt', (err, stats) => {
  if (err) {
    console.error(err)
    return
  }

  stats.isFile() //true
  stats.isDirectory() //false
  stats.isSymbolicLick() //false
  stats.size //1024000 //= 1MB
  })
```

## Node.js File Paths
시스템의 모든 파일은 경로가 잇습니다. 리눅스와 맥에서는 경로가 다음과 같을 것입니다.
<center>
```
/users/flavio/file.txt
```
</center>
윈도우 컴퓨터들은 좀 다른데 다음과 같은 구조를 가지고 있습니다.
<center>
```
C:\users\flavio\file.txt
```
</center>
여러분은 응용프로그램에서 경로를 사용할 때 이런 차이점이 계정에 반드시 포함되어 있도록 주의를 기울여야 합니다. 파일을 사용할 때 이 모듈을 포함시키세요
<center>
const path = require('path')
</center>
그러면 경로의 메소드를 사용할 수 있습니다.

### Getting information out of a path
주어진 경로에서 다음의 메소드를 사용해서 정보를 추출할 수 있습니다.
* dirname: 파일의 부모 폴더를 가져옴
* basename: 파일이름의 부분을 가져옴
* extname: 파일의 확장자를 가져옴

```
const notes = '/users/flavio/notes.txt'

path.dirname(notes) // /users/flavio
path.basename(notes)// notes.txt
path.extname(notes) // .txt
```
basename에 두번째 매개변수를 지정해서 확장자 없이 파일의 이름만 가져올 수 있습니다.
```
path.basename(notes, path.extname(notes)) //notes
```

### Working with paths
path.join()을 사용해서 두 개 이상의 경로를 합칠 수 있습니다.
```
const name = 'flavio'
path.join('/', 'users', name, 'notes.txt')
// '/users/flavio/notes.txt'
```
path.resolve()를 사용해서 절대경로를 얻어낼 수 있습니다.
```
path.resolve('flavio.txt')
// '/Users/flavio/flavio.txt'
```
이 경우 Node.js는 간단히 /flavio.txt를 현재 작업 폴더에 추가할 것입니다. 두번째 매개변수를 지정하면 resolve는 첫번째 피연산자를 두번째 피연산자의 base로 간주합니다.
```
path.resolve('tmp', flavio.txt)
// '/Users/flavio/tmp/flavio.txt'
```
첫번째 피연사자가 /로 시작하면 절대경로란 말입니다.
```
path.resolve('/etc', 'flavio.txt')
// '/etc/flavio.txt'
```
path.nomalize()는 또 다른 유용한 함수로 "," , ", 같은 상대지정자의 실제 주소를 계산해줍니다. 그러나 resolve와 path가 있는지 없는지 검사를 하제 않습니다.

## Reading files with Node.js
Node.js에서 파일을 읽는 가장 간단한 방법은 fs.readFile() 메소드를 사용하는 것입니다. 경로와 파일 데이터 및 에러를 받으면 동작할 콜백을 전달하면 됩니다.
```
const fs = require('fs')

fs.readFile('/Users/flavio/test.txt', (err, data) => {
  if (err) {
    console.error(err)
    return
  }
  console.log(data)
  })
```
동기화 버전인 fs.readFileSync()를 대신사용 할 수도 있습니다.
```
const fs = require('fs')

try {
  const data = fs.readFileSync('/Users/flavio/test.txt')
  console.log(data)
} catch (err) {
  console.error(err)
}
```
기본적으로 utf8로 인코딩되지만 두번째 매개변수로 다른 인코딩 방식을 지정할 수 있습니다. fs.readFile()이나 fs.readFileSync() 두 메소드 모두 데이터를 리턴하기 전에 메모리에서 파일 전체를 읽습니다. 이말은 큰 파일은 여러분의 메모리 소비와 프로그램 실행 속도에 중요한 영향을 미치게 될 것이라는 것입니다. 이 경우에는 스트림을 사용해서 파일 내용을 읽는 것이 더 나은 선택일 수도 있습니다.

## Writing files with Node.js
Node.js에서 파일에 쓰는 가장 쉬운 방법은 fs.writeFile() API 입니다.
```
const fs = require('fs')

const content = 'Some content!'

fs.writeFile('/Users/flavio/test.txt', content, (err) => {
  if (err) {
    console.error(err)
    return
  }
  //성공적으로 파일쓰기 완료
  })
```
대안으로 동기화 버전인 fs.writeFileSync()를 사용할 수 있습니다.
```
const fs = require('fs')

const content = 'Some content!'

try {
  const data = fs.writeFileSync('/Users/flavio/test.txt', content)
  //성공적으로 파일 쓰기 완료
} catch (err) {
  console.error(err)
}
```
기본적으로 이 API는 기존에 존재하는 파일의 내용을 대체합니다. 다음과 같이 플래그를 지정해서 기본설정을 변경할 수 있습니다.
```
fs.writeFile('/Users/flavio/test.txt', content, { flag: 'a+'},
(err) => {})
```

### Append to file
fs.appendFile()은 손쉽게 파일의 끝에 내용을 붙일 수 있게 해줍니다.
```
const content = 'Some content!'

fs.appendFile('file.log', content, (err) => {
  if (err) {
    console.error(err)
    return
  }
  // done!
  })
```
### Using streams
모든 쓰기 메소드들은 제어를 프로그램에 반납하기 전에 모든 내용을 파일에 씁니다. 비동기 버전에서 이말은 콜백을 실행하는 것이죠. 이 경우 파일의 내용을 스트림을 이용해서 쓰는 것이 좋은 선택입니다.

## Working with folders in Node.js
Node.js의 fs 코어모듈은 여러분이 폴더와 작업할 때 쓸 수있는 간편한 메소드를 많이 제공합니다.

### Check if a folder exists
fs.access()를 사용해서 Node.js가 접근할 권한이 있는지 해당 폴더가 존재하는 지 체크할 수 있습니다.

### Create a new folder
fs.mkdir(), fs.mkdirSync()로 새로운 폴더를 만들 수 있습니다.
```
const fs = require('fs')

const folderName = '/Users/flavio/test'

try {
  if (!fs.existsSync(dir)){
    fs.mkdirSync(dir)
  }
} catch (err) {
  console.error(err)
}
```

### Read the content of a directory
fs.readdir(), fs.readdirSync()를 사용해서 디렉토리의 내용을 읽을 수 있습니다. 아래의 코드는 파일과 하위폴더들과 같은 폴더의 내용을 읽고 그들의 상대 경로를 리턴합니다.
```
const fs = require('fs')
const path = require('path')

const folderPath = '/Users/flavio'

fs.readdirSync(folderPath)
```
다음과 같이 전체 경로를 얻을 수 있습니다.
```
fs.readdirSync(folderPath).map(fileName => {
  return path.join(folderPath, fileName)
  })
```
폴더들은 제외하고 파일의 결과만 리턴하도록 필터링 할 수 있습니다.
```
const isFile = fileName => {
  return fs.lstatSync(fileName).isFile()
}

fs.readdirSync(folderPath).map(fileName => {
  return path.join(folderPath, fileName).filter(isFile)
  })
```

### Rename a folder
fs.rename(), fs.renameSync()로 폴더의 이름을 바꿀 수 있습니다. 처음 매개변수는 현재의 경로고 두번째는 새로운 경로 입니다.
```
const fs = require('fs')

fs.rename('/Users/flavio', '/Users/roger', (err) => {
  if (err) {
    console.error(err)
    return
  }
  //done
  })
```
fs.renameSync()는 동기화 버전입니다.
```
const fs = require('fs')

try {
  fs.renameSync('/Users/flavio', '/Users/roger')
} catch (err) {
  console.error(err)
}
```

### Remove a folder
fs.rmdir(), fs.rmdirSync()를 이용해서 폴더를 제거할 수 있습니다. 내용물이 있는 폴더도 여러분이 원한다면 지울 수 있습니다. 이 경우에 저는 fs-extra 모듈을 설치하길 추천합니다. 잘 유지보수 되는 유명한 모듈로 fs모듈에 구속받지 않으며 더욱 많은 기능을 제공합니다.

이 경우에는 remove()메소드가 여러분이 원하는 것입니다. 사용할려면 <b>npm install fs-extra</b>를 통해 설치하고 다음과 같이 하면 됩니다.
```
const fs = require('fs-extra')

const folder = '/Users/flavio'

fs.remove(folder, err => {
  console.error(err)
  })
```
아니면 프로미스와 함께 사용할 수 있습니다.
```
fs.remove(folder).then(() => {
  //done
  }).catch(err => {
    console.error(err)
  })
```
아니면 async/await 같은 비동기 함수를 사용해도 됩니다.
```
async function removeFolder(folder) {
  try {
    await fs.remove(folder)
    //done
  } catch (err) {
    console.error(err)
  }
}

const folder = '/Users/flavio'
removeFolder(folder)
```
