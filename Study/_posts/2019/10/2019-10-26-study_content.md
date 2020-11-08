---
layout: post
title: Node.js Study (20)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
Node.js Study (20)

## The basics of working with MySQL and Node.js
MySQL은 가장 유명한 관계형 데이터베이스 입니다. 노드 에코시스템은 MySQL을 사용해서 데이터를 저장하고 조회하는 등의 작업을 할 수 있는 다양한 패키지를 제공합니다. 우리는 mysqljs/mysql을 사용할 것이며 오랜기간동안 깃허브에서 1만2천개의 별을 받아온 패키지 입니다.

### Installing the Node.js MySql package
<center>
```
npm install mysql
```
</center>

### Initializing the connection to the database
<center>
```js
//먼저 패키지를 포함시킵니다.
const mysql = require('mysql')
//그리고 커넥션을 만듭니다.
const options = {
  user: 'the_mysql_user_name',
  password: 'the_mysql_user_password',
  database: 'the_mysql_database_name'
}
const connection = mysql.createConnection(options)
//호출을 통해 새로운 커넥션을 유발할 수 있습니다.
connection.connect(err => {
  if (err) {
    console.error('An error occurred while connection to the DB')
    throw err
  }
})
```
</center>

### The connection options

위의 예제에서 options 객체는 3개의 옵션을 가지고 잇습니다.
<center>
```js
const options = {
  user: 'the_mysql_user_name',
  password: 'the_mysql_user_password',
  database: 'the_mysql_database_name'
}
```
</center>
다음은 여러분들이 많이 사용하는 것들입니다.
* host - 데이터베이스의 호스트네임으로 기본은 localhost 입니다.
* port - MySQL 서버 포트번호로 기본은 3306 입니다.
* socketPath - 호스트/포트번호를 대신해서 지정된 유닉스 소켓을 사용할 떄 쓰입니다.
* debug - 기본적으로 비활성화 되어 있으며 디버깅에 사용할 수 있습니다.
* trace - 기본적으로 활성화 되어 있으며 에러 발생 시 누적된 추적을 출력합니다.
* ssl - 서버에 SSL 연결을 설정할 때 사용합니다.

### Perform a SELECT query

이제 여러분은 데이터베이스에 SQL 쿼리를 보낼 준비가 되었습니다. 실행된 쿼리는 발생할 수 있는 에러와 결과 필드를 가지고 있는 콜백함수를 호출할 것입니다.
<center>
```js
connection.query('SELECT * FROM todos', (error, todos, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }
  console.log(todos)
})
//자동적으로 탈출되는 값을 전달할 수도 있습니다.
const id = 223
connection.query('SELECT * FROM todos WHERE id = ?', [id], (error, todos, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }
  console.log(todos)
})
//여러개의 값을 전달하려면 두번쨰 매개변수로 배열을 전달하면 됩니다.
const id = 223
const author = 'Flavio'
connection.query('SELECT * FROM todos WHERE id = ? AND author = ?',
[id, author], (error, todos, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }
  console.log(todos)
})
```
</center>

### Perform a INSERT query
객체를 전달할 수 있습니다.
<center>
```js
const todo = {
  thing: 'Buy the milk'
  author: 'Flavio'
}
connection.query('INSERT INTO todos SET ?', todo, (error, results, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }
})
//테이블이 auto_increment 하는 주요키가 있다면 results.insertID 값으로 리턴될 것입니다.
const todo = {
  thing: 'Buy the milk'
  author: 'Flavio'
}
connection.query('INSERT INTO todos SET ?', todo, (error, results, fields) => {
  if (error) {
    console.error('An error occurred while executing the query')
    throw error
  }
  const id = results.resultId
  console.log(id)
})
```
</center>

### Close the connection
데이터베이스의 연결을 종료시킬 필요가 있다면  end()메소드를 사용해서 <b>connection.end()</b> 라고 하면 됩니다. 이것은 펜딩 중인 모든 쿼리가 보내지게 된 이후에 종료될 수 있도록 합니다.

## The difference between development and production
개발과 생산환경에 따라서 다른 설정을 할 수 있습니다. 노드에서는 항상 개발 환경인 것으로 가정합니다. NODE_ENV=production 환경변수 값을 설정함으로써 노드에게 생산환경에서 동작 중이라고 알려줄 수 있습니다. 이것은 쉘에서 다음과 같은 명령을 실행하여 수행할 수 있습니다. <b>export NODE_ENV=production</b>

그러나 쉘에서 쉘 설정파일에 해당 명령어를 넣는 것이 더욱 낫습니다. 왜냐면 시스템이 재시작할 때 설정값이 날라가기 때문입니다. 환경 변수를 사용해서 응용프로그램이 초기화 될 때 적용 시킬수도 있습니다. <b>NODE_ENV=production node app.js</b> 이런 환경변수는 매우 유용하고 외부 라이브러리에서도 폭 넓게 사용됩니다. 생산환경으로 설정하는 것은 다음을 보장합니다.
* logging is kept to a minimum, essential level
* more caching levels take place to optimize performance

익스프레스의 템플릿 라이브러리인 Pug를 예로들자면 디버그 모드에서 컴파일을 하면 생산으로 설정되지 않습니다. 익스프레스의 뷰는 항상 개발모드에서 요청되며 생산에서는 캐시됩니다. 이것말고도 다른 예제가 많습니다. 익스프레스는 특정 환경에 대한 설정을 걸어 둘 수 있어서 자동적으로 NODE_ENV 값에 따라 설정이 변경됩니다.

<center>
```js
app.configure('development', () => {
  //...
})
app.configure('production', () => {
  //...
})
app.configure('production', 'staging', () => {

})
//예를 들어서 모드에 따라서 다른 에러핸들러를 설정할 수 있습니다.
app.configure('development', () => {
  app.use(express.errorHandler({ dumpExceptions: true, showStack: true}));
})

app.configure('production', () => {
  app.use(express.errorHandler())
})
```
</center>

## END
