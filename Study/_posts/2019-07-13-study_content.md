---
layout: post
title: 부스트코스 - Swift&iOS - 1주차
description: >
  커넥트 재단의 스위프트와 iOS 강의, 그리고 현업 선배님들의 리뷰를 통해 배우게 된 것을 정리하기 위한 포스팅 입니다.
author: author

---

Swift&iOS 강의 1주차 학습 내용 리뷰

![500x400](https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_1.png)

## iOS - 뮤직플레이어 만들기(따라하기)

### Xcode 사용 법 및 단축키

Xcode는 애플의 IDE로서 애플사 제품의 앱을 제작하는 것은 물론 다양한 환경의 응용 프로그램을 만들 수 있습니다.

오랜만에 다시 Xcode를 사용하면서 사용법도 많이 까먹었지만 해당 강의를 통해 다시 Xcode와 친해질 수 있었고 강의 내용 중 야곰님께서 cmd+r, cmd+., cmd+shift+y 같이 매우 유용하고 자주 사용하는 단축키들을 알려주시기 때문에 더욱 좋았습니다.

### 인터페이스 빌더

인터페이스 빌더는 안드로이드 스튜디오에서 XML 레이아웃을 구성하는 것과 비슷했습니다. 이번 주차의 강의 내용은 따라하기 위주기 때문에 편안한 마음으로 교육을 들을 수 있었고 Xcode의 버전이 달라짐으로써 변경된 사항이 있었는데 내용 보완 항목을 통해 확인할 수 있어서 헷갈릴 일이 없었습니다.

### IBAction & IBOutlet

인터페이스 빌더의 객체를 코드와 연결하는 과정이었습니다. 객체와 빌더가 연결된 이후 리펙터를 통하지 않고 이름을 변경하게 되면 해당 객체와 빌더의 연결이 끊어지게 되고 오류가 발생하게 됩니다. 이름을 바꿀 때는 리펙터를 통해 안전하게 객체의 이름을 바꿔야 겠습니다.

IBAction은 객체에서 발생하는 액션을 코드로 연결하는 것으로 어떤 이벤트를 감시할 것인지 선택할 수 있고 해당 이벤트가 발생하면 원하는 코드를 수행할 수 있는 일종의 트리거 연결이었습니다. 마찬가지로 이름이 바뀌게 되면 오류가 발생하게 되니 주의해야 합니다.

### Asset

에셋은 MVC 디자인 구조로 보면 모델에 속하는 요소로서, 응용프로그램에 쓰이는 리소스 들입니다. Assets.xcassets라는 폴더가 자동으로 생성되는데 해당 폴더에서 앱에서 쓰이는 에셋을 관리할 수 있고 이를 <b>에셋 카탈로그</b>라고 합니다.

또한 해당 강의 내용 중 앱 시닝의 개념을 배우게 되었는데 앱 시닝은 앱이 사용자의 디바이스에 설치될 때 디바이스의 특성에 맞게 설치되록 하는 <b>설치 최적화</b> 기술입니다. 기술 구성요소로는 <b>슬라이스, 비트코드, 주문형 리소스</b>가 있으며 이중 슬라이싱은 개발자가 전체 버전을 iTunes에 업로드 하면 앱스토어에는 다양한 버전의 조각들이 생성되고 사용자가 앱을 설치할 때 가장 적합한 조각이 설치되게 하는 것입니다.

나머지 다른 기술 구성요소인 비트코드와 주문형 리소스에 대해서도 따로 찾아봐야 겠습니다.

### 오토레이아웃

오토레이아웃은 디바이스의 환경이 바뀜에 따라 앱의 화면구성이 자동으로 바뀌게 해주는 것으로 코드로 작성할 수도, 인터페이스 빌더를 사용해서 작성할 수도 있습니다. '녹초보' 리뷰어님의 말씀으로는 두 방식 중 어떤 것이 확실히 좋다 하는 것이 없기 때문에 두가지 방법에 모두 익숙한 것이 좋다고 조언해 주셨습니다.

코드로 오토레이아웃을 작성하는 것은 좀 더 세밀하게 할 수 있으나 객체 간의 위치와 크기를 지정하는데 시간이 걸렸고 인터페이스 빌더는 빠르게 할 수 있으나 세밀하게 컨트롤 하기는 조금 부족했습니다.

