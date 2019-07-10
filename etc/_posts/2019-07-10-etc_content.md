---
layout: post
title: Medium - Real World:iOS Design Patterns
description: >
  <a href="https://medium.com/cocoaacademymag/real-world-ios-design-patterns-3e5aad172094">원문 링크 - Rodrigo Cavalcante</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - 현실의 iOS 디자인 패턴들

![500x400](https://cdn-images-1.medium.com/max/2600/1*D_lE7ztXABCvrN9jmi3a6w.jpeg)

디자인 패턴은 포럼이나 직장에서 짧게 대화할 때 자주 등장하는 주제입니다.

당신은 책이나 인터넷에서 디자인 패턴에 대해 고무 오리들이나 카페나 피자가게들 을 사용한 많은 예시들을 봤을 것입니다.

제가 패턴에 대해 공부를 할 때 이해는 했지만 어떻게 코드에 적용하는지에 대해 문제가 많이 생기곤 했습니다.

Factory 패턴은 객체를 만들기 위해 사용한다는 것은 이해했지만 왜 그것을 써야하는 지는 몰랐죠

내가 정말 객체를 만드는데 Factory가 필요한가? 같은 의문이 떠올랐습니다.

이 글의 목적은 제가 프로젝트에서 사용한 디자인 패턴들을 통해 실제 예제들을 보여주는 것입니다.

## Strategy

~~~swift

protocol Fly {
  func fly()
}

class Duck: Fly {
  func fly() {
    print("spread wings")
  }
}

class Rocket: Fly {
  func fly() {
    print("vrooommm!!")
  }
}

let flyableObject: Fly = Rocket()
flyableObject.fly()
~~~

### Problem solved using Strategy

~~~swift
protocol LoginViewControllerActions {
    func loginBtnPressed(user: User)
}

//swift 3
protocol LoginViewController: UIViewController {
    let user: User
    var delegate: LoginViewControllerActions?
}
~~~

## Factory

~~~swift
enum PizzaType {
  case cheese
  case pepperoni
  case greek
}

class PizzaFactory {

  func build(type: PizzaType) -> Pizza {
    switch type {
    case cheese:
      return CheesePizza()
    case pepperoni:
      return PepperoniPizza()
    case greek:
      return GreekPizza()
    }
  }

}
~~~

### Problem solved using Factory

~~~swift

protocol LoginViewControllerActions {
    func loginBtnPressed(user: User)
}

//swift 3
protocol LoginViewController: UIViewController {
    let user: User
    var delegate: LoginViewControllerActions?
}

protocol LoginViewControllerFactory {
    func build(delegate: LoginViewControllerActions) -> LoginViewController
}

class ViewCodedLoginViewControllerFactory: LoginViewControllerFactory {
  func build(delegate: LoginViewControllerActions) -> LoginViewController {
    return ViewCodedLoginViewController(delegate: delegate)
  }
}

class StoryboardLoginViewControllerFactory: LoginViewControllerFactory {
  func build(delegate: LoginViewControllerActions) -> LoginViewController {
     let viewController = UIStoryboard(name: "Main", bundle: nil).instantiateViewControllerWithIdentifier("LoginViewController") as LoginViewController
     viewController.delegate = delegate
     return viewController
  }
}

let viewController = factory.build(delegate: self) //LoginViewControllerFactory
self.presentViewController(viewController, animated: false, completion: nil)
~~~

## Decorator

~~~swift

protocol Beverage {
    func cost() -> Double
    func description() -> String
}

class Coffee: Beverage {
    func cost() -> Double {
        return 0.95
    }

    func description() -> String {
        return "Coffe"
    }
}

class Whip: Beverage {
    let beverage: Beverage

    init(beverage: Beverage) {
        self.beverage = beverage
    }

    func cost() -> Double {
        return 0.45 + self.beverage.cost()
    }

    func description() -> String {
        return self.beverage.description() + ", Whip"
    }
}

var darkRoast: Beverage = Coffee()
darkRoast = Whip(beverage: darkRoast)

darkRoast.description()
darkRoast.cost()
~~~

### Problem solved using decorator

~~~swift

public typealias JsonObject = [String : Any]

public protocol Request {
    func request(method: HTTPMethod, data: JsonObject, header: JsonObject?, completion: @escaping (Result) -> Void)
}

public class MyRequest: Request {

    public init() {

    }

    public func request(method: HTTPMethod, data: JsonObject, header: JsonObject?, completion: @escaping (Result) -> Void) {
        //do request
    }
}

public class MyHeader: Request {

    let request: Request
    let header: [String: String]

    public init(request: Request, apiVersion: APIVersion = .standard){
        self.request = request
        self.header = ["myapikey": "apiKey",
                       "key" : "key",
                       "version" :  "\(apiVersion.rawValue)"]

    }

    public func request(method: HTTPMethod, data: JsonObject, header: JsonObject?, completion: @escaping (Result) -> Void) {

        let mutableHeader = self.header + (header ?? [:])

        self.request.request(method: method, data: data, header: mutableHeader, completion: completion)
    }
}

let v1Request: Request = MyHeader(request: MyRequest(), apiVersion: .v1)
let standardRequest: Request = MyHeader(request: MyRequest())
~~~

~~~swift

protocol Service {
  func fetch(completion: @escaping (Result<[String]>) -> Void) -> Void
}

class ViewControllerLoader<D> {
    func load(completion: @escaping (Result<D>) -> Void) {
      fatalError("load method need to be override on subclasses")
    }
}

class ServiceViewControllerLoader: ViewControllerLoader<[String]> {

  let service: Service

  init(service: Service) {
        self.service = service
  }

    override func load(completion: @escaping (Result<[String]>) -> Void) {
        self.service.fetch() { (result) in
            switch result {
            case .success(let strings):
                completion(.success(strings))
            case .error(let error):
                completion(.error(error))

            }
        }
    }
}

class ServiceViewControllerLoaderDecorator: ViewControllerLoader<[String]> {

  let loader: ViewControllerLoader<[String]>

  init(loader: ViewControllerLoader<[String]>) {
        self.loader = loader
  }

  func filter(data: [String]) {
    //do filtering
  }

  override func load(completion: @escaping (Result<[String]>) -> Void) {

        self.loader.service.fetch { (result) in
            switch result {
            case .success(let strings):
                let filteredStrings = self.filter(data: strings)
                completion(.success(filteredStrings))
            case .error(let error):
                completion(.error(error))
            }
        }
    }
}
~~~


## Adapter

~~~swift

public struct Card {
    var lastNumber: String = ""
}

public struct PassKitCard {

    let passKitCard: PKPaymentPass?

    public func toCard() -> Card {
        return Card(lastNumber: paymentPass.primaryAccountNumberSuffix)
    }
}
~~~

### Problem solved using Adapter

~~~swift

public protocol LastNumber {
    var lastNumber: String { get }
}

public struct PassKitLastNumber: LastNumber {

    let passKitCard: PKPaymentPass?

    public var lastNumber: String {

        if let paymentPass = self.passKitCard {
            return paymentPass.primaryAccountNumberSuffix
        }

        return ""
    }
}

class Card: LastNumber {

    let card: Card

    init(card: Card) {
        self.card = card
    }

    var lastNumber: String {
        return self.card.lastNumbers
    }
}
~~~

## summary
* 디자인 패턴은 코드의 재사용성을 높여주기 때문에 시간을 절약하게 된다.
* 디자인 패턴은 잘 공부해야 적용된 디자인만 보고도 해당 프로그램의 구조를 파악할 수 있다.
* 디자인 패턴을 잘 이해해야 개발자 간에 구조에 대해서 효율적으로 얘기할 수 있다.
