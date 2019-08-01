---
layout: post
title: 부스트코스 - Swift&iOS - 2주차
description: >
  커넥트 재단의 Swift와 iOS 강의, 그리고 현업 선배님들의 리뷰를 통해 배우게 된 것을 정리하기 위한 포스팅 입니다.
author: author

---

Swift&iOS 강의 2주차 학습 내용 리뷰

\#부스트코스 \#iOS프로그래밍

![500x400](https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_2.png)

## Human Guide Interface
해당 강의에서는 H.G.I 문서의 중요성에 대해서 알 수 있었습니다. 해당 문서의 항목을 보면 크게 iOS 플랫폼 테마의 특징과 iOS11의 새로운 특징부터 앱의 구조, 사용자 상호작용, 각종 뷰와 컨트롤과 기술들에 대한 설계 지침이 나와있습니다. 해당 문서를 준수하며 기능 구현을 해야 <b>사용자에게 좋은 UX를 제공할 수 있기 때문</b>에 신입 iOS 개발자로서 해당 문서를 자주 찾아보는 습관을 가져야 겠습니다.

## Navigation Interface(stack) vs Modal
해당 강의에서는 View이동에 관한 2가지 방법을 배웠습니다. Navigation과 Modal을 이용한 두 가지 방법이었는데 두 구현방식의 차이점은 <b>정보의 연속성</b>에 있었습니다. 많은 다른 앱들이 이러한 점을 고려하여 화면이동을 구현했을 것이기 때문에 좋은 UX를 위해서는 정보의 연속성을 고려하여 화면 이동을 구현해야겠습니다.

