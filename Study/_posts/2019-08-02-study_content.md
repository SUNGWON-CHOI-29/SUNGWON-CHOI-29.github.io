---
layout: post
title: 부스트코스 - Swift&iOS - 3주차
description: >
  커넥트 재단의 Swift와 iOS 강의, 그리고 현업 선배님들의 리뷰를 통해 배우게 된 것을 정리하기 위한 포스팅 입니다.
author: author

---

Swift&iOS 강의 3주차 학습 내용 리뷰

\#부스트코스 \#iOS프로그래밍

## 학습목표
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_3.png"/>
</center>
## TableView
테이블 뷰는 정보를 리스트 형태로 보여줄 수 있는 레이아웃으로써 많은 앱에서 활용되는 사용자 인터페이스 입니다. 해당 강의를 통해 테이블 뷰의 기본적인 구성과 형태에 대해 알 수 있었습니다. 테이블 뷰는 하나의 열과 다수의 행으로 구성되며 <b>Cell</b> 하나가 하나의 <b>행</b>에 해당합니다.
<center>
<img src="https://cphinf.pstatic.net/mooc/20180120_75/1516452980003BId4E_PNG/123_2.png"/>
</center>
기본 스타일의 테이블 뷰
{:.figure}

<center>
<img src="https://cphinf.pstatic.net/mooc/20180120_207/1516452998158XgYpC_PNG/123_3.png"/>
</center>
섹션을 그룹으로 구분 짓는 테이블
{:.figure}

<center>
<img src="https://cphinf.pstatic.net/mooc/20180208_290/1518017999963lFHYL_PNG/123_1.png"/>
</center>
테이블 뷰의 헤더와 푸터, 섹션의 영역
{:.figure}

### TableViewDataSource
뷰 컨트롤러에서 테이블 뷰의 셀에 데이터를 넣어주기 위해서는 TableViewDataSource 델리게이트를 사용해야 합니다. 해당 델리게이트를 준수하기 위해서는 다음과 같은 2개의 메소드를 구현해야 합니다.
```
```

Android의 리사이클러뷰에 데이터를 넣어주기 위한 어댑터의 역할을 iOS에서는 데이터소스가 수행하는 것 같았습니다.

## TableViewCell

### CustomTableViewCell

## 뷰의 재사용
테이블을 구성하는 셀이 매우 많을 경우 화면에 표시되는 셀의 갯수를 생각하면 모든 셀에 메모리를 할당하는 것은 무척이나 비효율적인 메모리 사용일 것입니다. 따라서 화면에 표시되지 않는 셀은 회수하여 다음 셀을 만들 때 재활용 됩니다. 이것을 위해 사용되는 메소드는 다음과 같습니다.
```
```

## 스토리보드 세그
해당 강의에서는 뷰 컨트롤러간 이동을 할 때 데이터를 전달해주는 방법에 대해 알 수 있었습니다.

## JSON Decode
해당 강의에서는 Json파일을 디코딩하여 배열의 형태로 가지고 있다가 cell에 하나씩 넣어주는 것을 배웠습니다. 이 강의를 통해

## 과제 중점사항
과제를 수행하는데 있어서 코드 리팩토링을 고려한 두가지 사항입니다.
1. 구조체의 타입 메소드와 프로퍼티 활용

1. 커스텀 셀을 생성할 때 as! 처리

## Summary
*
*
