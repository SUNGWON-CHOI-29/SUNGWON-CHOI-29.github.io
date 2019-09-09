---
layout: post
title: 부스트코스 - Swift&iOS - 4주차
description: >
  커넥트 재단의 Swift와 iOS 강의, 그리고 현업 선배님들의 리뷰를 통해 배우게 된 것을 정리하기 위한 포스팅 입니다.
author: author

---

Swift&iOS 강의 4주차 학습 내용 리뷰

\#부스트코스 \#iOS프로그래밍

## 학습목표
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_4.png"/>
</center>

## Photos
포토 프레임워크는 iOS 및 macOS 환경에서 사진 및 비디오에 직접 접근할 수 있는 클래스를 제공합니다. 해당 프레임워크의 <b>PHPhotoLibrary</b>는 공유 객체를 통해 PHAsset, PHAssetCollection, PHCollectionList 인스턴스를 읽기 전용으로 가져올 수 있습니다. 변경 작업이 필요한 경우 변경된 인스턴스를 PHPhotoLibrary에 변경요청 메소드를 호출하면 해당 변경사항이 공유 객체에 적용됩니다.

PHPhotoLibrary의 공유객체는 PHCollectionList - PHAssetCollection - PHAsset 의 계층구조를 가지며 아래의 그림과 같습니다.
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_4_1.png"/>
</center>

## 동시성/비동기 프로그래밍
<b>동시성/비동기 프로그래밍은 앱의 성능 및 사용자 UX에 굉장히 큰 영향을 주는 요소로 매우 중요합니다.</b> iOS에서는 언어에서 OperionaQueue 통해 비동기 프로그래밍을 지원합니다. main 큐에 코드블럭의 작업을 요청하거나 백그라운드의 큐에 작업을 요청할 수 있습니다. <b>주의점으로는 UI관련된 사항은 꼭 main 큐에서 수행되어야 한다는 것</b>이며 이것을 준수하지 않으면 컴파일러 단계에서 경고를 표시합니다.

실제 강의에서는 짧은 개념만 알려주시고 큰 이미지를 불러올 때 앱이 멈추는 현상만 간략히 보여주셨습니다. 그러나 과제를 통해 콜렉션 뷰에서 데이터를 읽어올 때와 공유 라이브러리의 변화를 감지했을 때 해당 사항이 원활히 콜렉션 뷰에 적용되도록 하기 위해서는 비동기 프로그래밍의 개념을 활용할 필요가 있었습니다.

과제를 진행하면서 가장 애를 먹었던 부분이었지만 직접 실습을 통해 iOS에서 비동기 프로그래밍을 처리하는 기초적인 방법에 대해 확실히 알 수 있었습니다.

## 스크롤 뷰
스크롤 뷰는 해당 뷰의 subView를 스크롤하거나 확대할 수 있는 뷰입니다. ScrollView를 상속받는 뷰로는 테이블뷰, 컬렉션뷰, 텍스트 뷰들이 있습니다. 줌 기능을 구현하기 위해서는 ScrollViewDelegate를 활용하여 줌이 될 객체를 지정해야 합니다. ViewForZooming 메소드를 통해 스크롤 뷰 객체에 줌 기능이 적용될 UIView 객체를 전달할 수 있습니다.

## 네비게이션 아이템
해당 강의에서는 네비게이션 바와 하단의 툴바에 들어가는 BarButtonItem에 대해서 알 수 있었습니다. 특이사항으로는 오토레이웃과 관련된 제약조건을 StoryBoard에서 설정할 수가 없고 대신 Flexible BarButtonItem을 활용하여 쉽게 바 버튼간의 간격을 조정할 수 있다는 것입니다. 프로그래밍으로 BarButtonItem을 정렬하는 법에 대해 찾아봐야 겠습니다.

## 컬렉션 뷰
컬렉션 뷰는 구조적으로 테이블 뷰와 유사합니다. DataSource를 통해 컬렉션 뷰의 셀들의 데이터를 넘겨주게 됩니다. 컬렉션 뷰의 다른점은 Flowlayout을 통해 셀의 크기와 간격, 스크롤 방향 등을 설정할 수 있다는 것입니다. 셀의 크기를 설정하는 프로퍼티는 itemSize와 estimateItemSize가 있습니다. itemSize는 모든 셀의 크기를 동일하게 적용하는 것이고 estimateItemSize는 오토레이아웃을 통해 셀이 스스로 크기를 정하는 것입니다. 이 때 셀의 대략적인 최소크기를 전달해 주는 것으로 estimateItemSize 프로퍼티를 사용합니다.

