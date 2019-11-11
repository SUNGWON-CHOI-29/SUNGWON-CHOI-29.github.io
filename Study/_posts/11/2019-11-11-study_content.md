---
layout: post
title: Node.js 교과서 학습 정리 (3)
description: >
  Node.js 교과서(조현영) 책을 바탕으로 학습 내용을 정리한 포스팅 입니다.
author: author
comments: true
---

Node.js 교과서 학습 정리 (3)

## http 모듈로 웹 서버 만들기

### 요청과 응답 이해하기

* 서버는 클라이언트가 있기에 동작합니다. 클라이언트에서 request를 보내고 서버는 해당 내용을 처리한 뒤 response를 보냅니다.

```js
const http = require('http');

http.createServer( (req, res) => {
  //여기에 어떻게 응답할지 적습니다.
})
```

* 응답을 보내는 부분과 서버 연결 부분을 추가해 봅시다

```js
const http = require('http');

http.createServer( (req, res) => {
  res.write('<h1>Hello Node!</h1>');
  res.end('<p>Hello Server!</p>');
}).listen(8080, () => {
  console.log('8080번 포트에서 서버 대기 중입니다!');
});
```

* listening 이벤트 리스너와 error 이벤트 리스너를 붙여봅시다.

```js
const http = require('http');

const server = http.createServer( (req, res) => {
  res.write('<h1>Hello Node!</h1>');
  res.end('<p>Hello Server!</p>');
});
server.listen(8080); //8080번 포트에서 서버 대기 중

server.on('listening', () => {
  console.log('8080번 포트에서 서버 대기 중입니다!');
});
server.on('error', (error) => {
  console.error(error);
})
```

* res.write 메소드는 클라이언트에게 보낼 데이터 입니다. 여러개를 호출해도 됩니다.
* res.end 메소드는 응답을 종료합니다. 인자가 있다면 해당 데이터를 보냅니다.
* 리눅스와 macOS에서는 1024번 이하의 포트에 연결할 때 관리자 권한이 필요합니다. 이럴 때 명령어 앞에 sudo를 붙여줘야 합니다.

HTML 파일을 만들어두고 해당 파일을 읽어들여서 클라이언트에게 보내봅시다.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8"/>
  <title>Node.js 웹 서버</title>
</head>
<body>
  <h1>Node.js 웹 서버</h1>
  <p>만들 준비되셨나요?</p>
</body>
</html>
```

```js
const http = require('http');
const fs = require('fs');


http.createServer( (req, res) => {
  fs.readFile('./server2.html', (err, data) => {
    if (err) {
      throw err;
    }
    res.end(data);
  });
}).listen(8081, () => {
  console.log('8081번 포트에서 서버 대기 중입니다.');
});
```

### 쿠키와 세션 이해하기

클라이언트에서 보내는 요청이 누구인지 알기 위해서는 로그인을 구현해야 합니다; IP 주소나 브라우저 정보만으로는 클라이언트를 특정할 수 없습니다. 서버가 로그인 정보를 유지하기 위해서는 **쿠키와 세션** 을 사용해야 합니다. 서버가 요청에 대한 응답을 할 때 쿠키라는 것을 같이 보냅니다. 쿠키는 name=PUMP와 같이 단순한 키-값의 쌍입니다. 웹 브라우저는 쿠키를 저장해뒀다가 요청할 때마다 쿠키를 같이 보냅니다. 서버는 쿠키를 읽어서 누군지 파악합니다. **서버에서 브라우저로 쿠키를 보낼 때만 코드를 작성하여 처리** 하면 됩니다.

쿠키는 request의 헤더에 저장됩니다. 쿠키를 만들어 요청자의 브라우저에 넣어봅시다.

```js
const http = require('http');

const parseCookies = (cookie = '') =>
  cookie
    .split(';')
    .map(v => v.split('='))
    .map(([k, ...vs]) => [k, vs.join('=')])
    .reduce((acc, [k, v]) => {
      acc[k.trim()] = decodeURIComponent(v);
      return acc;
    }, {});

