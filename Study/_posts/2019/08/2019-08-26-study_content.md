---
layout: post
title: 부스트코스 - Swift&iOS - 5주차
description: >
  커넥트 재단의 Swift와 iOS 강의, 그리고 현업 선배님들의 리뷰를 통해 배우게 된 것을 정리하기 위한 포스팅 입니다.
author: author
comments: true
---

Swift&iOS 강의 5주차 학습 내용 리뷰

\#부스트코스 \#iOS프로그래밍

## 학습목표
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_5.png"/>
</center>

## Alert and ActionSheet
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_5_1.png"/>
</center>
얼럿과 액션 시트는 사용자에게 알림을 표현하기 위해 사용하는 것으로 UIAlertController를 사용하여 생성한 인스턴스에서 스타일 구분을 통해 구현할 수 있습니다.

UIAlertAction 클래스는 얼럿컨트롤러에 추가될 액션들을 만드는 것으로 타이틀과 메시지등의 프로퍼티 설정과 함께 완료되었을 때 핸들러 처리를 통해 사용자 행동에 따른 원하는 기능을 구현할 수 있습니다.

UIAlertAction은 다음과 같은 세가지 스타일이 있습니다.

* default - 기본 스타일의 액션 버튼으로 하나의 UIAlertController는 여러개의 디폴트 액션을 가질 수 있습니다.
* cancel - 작업을 취소하거나 변경사항이 없는 경우 적용하는 스타일입니다.
* destructive - 사용자에게 데이터가 변경되거나 삭제와 같은 돌이킬 수 없는 상황을 나타내는 스타일로서 오직 한 개의 액션만 존재할 수 있습니다.

액션 시트의 경우 액션의 스타일에 따라 위치가 배치되므로 위의 사용법에 맞게 액션 스타일을 설정하는 것이 중요합니다.

## Tab Bar navigationController
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_5_2.png"/>
</center>
텝 바는 위의 이미지와 같이 구성되어 있으며 사용자가 탭바 뷰의 아이템을 클릭하는 것으로 해당 뷰로 전환되게 됩니다. 탭바 컨트롤러 객체는 다시 네비게이션 컨트롤러를 지닐 수 있는데 반대로 네비게이션 컨트롤러가 탭바 컨트롤러를 소유하는 것은 안됩니다.

## Networking
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_5_2.png"/>
</center>
URLSession을 이용하여 세션을 만들고 해당 세션을 이용하여 각종 태스크를 생성함으로써 네트워크 작업을 수행할 수 있습니다.

세션에는 세가지 유형이 있으며 이 유형은 configuration 프로퍼티를 통해 결정할 수 있습니다.
* default Session - URL 다운로드를 위한 기본 세션으로 디스크에 저장합니다.
* Ephemeral Session - 디스크에 어떤 데이터도 저장하지 않고 메모리에 올려서 세션과 연결합니다. 따라서 세션이 만료되면 관련 데이터가 사라집니다.
* Background Session - 백그라운드 세션은 모든 데이터 전송을 별도의 프로세스가 처리합니다.

## GCD
GCD는 Grand Central Dispatch로서 멀티코어와 멀티 프로세싱 환경을 최대한 활용한 프로그래밍을 할 수 있도록 애플이 개발한 기술입니다. 스레드 풀은 운영체제가 관리하기 때문에 프로그래머는 실행할 작업을 DispatchQueue에 추가하기만 하면 GCD가 알아서 스레드를 생성하고 작업이 종료되면 다시 스레드를 제거합니다.

디스패치 대기열은 Serial과 Concurrent 두 종류가 있으며 Serial은 한번에 하나의 태스크만 수행하고 기다리는 반면 Concurrent는 가능한한 많은 작업을 수행합니다.
### OperationQueue와 비교
OperationQueue는 Concurrent DispatchQueue와 동일하게 동작합니다. 연산 대기열에서는 동시에 실행할 수 있는 연산의 최대수를 지정할 수 있고 연산을 일시 중지, 다시 시작, 취소를 할 수 있습니다.

OperationQueue는 비동기적으로 실행되어야 하는 작업을 객체지향적인 방법으로 사용하는데 적합하고 GCD는 간단한 작업이나 특정 유형의 시스템 이벤트를 비동기적으로 처리할 때 적합합니다.

## Notification center
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_5_4.png"/>
</center>
노티피케이션은 노티피케이션 센터를 통해 노티피케이션을 등록하면 해당 노티피케이션을 옵저브하는 메소드에게 지정된 노티피케이션을 발송함은 물론 이 때 User Info를 실어서 전달할 수 있습니다.

노티피케이션 센터에서 발송한 노티피케이션을 처리하는 메소드는 메인 스레드와 동일한 흐름을 따르지 않으므로 처리에 주의해야 합니다.

## 과제 중점 사항

### 네트워크 처리
네트워크 상황과 status code를 이용하여 다양한 네트워크 환경에 적절한 메시지를 보여줄 수도 있었지만 과제 기간 내에 제출하려다 보니 status code가 성공 일때만 받아온 데이터를 전송하는 처리를 수행하고 그 외의 모든 경우에는 사용자에게 얼럿을 띄우도록 처리 했습니다.