![500x400](https://sungwon-choi-29.github.io/assets/img/blog/boostcourse_result_1.png)

## Swift - 문법

### 기본 자료형
스위프트의 기본 자료형에서는 기타 다른 언어와 크게 차이점은 없었습니다. 다만 다른 자료형의 경후 암시적연 형변환을 통해 오류가 발생하는 것을 막고자 타입이 다른 변수간의 값 교환이 컴파일러 수준에서 오류를 뱉어 줍니다. 그리고 let은 상수 지정 키워드로서 값이 한번 할당되면 변하지 않는 것에 대해서 사용되는 것으로 let으로 값을 지정한 변수에 다시 값을 지정하면 오류가 발생합니다. var는 변수를 지정하는 키워드로 반대로 값을 할당하지 않으면 오류가 발생합니다. var와 let으로 상수,변수를 구분짓게 한 것은 사용자가 유발할 수 있는 오류를 줄이려는 시도로 느껴졌습니다.

### 구조체
구조체는 사소한 문법의 차이 말고는 타 언어와 유사했습니다.
```
// 학생 구조체 사용 예
struct Student {
	// 가변 프로퍼티
    var name: String = "unknown"

    // 키워드도 `로 묶어주면 이름으로 사용할 수 있습니다
    var `class`: String = "Swift"

    // 타입 메서드
    static func selfIntroduce() {
        print("학생타입입니다")
    }

    // 인스턴스 메서드
    // self는 인스턴스 자신을 지칭하며, 몇몇 경우를 제외하고 사용은 선택사항입니다
    func selfIntroduce() {
        print("저는 \(self.class)반 \(name)입니다")
    }
}

// 타입 메서드 사용
Student.selfIntroduce() // 학생타입입니다

// 가변 인스턴스 생성
var yagom: Student = Student()
yagom.name = "yagom"
yagom.class = "스위프트"
yagom.selfIntroduce()   // 저는 스위프트반 yagom입니다

// 불변 인스턴스 생성
let jina: Student = Student()

// 불변 인스턴스이므로 프로퍼티 값 변경 불가
// 컴파일 오류 발생
//jina.name = "jina"
jina.selfIntroduce() // 저는 Swift반 unknown입니다
```

### 열거형
스위프트에서 열거형은 매우 강력합니다. C언어는 열거형이 숫자로 변환되어 처리되는 반면 스위프트에서는 열거형에 사용한 타입 그 자체를 사용할 수 있습니다. 또한 메소드를 추가 할 수 있는 점이 독특했습니다. 그리고 스위치 구문에서 매우 효과적으로 사용할 수 있습니다.
```
//열거형 메소드 사용 예
enum Month {
    case dec, jan, feb
    case mar, apr, may
    case jun, jul, aug
    case sep, oct, nov

    func printMessage() {
        switch self {
        case .mar, .apr, .may:
            print("따스한 봄~")
        case .jun, .jul, .aug:
            print("여름 더워요~")
        case .sep, .oct, .nov:
            print("가을은 독서의 계절!")
        case .dec, .jan, .feb:
            print("추운 겨울입니다")
        }
    }
}

Month.mar.printMessage()
```

### 함수
스위프트는 함수형 언어를 지원하는 다중 패러다임 언어이기 때문에 함수를 일급객체로 취급할 수 있습니다. 그래서 함수를 변수, 상수에 할당할 수 있으며 매개변수를 통해 전달할 수도 있습니다. 그리고 리턴값일 경우 return 생략 등 컴파일러가 인식할 수 있는 범위에 한해 사용자 편의적인 문법이 많이 있다는 것을 알 수 있었습니다.

```
//함수 타입 예
var someFunction: (String, String) -> Void = greeting(to:from:)
someFunction("eric", "yagom") // Hello eric! I'm yagom

someFunction = greeting(friend:me:)
someFunction("eric", "yagom") // Hello eric! I'm yagom


// 타입이 다른 함수는 할당할 수 없습니다 - 컴파일 오류 발생
//someFunction = sayHelloToFriends(me: friends:)


func runAnother(function: (String, String) -> Void) {
    function("jenny", "mike")
}

// Hello jenny! I'm mike
runAnother(function: greeting(friend:me:))