http.createServer( (req, res) => {
  const cookies = parseCookies(req.headers.cookie);
  console.log(req.url, cookies);
  res.writeHead(200, { 'Set-Cookie': 'mycookie=test' });
  res.end('Hello Cookie');
})
  .listen(8082, () => {
    console.log('8082번 포트에서 서버 대기 중입니다!');
  });
```

* 브라우저는 HTTP 상태코드를 보고 요청의 성공여부를 판단합니다.
* 2XX: 성공을 알리는 코드입니다. 200(성공), 201(작성됨)이 많이 사용됩니다.
* 3XX: 리다이렉션을 알리는 상태 코드입니다. 301(영구이동), 302(임시이동) 이 있습니다.
* 4XX: 요청 오류를 나타냅니다. 401(권한없음), 403(금지됨), 404(찾을 수 없음)이 있습니다.
* 5XX: 서버 오류를 나타냅니다. 500(내부 서버 오류), 502(불량 게이트웨이), 503(서비스를 사용할 수 없음)이 자주 사용됩니다.

쿠키를 식별하는 방법에 대해 알아봅시다.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8"/>
  <title>쿠키&세션 이해하기</title>
</head>
<body>
    <form action="/login">
      <input id="name" name="name" placeholder="이름을 입력하세요" />
      <button id="login">로그인</button>
    </form>
</body>
</html>
```

```js
const http = require('http')
const fs = require('fs')
const url = require('url')
const qs = require('querystring')

const parseCookies = (cookie = '') =>
  cookie
    .split(';')
    .map(v => v.split('='))
    .map(([k, ...vs]) => [k, vs.join('=')])
    .reduce((acc, [k v]) => {
      acc[k.trim()] = decodeURIComponent(v);
      return acc;
    }, {});

http.createServer( (req, res) => {
  const cookies = parseCookies(req.headers.cookie);
  if (req.url.startWith('/login')) {
    const { query } = url.parse(req.url);
    const { name } = qs.parse(query);
    const expires = new Date();
    expires.setMinutes(expires.getMinutes() + 5);
    res.writeHead(302, {
      Location: '/',
      'Set-Cookie': `name=${encodeURIComponent(name)};
      Expires=${expires.toGMTString()};
      HttpOnly;
      Path=/`,
    });
    res.end();
  } else if (cookies.name) {
    res.writeHead(200, { 'Content-Type': 'text/html; charset=utf-8' });
    res.end(`${cookies.name}님 안녕하세요`);
  } else {
    fs.readFile('./server4,html', (err, data) => {
      if (err) {
        throw err;
      }
      res.end(data);
    });
  }
})
  .listen(8083, () => {
    console.log('8083번 포트에서 서버 대기 중입니다!');
  });
```

* 주소가 /login으로 시작할 때에는 url과 쿼리 문자열 모듈로 주소와 주소에 딸려오는 쿼리를 분석합니다. 쿠키 만료 시간은 5분 뒤 입니다.
* 302 응답코드를 이용하여 리다이렉트 주소와 함께 쿠키를 헤더에 넣습니다. 브라우저는 해당 주소로 리다이렉트 합니다.
* /주소로 접속 했을 때는 쿠키가 있는지 여부를 확인합니다. 없다면 로그인 페이지로 보냅니다. 있다면 인삿말을 보냅니다.
* 쿠키에 민감정보를 넣는 것은 매우 위험하며 쿠키가 조작될 위험도 있습니다.

