---
layout: post
title: Node.js 교과서 학습 정리 (7)
description: >
  Node.js 교과서(조현영) 책을 바탕으로 학습 내용을 정리한 포스팅 입니다.
author: author
comments: true
---

Node.js 교과서 학습 정리 (7)

## 몽고디비

* 몽고디비의 특징 중 하나는 자바스크립트를 사용한다는 것이다. 떄문에 자바스크립트만 사용하여 웹 어플리케이션을 만들 수 있다. 하나의 언어만 사용하는 것은 높은 생산성을 가져다 준다.

### NoSQL vs SQL

* MySQL은 SQL을 사용하는 대표적인 데이터베이스이며 SQL을 사용하지 않는 NoSQL 데이터베이스의 대표주자가 몽고디비 이다.
| SQL(MySQL) | NoSQL(몽고디비) |
|:===========|:==============|
| 규칙에 맞는 데이터 입력 | 자유로운 데이터 입력 |
| 테이블 간 JOIN 지원 | 컬렉션 간 JOIN 미지원 |
| 트랜잭션 지원 | 트랜잭션 미지원 |
| 안정성, 일관성 | 확장성, 가용성 |
| 용어( 테이블, 로우, 컬럼 ) | 용어( 컬렉션, 도큐먼트, 필드) |

* NoSQL에는 고정된 테이블이 없고 컬럼을 따로 정의하지 않습니다.
* MySQL 수준의 트랜잭션이 없으므로 데이터 일관성, 무결성에 문제가 있을 수 있다. (몽고디비 4버전부터는 트랜잭션을 지원함)
* 트랜잭션과 JSON을 지원하지 않아도 몽고디비를 사용하는 이유는 확장성과 가용성이 좋기 때문이다.

### 몽고디비 설치하기

```
brew install mongodb
sudo mkdir -p /data/db
Password: [macOS 계정 비밀번호 입력]
```

### 데이터베이스 및 컬렉션 생성하기

* `use [데이터베이스명]`
* `show dbs`
* `db.createCollection('컬렉션명')`
* `show collections`

### CRUD 작업하기

* Create - `db.[컬렉션명].save({})`
* Read - `db.users.find({})`
* Update - `db.[컬렉션명].update({})`
* Delete - `db.[컬렉션명].remove({})`

### 몽구스 사용하기

* 몽구스는 시퀄라이즈와 달리 ODM(Object Document Mapping)이라고 불립니다. 몽고디비에 없어서 불편한 기능들을 몽구스가 보완해줍니다.
* **스키마 라는 것이 생겨서 데이터를 넣기전 노드 서버 단에서 데이터를 한 번 필터링 해주는 역할을 해줍니다.**
* JOIN 기능을 **populate** 라는 메서드로 어느 정도 보완해줍니다. 관계가 있는 데이터를 쉽게 가져올 수 있습니다.
* 몽고디비는 주소를 사용해 연결합니다. 주소형식은 `mongodb://[username:password@]host[:port][\[database][?options]]`입니다. []는 옵셔널입니다.
* host가 localhost, port가 27017, 계정이 있는 데이터베이스가 admin일 경우 주소는 `mongodb://username:pw@localhost:27017/admin`이 됩니다.

### 함께 보면 좋은 자료

* <a href="https://docs.mongodb.com">몽고디비 문서</a>
* <a href="http://mongoosejs.com/docs/guide.html">몽구스 문서</a>