// Hello jenny! I'm mike
runAnother(function: someFunction)
```

### 옵셔널
옵셔널은 스위프트에서 처음 알게된 개념으로 변수의 값이 있을 수도 있고 없을 수도 있는 것을 고려해 사용하는 것입니다. 옵셔널로 선언된 변수는 if-let 구문을 통해 값을 꺼내올 수 있게되며 이 과정에서 해당 변수에 값이 있는지 여부에 따라 다른 처리를 할 수 있습니다. 이 옵셔널로 인해 NULL인지 확인해야 하는 변수의 경우 그 처리과정을 매우 손쉽고 깔끔하게 해결할 수 있습니다.

```
//옵셔널 추출 예
func printName(_ name: String) {
    print(name)
}

var yourName: String! = nil

if let name: String = yourName {
    printName(name)
} else {
    print("yourName == nil")
}
```

### 클로저
클로저 또한 스위프트에서 처음 접한 개념으로 <b>실행가능한 코드 블럭</b>을 의미합니다. 클로저 기준에 따르면 함수는 이름이 있는 클로저 입니다. 이 클로저는 함수처럼 매개변수 전달과 반환 값을 사용할 수 있으며 함수의 전달인자로써도 많이 쓰입니다.
```
//함수의 전달인자로서 클로저

let add: (Int, Int) -> Int
add = { (a: Int, b: Int) in
    return a + b
}

let substract: (Int, Int) -> Int
substract = { (a: Int, b: Int) in
    return a - b
}

let divide: (Int, Int) -> Int
divide = { (a: Int, b: Int) in
    return a / b
}

func calculate(a: Int, b: Int, method: (Int, Int) -> Int) -> Int {
    return method(a, b)
}

var calculated: Int

calculated = calculate(a: 50, b: 10, method: add)

print(calculated) // 60

calculated = calculate(a: 50, b: 10, method: substract)

print(calculated) // 40

calculated = calculate(a: 50, b: 10, method: divide)

print(calculated) // 5

//따로 클로저를 상수/변수에 넣어 전달하지 않고,
//함수를 호출할 때 클로저를 작성하여 전달할 수도 있습니다.

calculated = calculate(a: 50, b: 10, method: { (left: Int, right: Int) -> Int in
    return left * right
})

print(calculated) // 500
```

또한 클로저는 다음과 같은 규칙을 통해 축약될 수 있습니다.
1. 후행 클로저 : 함수의 매개변수로 전달되는 경우 함수 밖에 구현 가능
1. 반환 타입 생략 : 컴파일러가 클로저의 타입을 유추할 수 있는 경우 매개변수, 반환 타입 생략 가능
1. 단축 인자 이름 : 컴파일러가 타입을 유추할 수 있는 경우 전달인자를 $0,$1로 대체 가능
1. 암시적 반환 : 반환 값이 있는 경우 마지막 행은 반환 값으로 간주되어 return 이 필요없습니다.

```
//축약 전
result = calculate(a: 10, b: 10, method: { (left: Int, right: Int) -> Int in
    return left + right
})

//축약 후
result = calculate(a: 10, b: 10) { $0 + $1 }

print(result) // 20
```

<b>지나친 축약은 가독성을 떨어트리므로 주의해야 합니다.</b>

## Summary

* iOS는 MVC 패턴 틀을 기본적으로 제공해주며 Controller 부분에 Asset(Model)과 사용자 에게 보여지는 View를 관리하는 코드를 쓴다
* Xcode에서 View 간의 계층 구조를 보며 문제를 찾을 수 있는 기능이 좋았다.
* 이번 예제를 통해 Xcode의 사용법을 알게 되었고 인터페이스 빌더, 오토레이아웃등 가장 중요하고 많이 쓰일 개념에 대해 알 수 있었다.
* Swift는 함수형 언어를 지원하는 다중 패러다임 언어이다.
* Swift는 서로 다른 자료형 간에 자료변환 중 발생하는 오차로 인한 오류를 막기 위해 형변환이 매우 엄격하다.
* Swift에서는 열거형 자료형이 매우 강력하다. 정수형으로 변환되는 것이 아닌 이름 자체를 사용할 수 있다.
* 클로저는 생략할 수 있는 표현이 많아 짧게 쓸 수 있으나 가독성을 고려해야 한다.
