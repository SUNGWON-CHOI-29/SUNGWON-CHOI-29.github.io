---
layout: post
title: Medium - Simple MVP Design Pattern in Swift
description: >
  <a href="https://medium.com/swlh/simple-mvp-design-pattern-in-swift-3655811e0415">원문 링크 - David McCallum</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - Swift에서 쓸 수 있는 간단한 MVP 디자인 패턴

![500x400](https://cdn-images-1.medium.com/max/1600/1*Yf9H3RWc9pdcnxxco_dTqQ.png)

많은 사람들이 스위프트 공부를 시작할 때 MVC 모델에 익숙해 집니다. 그러나 MVC모델은 뷰컨트롤러가 매우 많아지고

앱의 로직에 대하여 단위테스트를 수행하는 것도 제한적입니다.

Massive VC 문제를 해결하기 위한 대안으로 MVP 모델이 있습니다. 무겁고 많은 뷰 컨트롤러의 로직을 프레젠터를

호출하는 것으로 대신할 수 있습니다.

따라서 프레젠터에 있는 모든 것들을 테스트할 수 있고 쉽게 읽고 접근할 수 있습니다.

![500x400](https://cdn-images-1.medium.com/max/1600/1*sGI2Yl9n2YQLImr3RdndLw.png)

간단하고 기본적인 앱은 우리가 MVP 모델을 구성하는데 도움이 될 것입니다. 앱의 기능은 매우 작고 간단합니다.

버튼을 5번 터치하면 라벨이 바뀌게 됩니다 배경의 색깔도 함께 말이죠


기본적으로 단일 뷰 프로젝트에서 ViewController.swift 파일은 이렇게 생겼습니다.

~~~Swift
import UIKit
class ViewController: UIViewController {

lazy var presenter = Presenter(with: self)
  @IBOutlet weak var changeTextLabel: UILabel!
  override func viewDidLoad() {
    super.viewDidLoad()
  }
  @IBAction func tapMeButton(_ sender: Any) {
    presenter.buttonTapped()
  }
}
~~~

우리는 뷰 컨트롤러에게 프레젠터에게 접근할 수 있도록 할겁니다. 그래서 뷰가 로드되면 프레젠터의 self를 전달해줍니다.

tapMeButton이 터치되면 우리는 프레젠터를 호출하게 됩니다.

다음으로 Presenter.swift 파일의 내용을 봅시다

~~~ Swift
import Foundation
protocol PresenterView: class {
    func updateLabel()
  }
  class Presenter {
    weak var view: PresenterView?
    // Pass something that conforms to PresenterView
    init(with view: PresenterView) {
      self.view = view
    }
  var timesTapped = 0
  func buttonTapped() {
    timesTapped += 1
    if timesTapped >= 5 {
      self.view?.updateLabel()
    }
  }
}
~~~

위의 코드가 프레젠터 뷰의 프로토콜 메소드 입니다.


ViewController 파일에 다음과 같이 확장을 추가합시다

~~~swift
extension ViewController: PresenterView {
   func updateLabel() {
   changeTextLabel.text = "I have been changed!"
   self.view.backgroundColor = .yellow
 }
}
~~~

해당 부분이 우리가 UI 변화를 처리하고 가공하는 영역입니다.

이걸로 끝입니다! 당신의 VC에 더 많은 UI 요소를 추가해보세요

* MVC의 단점은 뷰컨트롤러가 복잡해지고 단위테스트가 어렵다는 것이다
* MVP를 이용해 프레젠터를 사용하면 위의 문제를 해결할 수 있다.