컬렉션 뷰의 개념은 테이블 뷰와 유사하여 데이터소스를 이용하여 셀에 데이터를 넣는 기능은 손쉽게 구현하였지만 플로우레이아웃이 모바일 기기의 방향에 따라 올바르게 적용되지 않아 많이 고생을 했습니다.

## 자료 공유
자료공유 및 기타 내보내기 서비스들은 UIActivityViewController를 활용하면 해당 클래스에서 제공하는 여러 서비스들을 손쉽게 사용할 수 있습니다. UIActivityViewController 생성자에는 공유하는 아이템과 어플리케이션이 지원하는 커스텀 서비스들을 추가하여 전달할 수 있습니다. UIActivityViewController 인스턴스를 생성하고 원하는 아이템을 넣어 초기화를 하고 present를 호출하는 방식으로 구현했습니다.

## 과제 중점사항
이번 과제는 많이 애먹은 만큼 재미도 있었고 배운 것이 많았습니다. 우선 비동기성 프로그래밍의 개념에 대해서 알고 있었고 앱이 프리징현상이 걸리지 않으려면 잘 써야한다는 것도 알고 있었습니다. 그러나 처음부터 확실한 개념을 적용하여 프로그래밍을 설계하지 않고 나중에 기능을 추가하다 보니 디버깅이 매우 어려웠습니다. 비효율적인 방법이었지만 그래도 디버깅을 하며 iOS에서 operatinQueue를 통해 비동기성 프로그래밍을 어떻게 지원하고 처리되는지 기본적인 방법을 확실히 알 수 있었습니다.

PHPhotoLibrary 프레임워크에 대해서는 강의를 통해 막연히 개념을 알게 되었지만 직접 실습을 통해 Asset과 관련된 모델 클래스의 계층과 공유 객체를 처리하는 법에 대해 확실히 알 수 있었습니다. 여러 뷰에서 공통적으로 사용하는 CollectionList, AssetCollection, Asset을 어떻게 관리할지도 중점사항이었습니다. 해당 인스턴스들을 가져오고 업데이트 하는 구조체를 만들어서 타입 메소드와 타입 프로퍼티를 이용해 여러개의 뷰에서 동일한 인스턴스에 접근할 수 있도록 처리했습니다.

끝으로 공유객체에 변경사항이 있을 경우 이 것을 처리하는 photoLibraryDidChange 메소드가 비동기적으로 수행되기 때문에 해당메소드에서 작업을 처리하는 것이 까다로웠습니다.

강의에서 과제에 필요한 전체적인 기능을 모두 배우는 것 보다는 오히려 기본적인 사항을 배우고 과제를 통해 추가적인 기능들을 Apple Developer 문서를 통해 직접 찾아보며 학습하는 것도 색다른 재미였습니다. 기능 구현에 테스트할 요소가 많았기 때문에 예외처리할 것이 많았고 그만큼 기능을 많이 상세히 알게되었고 재미있는 과제였습니다.

## 리뷰 결과
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourseResult4_2.png"/>
</center>
Operation Queue를 처리하는 과정에서 컬렉션 뷰의 데이터를 리로드하는 메소드를 오퍼레이션 큐의 백그라운드에서 수행되는 작업이 다 끝내고 호출해야 하는데 그렇지 않은 부분이 일부 있었습니다. 일부 뷰에서 ReloadData를 잘못호출 한 부분을 수정했습니다.

alpha 값 처리, 네비게이션 바 및 툴바 처리는 잘못된 메소드 사용으로 인해 Fail 처리 되었습니다. 기존 Cell 자체의 알파값을 수정하는 것에서 Cell내의 imageView의 알파값을 수정함으로써 화면 전환이 일어나도 뷰의 투명도가 유지되도록 하였습니다.

네비게이션 바와 툴바의 경우 네비게이션 컨트롤러의 프로퍼티에서 isHidden과 관련된 프로퍼티를 처리해야 했지만 네비게이션 바의 프로퍼티와 툴바 자체의 프로퍼티를 처리함으로써 네비게이션 컨트롤러에서 해당 뷰들을 그려준 후 hidden이 되었기 때문에 공간을 차지하는 오류가 있었습니다.

해당 오류들은 올바른 프로퍼티인 self.navigationController?.isNavigationBarHidden, self.navigationController?.isToolbarHidden 를 사용함으로써 처리했습니다.

<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourseResult4_3.png"/>
</center>
iOS 리뷰 점검기간으로 리뷰결과를 기다리는 중입니다.

## Summary
* 컬렉션 뷰, 스크롤 뷰, 네비게이션 아이템 등 UIView에 관련된 요소 학습
* 비동기성 프로그래밍, PHPhotoLibrary 프레임워크, 내보내기 기능 학습