```js
const http = require('http');
const fs = require('fs');
const url = require('url');
const qs = require('querystring');

const parseCookies = (cookie = '') =>
  cookie
    .split(';')
    .map(v => v.split('='))
    .map(([k, ...vs]) => [k, vs.join('=')])
    .reduce((acc, [k,v]) => {
      acc[k.trim()] = decodeURIComponent(v);
      return acc;
    }, {});

const session = {};

http.createServer( (req, res) => {
  const cookies = parseCookies(req.headers.cookie);
  if (req.url.startWith('/login')) {
    const { query } = url.parse(req.url);
    const { name } = qs.parse(query);
    const expires = new Date();
    expires.setMinutes(expires.getMinutes() + 5);
    const randomInt = Date.now();
    session[radomInt] = {
      name,
      expires,
    };
    res.writeHead(302, {
      Location: '/',
      'Set-Cookie': `session=${randomInt}; Expires=${expires.toGMTString()}; HttpOnly; Path=/`,
    });
    res.end();
  } else if (cookies.session && session[cookies.session].expires > new Date()) {
    res.writeHead(200, { 'Content-Type': 'text/html'; 'charset=utf-8' });
    res.end(`${session[cookies.session].name}님 안녕하세요`);
  } else {
    fs.readFile('.server4.html', (err, data) => {
      if (err) {
        throw err;
      }
      res.end(data);
    });
  }
})
  .listen(8084, () => {
    console.log('8084번 포트에서 서버 대기 중입니다!');
  });
```

쿠키에 이름을 담아서 보내는 대신 randomInt 라는 임의의 숫자를 보냈습니다. 이름과 만료시간은 session 객체에 저장합니다. cookie.session이 있고 만료기한을 넘기지 않았다면 session 객체에서 정보를 가져옵니다. 실제로는 세션을 변수에 저장하지 않고 데이터베이스에 넣어둡니다.

### REST API와 라우팅

* 요청이 주소를 통해 들어오므로 서버가 이해하기 쉬운 주소를 사용하는 것이 좋습니다.
* REST API는 REpresentational State Transfer의 약어로 **서버의 자원을 정의하고 자원에 대한 주소를 지정하는 방법** 을 가리킵니다.
* **REST API** 는 의미를 명확히 전달하기 위해 명사로 구성되며 /user 이면 사용자 정보에 관련된 자원을 요청하는 것이고 /post라면 게시글에 관련된 자원을 요청하는 것이라고 추측할 수 있어야 합니다.
* GET - 서버 자원을 가져오고자 할 때 사용합니다.
* POST - 서버에 자원을 새로 등록하고자 할 때 사용합니다.
* PUT - 서버의 자원을 요청에 들어있는 자원으로 치환하고자 할 때 사용합니다.
* PATCH - 서버 자원의 일부만 수정하고자 할 때 사용합니다.
* DELETE - 서버의 자원을 삭제하고자 할 때 사용합니다.

이렇게 주소와 메소드만 보고 요청의 내용을 명확하게 알아볼 수 있다는 것이 장점입니다. **GET 메소드의 경우 브라우저에서 캐싱할 수도 있어서 같은 주소의 GET 요청을 할 때 캐싱을 사용에 성능을 개선할 수 있습니다** 또한, HTTP 프로토콜을 사용하면 클라이언트가 누구든 상관없이 서버와 소통할 수 있습니다. 이 말은 **서버와 클라이언트가 분리** 되어 있다는 것이며 추후에 서버를 확장할 때 클라이언트에 구애되지 않아 좋습니다.

* **REST API를 따르는 서버를 RESTful 하다고 합니다.**
* 코드를 작성하기 전에 대략적인 주소를 먼저 설계하는 것이 좋습니다.

| HTTP 메서드 | 주소 | 역할 |
|:---------:|:---|:----|
| GET | / | restFront.html 파일 제공 |
| GET | /about | about.html 파일 제공 |
| GET | /users | 사용자 목록 제공 |
| GET | 기타 | 기타 정적 파일 제공 |
| POST | /users | 사용자 등록 |
| PUT | /users/사용자id | 해당 id의 사용자 수정 |
| DELETE | /users/사용자id | 해당 id의 사용자 제거 |

