---
layout: post
title: React-Native로 크로스 플랫폼 뮤직 플레이어 앱 만들기(iOS) - 2
description: >
  [9.16 ~ 9.29]
  부스트코스 에이스 커리어 부스팅 프로그램 중 기업과제 관련 포스팅
author: author
comments: true
---
\#부스트코스 \#React-Native \#사운드짐

## 학습 내용
### react-native
* Component

리액트 네이티브는 리액트와 같습니다 그러나 웹 컴포넌트 대신에 네이티브 컴포넌트를 빌딩블록으로 사용하는 것이 다른점입니다. 그래서 리액트 네이티브의 기본 구조를 이해하기 위해서는 기본 리액트 컴포넌트들과 <b>state</b>와 <b>props</b>에 대해 아셔야 할 필요가 있습니다.

#### Hello World in react-native
```JavaScript
import React, { Component } from 'react';
import { Text, View } from 'react-native';

export default class HelloWorldApp extends Component {
  render() {
    return (
      <View style= {
          {flex: 1,
          justifyContent: "center",
          alignItems: "center"}
        }>
        <Text>Hello, world!</Text>
      </View>
    );
  }
}
```
ES6은 자바스크립트의 개선된 집합이고 모든 브라우저에서 지원하는 공식적인 표준입니다. 따라서 호환성에 대한 걱정없이 사용할 수 있습니다. import, from, class, extends는 ES6의 피처들입니다.

```
<View>
  <Text>Hello world!</Text>
</View>
```
이 코드는 자바스크립트 내에 내장된 XML 문법인 JSX입니다. JSX는 마크업 언어를 코드안에 사용할 수 있도록 해줍니다. <div>처럼 웹의 HTML처럼 보이기도 하죠. 리액트 네이티브 앱을 만들 때 기본 요소가 컴포넌트가 되며 화면에 보이는 모든 것이 컴포넌트 입니다. 컴포넌트에서 요구되는 것은 render함수로 이것은 렌더링 될 JSX를 리턴합니다.

* Props

대부분의 컴포넌트들은 생성시에 다른 매개변수를 통해 커스텀될 수 있습니다. 이 생성시에 전달되는 매개변수를 props라고 합니다. properties의 축약어 입니다.

리액트 네이티브의 기본적인 컴포넌트 중 하나는 Image입니다. 이미지를 생성할 때 source라는 prop을 사용해서 보여줄 이미지를 조정할 수 있습니다.
#### Props example
```JavaScript
import React, { Component } from 'react';
import { Text, View } from 'react-native';

class Greeting extends Component {
  render() {
    return (
      <View style= {
        {alignItems: 'center'}
      }>
        <Text>Hello {this.props.name}!</Text>
      </View>
    );
  }
}

export default class LotsOfGreetings extends Component {
  render() {
    return (
      <View style= {
        {alignItems: 'center', top: 50}
        }>
        <Greeting name='Rexxar' />
        <Greeting name='Jaina' />
        <Greeting name='Valeera' />
      </View>
    );
  }
}
```
JSX에서 자바스크립트 표현을 사용할 때는 중괄호로 묶어줘야 합니다. {pic}은 pic변수를 JSX내에서 사용할 수 있게 해줍니다. Greeting 컴포넌트에서 name props를 활용하여 재사용하는 것을 볼 수 있습니다. View 컴포넌트는 다른 컴포넌트를 담는 컨테이너 역활이며 스타일과 레이아웃을 컨트롤하는데 도움이 됩니다.

* state

컴포넌트를 컨트롤하는데 두가지 종류의 데이터가 있습니다. props와 state입니다. props는 부모에 의해서 설정되며 컴포넌트의 생명주기 동안 고정적입니다. 데이터가 변하는 경우에는 state를 사용합니다. 일반적으로 state는 생성자에서 초기화하며 setState를 통해 상태값을 변경합니다.

#### State example
```JavaScript
import React, { Component } from 'react';
import { Text, View } from 'react-native';

class Blink extends Component {

  componentDidMount(){
    // Toggle the state every second
    setInterval(() => (
      this.setState(previousState => (
        { isShowingText: !previousState.isShowingText }
      ))
    ), 1000);
  }

  //state object
  state = { isShowingText: true };

  render() {
    if (!this.state.isShowingText) {
      return null;
    }

    return (
      <Text>{this.props.text}</Text>
    );
  }
}

export default class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text='I love to blink' />
        <Blink text='Yes blinking is so great' />
        <Blink text='Why did they ever take this out of HTML' />
        <Blink text='Look at me look at me look at me' />
      </View>
    );
  }
}
```
일반적으로 state 설정은 서버로부터 새로운 데이터가 있거나 사용자 입력으로부터 설정됩니다. 또한 <b>Redux</b>나 <b>Mobx</b>같은 state 컨테이너를 사용해서 데이터 플로우를 컨트롤할 수 있습니다. setState가 호출되면 컴포넌트가 다시 렌더링됩니다. 리액트에서 state와 똑같이 동작하므로 더욱 자세한 내용은 <a href="https://reactjs.org/docs/react-component.html#setstate">React.Component API</a>에서 확인할 수 있습니다.