## UIViewController 뷰의 상태변화
![500x400](https://cphinf.pstatic.net/mooc/20180718_111/1531896601065H8NTL_PNG/2__.png)
해당 강의에서는 뷰가 화면에 표시되거나 레이아웃에 변화가 생길 때 어떠한 상태변화를 거치는 지 알 수 있었습니다. 화면에 뷰가 표시될 때 호출되는 함수의 순서는 다음과 같습니다.

1. func viewDidLoad() //뷰가 메모리에 로드 됨
1. func viewWillAppear(_ animate: Bool) //뷰가 화면에 표시될 예정
1. func viewWillDidAppear(_ animate: Bool) //뷰가 화면에 표시됨
1. func viewWillDisappear(_ animate: Bool) //뷰가 화면에서 사라질 예정
1. func viewDidDisappear(_ animate: Bool) //뷰가 화면에서 사라짐

## Design Pattern(Singleton)
해당 강의에서는 싱글톤 디자인 패턴을 사용한 Model 관리에 대해서 알 수 있었습니다. 강의에서 소개된 예제는 여러개의 뷰컨트롤러가 공통으로 접근하는 유저 정보에 대해 싱글톤을 적용시켜 하나의 데이터 객체만 존재하도록 하였습니다. 또 한 디자인패턴을 잘못적용하는 것은 차라리 쓰지 않느니만 못하다는 얘기를 강사님께서 해주셨기 때문에 개발에 앞서 적용할 디자인패턴의 장점과 활용 예를 분명히 알아야겠습니다.

## Deligation, Target-Action
관련 강의에서는 User Interaction을 처리할 때의 두 가지 방법에 대해서 알 수 있었습니다. 델리게이션은 하나의 객체가 다른 객체를 대신하여 동작 또는 조정할 수 있는 기능입니다.

델리게이션은 뷰컨트롤러에 사용할 해당 델리게이트의 프로토콜을 채택하고 뷰컨트롤러를 델리게이트로 등록한 다음 사용할 메소드를 재정의 하여 사용하는 방식입니다. 델리게이션의 장점은 동일한 동작에 대해 커스텀 컨트롤러에서 세부구현을 통해 다양한 대응을 할 수 있다는 것입니다.

타겟-액션 디자인패턴에서 객체는 이벤트가 발생했을 때 다른 객체에게 메시지를 보내는데 필요한 정보입니다. 객체에 발생할 수 있는 이벤트 종류들은 UIControlEvents에 정의되어 있습니다. 액션은 특정 이벤트가 발생했을 때 호출될 메소드를 가리키며 타겟은 액션이 호출될 객체를 의미합니다. 일반적으로 타겟은 컨트롤러가 됩니다. 인터페이스 빌더에서는 \@IBAction 양식을 사용했지만 여기서 호출될 메소드는 \@obj 양식을 사용해야 합니다. \@obj 양식은 컴파일러에게 Object-C 스타일 코드라고 알려주는 것입니다.

## 프로젝트2의 중점사항
* Gesture Recognizer를 뷰마다 사용하여 텍스트 뷰 외의 탭을 인삭하여 Editing 모드를 종료함
* 각 UIView의 값들이 변경됨을 감지하는 메소드를 델리게이션 방식으로 재정의 하여 사용자가 모든 값을 입력했는지 확인함
* 어떤 UIView의 값이 마지막에 입력될 지 알 수 없으므로 모든 UIView 컴포넌트에 대해 값이 변결될 경우 유효성 검사를 하는 checkValidate() 메소드를 호출함
```
func checkValidate(){
    if idTextField.hasText, pwTextField.hasText, checkTextField.hasText , introduceTextView.hasText, isEditImage{
        print("all data are input")
        if let password: String = pwTextField.text,
        let checkpw: String = checkTextField.text{
            if password.elementsEqual(checkpw){
                print("password is checked")
                nextButton.isEnabled = true
            }else {
                nextButton.isEnabled = false
            }
        }
    }else {
        print("some data missing")
        nextButton.isEnabled = false
    }
}
```
* 세 번째 뷰에서 취소를 누를 경우 싱글톤으로 관리되는 유저 정보를 지워야 했는데 버튼을 눌렀을 때 유저 정보를 지우는 것은 처리가 되지 않았음, <b>첫 번째 뷰의 viewDidLoad()에서 유저 정보를 가져왔는데 이 메소드가 유저 정보를 지우기 전에 먼저 호출되었기 때문이었음<b>
* 따라서 첫 번째 뷰에서 유저 정보를 가져오는 작업을 viewWillAppear()에서 처리하는 것으로 위의 문제를 해결함.
```
override func viewWillAppear(_ animated: Bool) {
    if let userId: String = UserInformation.shared.id{
        userIdText.text = userId
    }else{
        userIdText.text = nil
    }
}
```
* 오토레이아웃의 제약사항을 꼼꼼히 설정하지 않아 첫 번째, 세 번째 뷰에서 일부 UI요소가 화면에 보이지 않음, <b>다양한 시뮬레이터를 통해 확인을 하지 않은 결과</b>이며 리뷰 실패를 함
![500x400](https://sungwon-choi-29.github.io/assets/img/blog/boostcourseResult2_1.png)

* 리뷰어 선배님의 조언 내용과 오토레이아웃을 수정하여 다시 리뷰를 받은 결과
![500x400](https://sungwon-choi-29.github.io/assets/img/blog/boostcourseResult2_2.png)

* 가로모드에서 테스트 하지 않아 또 다시 Fail을 받음, 세 번째 리뷰 진행 중.
![500x400](https://sungwon-choi-29.github.io/assets/img/blog/boostcourseResult2_3.png)

* 최종 리뷰 결과
![500x400](https://sungwon-choi-29.github.io/assets/img/blog/boostcourseResult2_4.png)

## Summary
* User Interaction을 처리하는 2가지 디자인 패턴(Target-Action, Deligation)과 싱글톤 디자인 패턴에 대한 이해
* 화면 이동 및 각종 기능 구현 시 H.I.G를 준수하여 UX를 고려하는 개발을 지향해야 한다는 것을 알게 됨
* 뷰의 이동과 뷰의 상태변화에 따른 메소드 호출을 통해 다수의 뷰를 관리할 수 있게 됨
* 오토레이아웃 관련 테스트를 진행할 때 <b>다양한 크기의 기기와 가로모드를 꼭 테스트<b> 해야한 다는 것을 알게 됨
