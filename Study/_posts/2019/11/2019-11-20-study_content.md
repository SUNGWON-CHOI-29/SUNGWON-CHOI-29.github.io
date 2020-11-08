---
layout: post
title: Node.js 교과서 학습 정리 (6)
description: >
  Node.js 교과서(조현영) 책을 바탕으로 학습 내용을 정리한 포스팅 입니다.
author: author
comments: true
---

Node.js 교과서 학습 정리 (6)

## MySQL

* 데이터를 변수에 저장한다는 것은 컴퓨터 메모리에 저장한다는 것으로 서버가 종료되면 메모리의 값이 날아가기 때문에 데이터도 사라진다
* 데이터 베이스를 사용해야 데이터를 안전하게 보존할 수 있으며 관계형 데이터베이스로 MySQL, NoSQL에 몽고디비가 있다.

### 데이터 베이스란?

**데이터 베이스란 관련성을 가지며 중복이 없는 데이터들의 집합** 이다. 데이터베이스를 관리하는 시스템을 DBMS라 한다.

### MySQL 설치하기

* macOS에서는 Homebrew를 통해 설치하는 것이 좋다. 홈브루는 다음의 명령어로 설치할 수 있다. `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

* 홈브루에서는 `brew install mysql` 명령어로 설치를 하고 `brew service start mysql`로 서비스를 시작하고 `mysql_secure_installation` 명령어로 루트 비밀번호를 설정할 수 있다.
* `mysql -h localhost -u root -p` 멍령어로 MySQL에 접속할 수 있다.

### 워크벤치 설치하기

* 콘솔에서는 데이터를 한눈에 보기에 무리가 있으므로 워크벤치라는 프로그램을 사용하면 데이터베이스 내부에 저장된 데이터를 시각적으로 관리할 수 있다.

### 데이터베이스 및 테이블 생성하기

* `CREATE SCHEMA [데이터베이스명]` 으로 데이터베이스를 생성할 수 있으며 MySQL에서 스키마와 데이터베이스는 같은 개념이다.
* `use [데이터베이스명]` 은 앞으로 해당 데이터베이스를 사용하겠다는 것이다.
* 테이블이란 데이터가 들어갈 수 있는 틀을 의미합니다.
* `CREATE TABLE [데이터베이스명].[테이블명]`을 사용해서 테이블을 만듭니다.
* `DESC [테이블명]` 를통해 만들어진 테이블을 확인할 수 있습니다.

### CRUD 작업하기

* CRUD란 Create, Read, Update, Delete의 머릿말로 데이터베이스에서 많이 하는 작업을 말합니다.
* Create는 데이터를 생성해서 데이터베이스에 넣는 작업입니다. `INSERT INTO [데이터베이스명].[테이블명] (field) VALUES ('value')`를 통해 추가할 수 있습니다.
* Read는 데이터베이스에 데이터를 조회하는 작업입니다. `SELECT [조건] FROM [데이터베이스명].[테이블명]`을 통해 조회할 수 있습니다.
* Update는 데이터를 수정하는 것으로 `UPDATE [데이터베이스명].[테이블명] SET field = 'value' WHERE [조건]` 으로 수정할 수 있습니다.
* DELETE는 데이터를 삭제하는 것으로 `DELETE FROM [데이터베이스명].[테이블명] WHERE [조건]` 입니다.

### 시퀄라이즈 사용하기

* 노드에서 MySQL 데이터베이스 접속을 할 때 작업을 쉽게할 수 있도록 도와주는 라이브러리가 **Sequelize** 입니다.
* `npm i sequelize mysql2` 을 사용해서 패키지를 설치합니다.
* `npm i -g sequelize-cli` 를 사용해서 cli를 전역 설치합니다.
* `sequelize init` 명령어를 호출하여 초기화 합니다.

### 함께 보면 좋은 자료

* <a href="https://ko.wikipedia.org/wiki/데이터베이스">데이터베이스 설명</a>
* <a href="https://dev.mysql.com/doc/refman/8.0/en/">MySQL 매뉴얼</a>
* <a href="http://docs.sequelizejs.com">시퀄라이즈 문서</a>