* Style

리액트 네이티브에서는 스타일을 정의하기 위해 특별한 언어나 문법을 사용할 필요가 없습니다. 모든 컴포넌트들은 style이라는 이름의 프로퍼티를 가지고 있습니다. style은 웹에서 CSS가 동작하는 것과 일치하는 경우가 많습니다. 스타을의 배열을 전달할 수도 있습니다. 컴포넌트가 많을 경우 깔끔하게 하기 위해서 StyleSheet를 사용합니다. 여러개의 스타일을 한 곳에 모아둠으로서 가독성을 높일 수 있습니다.

* Flexbox

컴포넌트의 하위 레이아웃은 flexbox 알고리즘을 사용해서 정의할 수 있습니다. flexbox는 다양한 화면의 레이아웃을 구성하기 위해 디자인 되었습니다.

flexboxDriection - 하위 항목이 전개될 방향을 설정하는 프로퍼티로 중심 축으로 간주되기도 합니다. row는 하위 항목을 왼쪽에서 오른쪽으로 정렬하며 column(default)은 위에서 아래로 정렬합니다. row-reverse는 오른쪽에서 왼쪽, column-reverse는 아래에서 위로 정렬합니다.

alignItems - 하위항목들이 컨테이너의 세로축에서 어떻게 나열될지 표현하는 프로퍼티입니다. justifyContent와 비슷하지만 가로축에 적용되는 것이아니라 세로축에 적용됩니다.

justifyContent - 하위항목이 컨테이너의 가로축에서 어떻게 나열될지 표현하는 프로퍼티입니다. 이 프로퍼티를 사용해서 컨테이너 내부에 수평적으로 하위항목을 배치할 수 있습니다.


* alignItems
<center>
<img src="https://cdn-images-1.medium.com/max/800/1*evkM7zfxt-9p-HJ1M0Bh2g.png"/>
</center>

* justifyContent
<center>
<img src="https://cdn-images-1.medium.com/max/800/1*i5TVlme-TisAVvD5ax2yPA.png"/>
</center>

### ES6
* Arrow Function
애로우 함수는 ES6에서 추가된 피처로 익명의 Function Expression을 간결히 표현할 수 있는 문법입니다. 특이한 점은 매개변수의 갯수에 따라 문법이 달라지게 되며 리턴 값이 한줄의 코드일 경우 return 키워드를 생략할 수 있습니다. 애로우 함수는 매개변수를 담는 괄호부분과(생략가능) => 화살표 부분 그리고 함수의 바디인 statement로 구성되어 있습니다.

```
const name = (parameters) => {
  statements
}
```

Function Expression과 비교한 애로우 함수 사용례는 다음과 같습니다.

```
const add3 = function(num1, num2, num3){
  return num1 + num2 + num3;
}

const add3 = (num1, num2, num3) => num1+ num2 + num3
```

```
const square = function(num){
  return num ** 2;
}

const square = num => num ** 2;
```

```
const sayHi = function(){
  console.log('Hi');
}


const sayHi = ()=> {
  console.log('Hi')
}
```

## 앱 이미지
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/soundGym_1.gif"/>
</center>

## 피드백 결과
<a href="https://github.com/connect-boostcamp/careerboost_SOUNDGYM/pull/2">PR 코멘트 Url</a>

1.<b>react life cycle</b>
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/soundGym_2.png"/>
</center>

2.ArrowFunction binding
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/soundGym_3.png"/>
</center>

3.Promise
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/soundGym_4.png"/>
</center>

4.async/await
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/soundGym_5.png"/>
</center>

5.Functional Component
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/soundGym_6.png"/>
</center>

6.적절치 않은 변수명
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/soundGym_7.png"/>
</center>

7.삼항 연산자 처리 및 track 추가 시 예외처리
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/soundGym_8.png"/>
</center>

8.컴포넌트 분리
<center>
<img src="https://sungwon-choi-29.github.io/assets/img/blog/soundGym_9.png"/>
</center>

리액트 네이티브를 사용해봐서 재밌었고 핫리로드 기능과 레이아웃과 코드가 한 곳에 있다보니 확실히 생산성이 향상된 것을 느낄 수 있었습니다. 또한 사운드짐 관계자분께서 자세하게 코드리뷰를 해주셔서 매우 좋았습니다. 코멘트 주신 내용을 수정하는 작업과 react-native-router-flux를 이용해 조금 더 복잡한 UI를 구성할 수 있도록 할 예정입니다.

## 추가 학습 및 피드백 적용 대상
* ReactNative - lifeCycle, 컴포넌트 최적화, Functional Component
* ES6 - ArrowFunction non-binding, Promise 패턴, async/await
* 기타 - 컴포넌트 분리, 변수명 조정, README.md 수정
