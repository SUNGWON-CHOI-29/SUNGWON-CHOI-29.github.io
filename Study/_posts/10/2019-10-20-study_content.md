---
layout: post
title: Node.js Study (14)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (14)

## Build an HTTP Server with Node.js
다음은 Hello World Node.js 응용프로그램에 사용되었던 HTTP 웹 서버입니다.
```
const http = require('http')

const port = 3000

const server = http.createServer((req, res) => {
  res.statsCode = 200
  res.setHeader('Content-Type', 'text/plain')
  res.end('Hello World\n')
  })

server.listen(port, () => {
  console.log(\`Server running at http://${hostname}:${port}/\`)
  })
```
간단하게 분석해보자면 http 모듈을 include 했습니다. 해당 모듈로 HTTP 서버를 만들었습니다. 서버는 3000번 포트번호로 리슨을 하며 서버가 준비되면 listen 콜백이 호출될 것입니다.

우리가 전달한 콜백 함수는 매번 요청이 들어올 때마다 실행될 것입니다. 새로운 요청이 들어오면 request 이벤트가 호출되고 두개의 객체를 제공합니다: a request와 a response입니다. request는 request의 자세한 정보를 제공하고 리퀘스트 헤더와 리퀘스트 디테일에 접근할 수 있습니다.

response는 우리가 클라이언트에게 되돌려줄 데이터를 생성하는 데 사용됩니다. 이 경우에서는
```
res.statusCode = 200
```
입니다.

우리는 statusCode 프로퍼티의 값을 200으로 설정해서 성공적인 응답임을 알려주도록 했습니다. Content-Type 헤더 또한 설정했습니다.
```
res.setHeader('Content-Type', 'text/plain')
```
그리고 해당 응답이 종료되면 content를 end()의 매개변수로 추가합니다.
```
res.end('Hello World\n')
```

## Making HTTP requests with Node.js
Node.js에서 GET, POST, PUT, DELETE를 사용하는 HTTP 리퀘스트는 어떻게 동작할까요? HTTP라는 용어를 사용했지만 HTTPS는 어디서나 반드시 사용되어야 합니다. 따라서 HTTP 대신에 HTTPS를 예제에서 사용하겠습니다.

### Peroform a GET Request
```
const https = require('https')
const options = {
  hostname: 'xingxing.com',
  port: 443,
  path: '/todos',
  method: 'GET'
}

const req = https.requests(options, (res) => {
  console.log(\`statusCode: ${res.statusCode}\)

  res.on('data', (d) => {
    process.stdout.write(d)
    })
  })
req.on('error', (error) => {
  console.error(error)
  })
req.end()
```

### Perform a POST Request
```
const https = require('https')

const data = JSON.stringfy({
  todo: 'Buy the milk'
  })

const options = {
  hostname: 'xingxing.com',
  port: 443,
  path: '/todos',
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Content-Length': data.length
  }
}

const req = https.request(options, (res) => {
  console.log(\`statusCode: ${res.statusCode}\`)

  res.on('data', (d) => {
    process.stdout.write(d)
  })
})
req.on('error', (error) => {
  console.error(error)
})

req.write(data)
req.end()
```

### PUT and DELETE
PUT과 DELETE 리퀘스트는 POSTs 리퀘스트와 동일한 포맷을 사용하고 단지 options.method의 값만 바꾸면 됩니다.

## HTTP requests in Node.js using Axios
Axios는 HTTP 리퀘스트를 수행하는데 사용할 수 있는 매우 인기있는 라이브러리입니다. 브라우저와 Node.js 플랫폼 둘다 동작합니다. 모든 최신 브라우저들을 지원하며 IE8과 더 높은 버전도 포함합니다. promise기반이며 XHR 리퀘스트를 수행하는 async/await를 매우 쉽게 작성할 수 있게 해줍니다.

Axios는 네이티브 fetch API를 넘어서는 다른 장점들이 있습니다.
* 오래된 브라우저 지원 (fetch에는 polyfill이 필요합니다)
* 리퀘스트를 중단하는 방법이 있습니다.
* 리스폰스 타임아웃을 설정할 수 있습니다.
* 내장 CSRF 프로텍션이 있습니다
* 업로드 프로그레스를 지원합니다
* 자동화 JSON 데이터 변환을 수행합니다
* Node.js에서 동작합니다.

### Installation
Axios는 npm을 통해 설치할 수 있습니다
```
npm install axios
//or yarn
yarn add axios
//or using unpkg.com
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

### The Axios API
axios 객체로부터 HTTP 리퀘스트를 시작할 수 있습니다.
```
axios({
  url: 'https://dog.ceo/api.breeds/list/all'.
  method: 'get',
  data: {
    foo: 'bar'
  }
})
```
그러나 편의성을 위해서 보통 axios.get()이나 axios.post()를 사용합니다.

Axios는 모든 HTTP 동사 메소드를 제공하며 유명하진 않지만 그래도 사용되고 있습니다.
* axios.delete()
* axios.put()
* axios.patch()
* axios.options()

그리고 HTTP 리퀘스트에서 바디를 제외한 헤더만 가져올려면 다음의 메소드를 사용하면 됩니다.
* axios.head()

### GET requests
편하게 Axios를 사용하는 방법은 최신(ES2017) async/await 문법에 사용하는 것입니다. 이 노드 예제는 axios.get()을 이용하여 Dog API에게 모든 강아지의 품종을 조회하는 질의를 날리고 결과를 카운팅합니다.
```
const axios = require('axios')

const getBreeds = async () => {
  try {
    return await axios.get('https://dog.ceo/api/breeds/list/all')
  } catch (error) {
    console.error(error)
  }
}

const countBreeds = async () => {
  const breeds = await getBreeds()

  if(breeds.data.message) {
    console.log(\`Got ${Object.entries(breeds.data.message).length}breeds\`)
  }
}

countBreeds()
```
async/await를 사용하고 싶지 않다면 프로미스 문법을 사용해도 됩니다.
```
const axios = require('axios')

const getBreeds = () => {
  try {
    return axios.get('https://dog.ceo/api/breeds/list/all')
  } catch (error) {
    console.error(error)
  }
}

const countBreeds = async () => {
  const breeds = getBreeds()
  .then(response => {
    if (response.data.message) {
      console.log(
        \`Got ${Object.entries(response.data.message).length} breeds\`
        )
    }
    })
    .catch(error => {
      console.log(error)
    })
}

countBreeds()
```

### Add parameters to GET requests
GET 응답은 다음과 같이 URL에 매개변수를 가질 수 있습니다. <b>https://site/?foo=bar</b> Axios에서는 다음과 같이 URL을 이용해서 수행할 수 있습니다.
```
axios.get('https://site.com/?foo=bar')
//or 옵션에 params 프로퍼티를 사용할 수 있습니다.
axios.get('https://site.com/', {
  params: {
    foo: 'bar'
  }
})
```

### POST Requests
POST 리퀘스트를 수행하는 것은 GET 리퀘스트와 비슷합니다만 axios.get 대신에 axios.post를 사용해야 합니다.
```
axios.post('https://site.com/')
//POST 매개변수를 가진 객체는 두번째 인자입니다.
axios.post('https://site.com/', {
  foo: 'bar'
})
```