### 탭 바에서 공통으로 사용하는 데이터 처리
첫 번쨰 뷰의 경우 테이블 뷰와 컬렉션 뷰에서 공통된 데이터를 사용하기 떄문에 데이터를 모델 단에서 저장하고 각 뷰 컨트롤러에서는 viewWillApear에서 데이터를 가져오는 방식으로 처리했습니다. 문제는 테이블 뷰에서 셀을 클릭하여 다음 테이블 뷰로 넘어가고(tableView1) 탭 바 아이템을 변경하여 컬렉션 뷰에서 셀을 클릭하여 다음 테이블 뷰로 넘어간 경우(tableView2)인데, 하나의 뷰 컨트롤러에서 super view에 따라 각각 자신의 테이블 뷰 데이터를 가질 수 있도록 currentIndex, currentID 변수를 활용하여 처리했습니다.

### 텍스트 뷰 처리
코멘트를 작성하는 기능을 담당하는 텍스트 뷰는 자체에 스크롤링 기능이 있기 때문에 오토레이아웃 만으로는 테이블 뷰의 셀로 정확히 표현되지 않았습니다. 테이블 뷰의 셀은 내부 아이템에 따라서 높이가 지정되는데 오토레이아웃으로 잡아준 아이템의 높이가 자동적으로 늘어나지 않았기 때문입니다. 따라서 superView의 높이를 얻어온 다음 SafeArea에 해당하는 높이와 텍스트 뷰 이전의 셀의 높이, 그리고 테이블 뷰가 그룹 스타일이었기 때문에 SectionFooter의 높이를 계산하여 텍스트 뷰의 크기를 구할 수 있었습니다.

### 레이팅 뷰 처리
안드로이드와는 달리 iOS에서는 레이팅뷰를 기본적으로 제공해 주지 않았습니다. 따라서 오픈소스를 사용하거나 사용자가 구현해야 했는데 부스트코스 에이스에서는 오픈소스 사용을 금지하므로 appleDeveloper의 관련 예제를 참고하여 커스텀 뷰를 만들었습니다. 과제에서 레이팅 뷰가 사용되는 곳은 label 크기(userInteractionEnable = false)와 일반 크기(userInterfaceEnable = true)가 있습니다. 따라서 isLabel 프로퍼티를 이용해 이 두가지를 구분했고 스타일에 따라 기본적인 크기와 사용자 인터렉션을 알맞게 설정할 수 있도록 수정했습니다.

버튼을 클릭하면 해당 인덱스까지 selected 상태의 이미지가 표시될 수 있도록 했고 UIPanGestureRecognizer를 추가하여 변화된 x 좌표 값이 몇 번째 버튼의 위치에 있는 지에 따라 알맞는 이미지가 표시될 수 있도록 하여 사용자가 Pan 제스쳐로 별점을 수정하는 것을 구현했습니다.

## 리뷰 결과
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/boostcourseResult5_1.png"/>
</center>


## iOS 프로젝트 5개 수행 소감
스타트업을 통해 iOS 앱을 개발한 경험은 있지만 기초가 부족했고 HGI를 준수하지 않았기 때문에 굉장히 수준낮은 앱이었습니다. 그러나 <b>부스트코스를 통해 iOS 개발과 스위프트 언어에 대한 학습을 통해 보다 탄탄한 기본을 갖게 되었고 각 과제마다 주어진 기준을 만족하면서도 MVC 패턴을 준수하는 코드를 짜려고 노력했습니다. 그리고 이러한 것을 현업에 계신 선배들의 코드 리뷰를 통해 보완해야할 점을 알게 되고 괜찮은 부분을 칭찬받으며 코딩을 하는 데 있어서 더욱 재미를 느낄 수 있었습니다.</b> 기존에 C++로 그래픽스를 만들었던 경험때문에 유지보수가 어려운 코딩스타일을 갖고 있었는데 (enum을 쓰지 않고 상수를 쓰는 것, for - in을 사용하지 않고 index를 직접 조작하는 것) 이번 기회를 통해 잘못된 것을 깨닫고 고치게 되었습니다. 무엇보다 코드 리뷰를 통해 피드백을 받으며 과제를 수행하는 것 자체가 매우 재미있었고 나중에는 과제 기준표에 없는 기능이라도 보다 나은 UX를 제공한다 싶은 것은 제가 스스로 추가하여 넣기도 했습니다.

아직 기초밖에 모르는 iOS Native 초보 개발자이지만 꾸준히 학습과 트렌드 파악을 통해 실력있는 개발자로 성장하는 길을 알게된 좋은 경험이었습니다.

부스트코스 관련된 과제는 끝이 났지만 React Native를 사용하여 크로스 플랫폼 앱 기업 과제와 구글의 Flutter를 사용하여 크로스 플랫폼 앱 개인 프로젝트를 진행하며 더욱 경험을 쌓도록 하겠습니다.