```js
function getUser() {
  var xhr = new XMLHttpRequest();
  var xhr = new XMLHttpRequest();
  xhr.onload = function () {
    if (xhr.status === 200) {
      var users = JSON.parse(xhr.responseText);
      var list = document.getElementById('list');
      list.innerHTML = '';
      Object.keys(users).map(function (key) {
        var userDiv = document.createElement('div');
        var span = document.createElement('span');
        span.textContent = user[keys];
        var edit = document.createElement('button');
        edit.textContent = '수정';
        edit.addEventListener('click', function() {
          var name = prompt('바꿀 이름을 입력하세요');
          if (!name) {
            return alert('이름을 반드시 입력하셔야 합니다');
          }
          var xhr = new XMLHttpRequest();
          xhr.onload = function () {
            if (xhr.status === 200) {
              console.log(xhr.responseText);
              getUser();
            } else {
              console.error(xhr.responsText);
            }
          };
          xhr.open('PUT', '/users/' + key);
          xhr.setRequestHeader('Content-Type', 'application/json');
          xhr.send(JSON.strigyfy({ name: name}));
        });
        var remove = document.createElement('button');
        remove.textContent = '삭제';
        remove.addEventListener('click', function () {
          var xhr = new XMLHttpRequest();
          xhr.onload = function () {
            if (xhr.status === 200) {
              console.log(xhr.responseText);
              getUser();
            } else {
              console.error(xhr.responseText);
            }
          };
          xhr.open('DELETE', '/usrs/' + key);
          xhr.send();
        });
        userDiv.appendChild(span);
        userDiv.appendChild(edit);
        userDiv.appendChild(remove);
        list.appendChild(userDiv);
      });
    } else {
      console.error(xhr.responseText);
    }
  };
  xhr.open('GET', '/users');
  xhr.send();
}
window.onload = getUser;

document.getElementById('form').addEventListener('submit', function (e) {
  e.preventDefault();
  var name = e.target.username.value;
  if (!name) {
    return alert('이름을 입력하세요');
  }
  var xhr = new XMLHttpRequest();
  xhr.onload = function () {
    if (xhr.status === 201) {
      console.log(xhr.responseText);
      getUser();
    } else {
      console.error(xhr.responseText);
    }
  };
  xhr.open('POST', '/users');
  xhr.setRequestHeader('Content-Type', 'application/json');
  xhr.send(JSON.stringify({name: name}));
  e.target.username.value = '';
});
```

페이지가 로딩되면 GET /users로 사용자 목록을 가져오고 수정 버튼과 삭제 버튼에 각각 PUT /users/사용자id와 DELETE /users/사용자id로 요청을 보내도록 지정했습니다/ form을 제출할 때는 POSR /user로 데이터와 함께 요청을 보냅니다.

```js
const http = require('http');
const fs = require('fs');

const users = {};

http.createServer((req, res) => {
  if (req.method === 'GET') {
    if(req.url === '/') {
      return fs.readFile('./restFront.html', (err, data) => {
        if (err) {
          throw err;
        }
        res.end(data);
      });
    } else if ( req.url === '/about') {
      return fs.readFile('./about.html', (err, data) => {
        if (err) {
          throw err;
        }
        res.end(data);
      });
    } else if (req.url === '/users') {
      return res.end(JSON.stringify(users));
    }
    return fs.readFile(`.${req.url}`, (err,data) => {
      if (err) {
        res.writeHead(404, 'NOT FOUND')
        return res.end('NOT FOUND');
      }
      return res.end(data);
    });
  } else if (req.method === 'POST') {
    if (req.url === '/users') {
      let body = '';
      req.on('data', data => {
        body += data;
      });
      return req.on('end', () => {
        console.log('POST 본문(Body):', body);
        const { name } = JSON.parse(body);
        const id = Date.now();
        user[id] = name;
        res.writeHead(201);
        res.end('등록 성공');
      });
    }
  } else if (req.method === 'PUT') {
    if (req.url.startsWith('/users')) {
      const key = req.url.split('/')[2];
      let body = '';
      req.on('data', data => {
        body += data;
      });
      return req.on('end', () => {
        console.log('PUT 본문(Body):', body);
        users[key] = JSON.parse(body).name;
      });
    }
  } else if (req.method === 'DELETE') {
    if (req.url.startsWith('/users')) {
      const key = req.url.split('/')[2];
      delete users[key];
      return res.end(JSON.strigify(users));
    }
  }
  res.writeHead(404, 'NOT FOUND');
  return res.end('NOT FOUND');
})
  .listen(8085, () => {
    console.log('8085번 포트에서 서버 대기 중입니다.');
  });
```

