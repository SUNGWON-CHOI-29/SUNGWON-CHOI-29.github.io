---
layout: post
title: React-Native로 크로스 플랫폼 뮤직 플레이어 앱 만들기(iOS) - 3
description: >
  [9.16 ~ 9.29]
  부스트코스 에이스 커리어 부스팅 프로그램 중 기업과제 관련 포스팅
author: author
comments: true
---
\#부스트코스 \#React-Native \#사운드짐

### 추가 학습 내용
react-native(react), ES6
### 사용 라이브러리
react-native, react-native-router-flux, react-native-track-player

## 추가 학습 내용
* ReactNative - lifeCycle, 컴포넌트 최적화, Functional Component

### lifeCycle 및 최적화
리액트에서는 state가 변화될 때마다 다시 렌더링을 하게 됩니다. 그리고 <b>react-native-track-player의 ProgressComponent의 경우 고정적으로 1초마다 position과 progress를 변경</b>하게 됩니다. 해당 컴포넌트에서 state 값을 변경할 경우 TrackPlayer에서 가져오는 값이 연결되지 않으므로 구조를 변경하는데 문제가 있어서 해당 이슈를 해결하지는 못했습니다.

리액트에서 라이프사이클은 다음과 같습니다.
* constructor() - 컴포넌트 생성, state 설정
* render()
* componentDidMount() - 타이머 설정 등,
* shouldComponentUpdate() - 리턴 값이 true일 때 render 수행
* componentWillUpdate()
* render()
* componentDidUpdate()

따라서 기존의 질문내용을 구현하려면 TrackPlayer의 position과 progress 값을 밀리세컨드 단위로 변경하게 되면 해당 state가 변경되므로 render가 더욱 빈번하게 수행됩니다. 이 작업은 플레이어가 재생 중일 때만 해당되므로 TrackPlayer의 state가 STATE_PLAYING 일 때만 컴포넌트를 업데이트 하게 함으로써 더욱 최적화가 가능합니다.
렌더링 할 필요가 없는 부분을 직접 조작함으로써 최적화가 가능하다는 말은 리액트 네이티브로 만들어진 앱은 기본적으로 최적화가 보장되지 않는다는 의미입니다. <a href="https://facebook.github.io/react-native/docs/performance">performance docs</a>에서는 리액트는 초당 60프레임의 성능을 보장하지만 앱의 성능 최적화에 대한 작업의 여지를 남겨둔 것에 대해 유감을 표시하고 있으며 성능 이슈에 대한 <a href="https://facebook.github.io/react-native/docs/performance#profiling">링크</a>를 통해 해법을 제시하고 있습니다.

리액트 라이프사이클에 대해 알게되면서 이번 기업 탐방 중 일부 기업에서 성능과 최적화 이슈로 iOS/AOS 네이티브 앱을 병행 개발한다는 이야기를 들었는데 그 배경에 대해서 알게되었습니다.

### Functional Component
펑셔널 컴포넌트는 스스로 state나 리액트 네이티브의 라이프사이클 메소드를 갖지 않는 컴포넌트를 말합니다. stateless components라고도 불리며 상위계층으로 받은 props를 이용하여 렌더링을 하거나 간단한 작업을 수행하는 컴포넌트 입니다.
이번 기업과제 중 ImageButton의 경우 클릭 이벤트 및 이미지 props, state가 모두 상위계층에서 관리되므로 펑셔널 컴포넌트로 간단히 구성하는 할 수 있습니다.

펑셔널 컴포넌트의 예시는 다음과 같습니다.
```
import React from 'react';

function Hello(props) {
    return (
        <div>Hello {props.name}</div>
    );
}

export default Hello;
```

애로우 펑션 예시는 다음과 같습니다.
```
import React from 'react';

const Hello = (props) => {
    return (
        <div>Hello {props.name}</div>
    );
}

export default Hello;
```

## Summary
간단한 프로젝트를 진행함으로써 ES6의 문법적인 특징과 lifeCycle과 같은 리액트 컴포넌트에 대한 추가적인 학습의 필요성을 느끼게 되었습니다. 사운드짐 관계자분께서 리뷰해주신 내용 중 남겨진 부분도 차근차근 학습하여 더욱 기본을 다질 수 있도록 하겠습니다.