* req.method를 사용해서 요청이 어떤 메소드를 사용했는지 알 수 있습니다. 따라서 해당 기준으로 if문을 분기처리 했습니다.
* 크롬 개발자 도구의 Network 탭에서 네트워크 요청을 실시간으로 볼 수 있습니다. 데이터는 메모리상의 변수에 저장되어 있으므로 서버를 종료하기 전까지 유지됩니다.

### https와 http2

* https 모듈은 웹 서버에 SSL 암호화를 추가합니다. GET, POST 요청을 할 때 오고 가는 데이터를 암호화해서 ㅈ우간에 다른 사람이 내용을 확인할 수 없게 해줍니다
* 발급받은 인증서가 있는 경우 첫번째 인자에 인증서에 관련된 옵션객체를 전달해 https 서버를 만들 수 있습니다.
* http2는 SSL 암호화와 더불어 최신 HTTP 프로토콜인 http/2를 사용합니다. http/1.1보다 개선된 요청/응답 방식을 사용하여 웹의 속도가 개선됩니다.
* http2는 https와 유사하나 createServer 메소드를 createSecureServer 메소드로 바꿔주면 됩니다.

### cluster

클러스터 모듈은 **싱글 스레드인 노드가 CPU 코어를 모두 사용할 수 있게 해주는 모듈** 입니다. 포트를 공유하는 노드 프로세스를 여러 개 둘 수도 있어서 **요청이 많이 들어왔을 때 병렬로 실행된 서버의 개수만큼 요청이 분산** 되게 할 수도 있습니다. 코어가 8개인 서버가 있을 때 노드는 보통 코어를 하나만 사용합니다 하지만 클러스터 모듈을 설정하여 코어 하나당 노드 프로세스 하나가 돌아가게 할 수 있습니다. **세션을 공유하지 못하는 등의 단점** 이 있습니다. 이것은 Redis 등의 서버를 도입하여 해결할 수 있습니다.

```js
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  console.log(`마스터 프로세스 아이디: ${process.pid}`);
  //CPU 개수만큼 워커를 생산
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
  //워커가 종료되었을 때
  cluster.on('exit', (worker, code, signal) => {
    console.log(`${worker.process.pid}번 워커가 종료되었습니다.`);
  });
} else {
  //워커들이 포트에서 대기
  http.createServer( (req, res) => {
    res.write('<h1>Hello Node!</h1>');
    res.end('<p>Hello Cluster!</p>');
  }).listen(8085);

  console.log(`${process.pid}번 워커 실행`);
}
```

* 클러스터에는 마스터 프로세스와 워커 프로세스가 있습니다. 마스터는 CPU 갯수만큼 워커 프로세스를 만듭니다.
* 워커 프로세스가 실질적인 일을 하는 프로세스입니다.

클러스터 모듈을 사용해서 직접 클러스터링을 구현할 수도 있지만 실무에서는 **pm2 등의 모듈로 클러스터 기능을 사용합니다.** REST API와 라우팅의 경우 주소가 많아질 수록 관리하기가 어렵습니다. 이런 문제를 모듈을 사용해서 해결할 수 있습니다.

### 함께 보면 좋은 자료

* <a href="https://nodejs.org/dist/latest-v10.x/docs/api/http.html">http 모듈 소개</a>
* <a href="https://nodejs.org/dist/latest-v10.x/docs/api/https.html">https 모듈 소개</a>
* <a href="https://nodejs.org/dist/latest-v10.x/docs/api/http2.html">http2 모듈 소개</a>
* <a href="https://nodejs.org/dist/latest-v10.x/docs/api/cluster.html">클러스터 모듈 소개</a>
* <a href="https://developer.mozilla.org/ko/docs/Web/HTTP/Cookies">쿠키 설명</a>
* <a href="https://developer.mozilla.org/ko/docs/Web/HTTP/Session">세션 설명</a>
