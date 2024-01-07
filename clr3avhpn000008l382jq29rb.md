---
title: "React 기초 다지기"
datePublished: Wed Nov 23 2022 15:00:00 GMT+0000 (Coordinated Universal Time)
cuid: clr3avhpn000008l382jq29rb
slug: react-basic-study
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704620122734/f8660008-5d2e-48b6-9c13-02715b51319e.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1704620218952/52831eb4-61cc-4cad-9bbc-4e3eb219448f.png
tags: reactjs, basics, study

---

# React의 기초를 다지자!🧱

역시 제일 중요한 것은 기초! 지금까지 리액트를 사용하여 프로젝트를 진행하고 웹 어플리케이션을 만들어왔지만 정작 기초 지식이 많이 부족하다고 느껴왔었다. 그래서 제로초님의 [리액트 무료 강좌(웹게임)](https://www.youtube.com/playlist?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn) 강의를 완강하였고 그 과정에서 리액트의 가장 중요한 기초 지식들을 정리할 수 있었다. 설명이 이해하기 쉽고, 최대한 많은 것을 가르쳐주시려는 게 느껴지는 강의였다. 리액트를 처음 공부하거나, 기초가 부족하다고 느끼시는 분이라면 이 강의를 한 번쯤 듣는 것을 추천한다👍🏻

# React를 사용하는 이유

## SPA

- Single Page Application
  - 사람들이 모바일 기기를 보편적으로 사용하게 됨으로써, 페이지가 명확하게 나뉘어 있는 웹 페이지와는 달리 모바일 어플리케이션과 유사하게 기능하는 웹 서비스의 필요성이 대두됨
    - 페이지가 새로고침 되며 화면이 깜빡이지 않는 등
  - React의 경우 데이터가 바뀌면 화면이 자동으로 따라서 바뀜으로써 화면 제어의 편의성이 보장됨
    - 컴포넌트: 데이터와 화면을 하나로 묶은 덩어리
    - 데이터: state
    - 화면: render() 내의 return 부분

# JSX과 Babel

## JSX

- 자바스크립트를 확장한 문법으로 JavaScript에 XML을 추가한 문법
  - 자바스크립트에서 HTML을 작성할 수 있어서 가독성 높고 쉬움

![](https://velog.velcdn.com/images/carmine/post/f2fa4d7b-d1fb-4b9e-92b1-5a0a080d6fe5/image.png)

- 다음과 같이 스크립트 태그 내에서 HTML 태그를 사용하려면 Babel의 도움이 필요함
- Babel
  - 자바스크립트로 결과물을 만들어주는 컴파일러
  - 컴파일 시 실행됨
  - JSX가 브라우저에서 실행되기 전 Babel이 일반 자바스크립트 코드로 변환
  - 새로운 문법을 기존 브라우저에서 사용하기 위해 필요(babel-polyfill)

```jsx
<script type="text/babel">
// Babel이 해당 코드를 발견하면 아래 JSX를 컴파일할 때 다음(형광펜 강조)과 같이 변환함
```

![](https://velog.velcdn.com/images/carmine/post/9bbbaa91-e34d-441b-af59-6e80f6f032d7/image.png)

# Webpack

## Webpack이란

- Webpack
  - 모듈 번들러(Module Bundler)의 일종으로, HTML, CSS, JavaScript 등 웹 애플리케이션의 자원들을 조합하여 하나의 결과물로 만들어주는 도구
  - 실무에서 리액트를 통해 개발을 할 때에는 컴포넌트를 하나만 사용하는 경우가 거의 없으므로 여러 개의 자바스크립트 파일을 하나의 자바스크립트 파일로 합쳐주는 웹팩을 사용해야 함
    - 즉, 여러 개의 자바스크립트 파일을 하나의 파일로 합쳐서 HTML이 실행할 수 있게 하며, 최신 문법들을 오래된 브라우저에서도 작동되도록 해주는 역할
  - 웹팩은 Node(= 자바스크립트 실행기)가 실행시킴

## Webpack 설정

- 기본 원리
  - entry에 있는 파일을 읽고, 그 파일에 module을 적용한 뒤, output으로 도출

```jsx
module.exports = {
  entry: {},

  module: {},

  plugins: [],

  output: {},
}
```

- 바벨 관련 설정
  - 웹팩에도 바벨 설정을 해줘야 jsx를 처리할 수 있음
    - @babel/core: 바벨의 기본적인 구성 요소들이 들어있는 패키지
    - @babel/preset-env: 사용하는 브라우저에 맞게 최신 문법을 옛날 문법으로 바꿔줌
    - @babel/preset-react: jsx를 지원하기 위해 필요
    - babel-loader: 바벨과 웹팩을 연결

## import vs require

- import
  - ES2015 모듈 문법
  - require과 호환 가능
- require
  - 노드의 모듈 문법(common.js)
  - 노드에서는 require만 지원하므로 바벨이 import을 require로 변환함
    - 웹팩은 노드가 실행해주기 때문에 웹팩에서는 노드의 모듈 문법을 사용해야 함

```jsx
// import/export
export const hello = 'hello' // import {hello}

// require/export
exports.hello = 'hello'
const hello = require('hello')
```

# React의 Re-rendering

## Re-rendering의 발생 조건

- State가 바뀌었을 때
- Props가 바뀌었을 때
- 부모 컴포넌트가 리렌더링 되었을 때

## Class Component와 Function Component의 Re-render 방식

### Class Component

- 클래스 컴포넌트의 경우, state가 변화할 때 render() 함수 내의 내용만 재실행됨
  - 따라서, render() 함수 내에서 이벤트 실행 시 발생할 함수의 내용을 구구절절 다 적지 말고, 실행할 함수를 위에서 선언한 뒤, 그 함수명만 넣어주는 방식을 권장
    - 이유: 재랜더링 발생할 때마다 함수가 새로 생성되지 않게 하기 위함

```jsx
render() {
	return {
		<div onClick={() => {console.log('hello'); console.log('hi');}}>어쩌구저쩌구</div>
	}
} // (X)

render() {
	return {
		<div onClick={this.sayHello}>어쩌구저쩌구</div>
	}
} // (O)
```

#### render() 함수의 주의 사항

- render() 내에 setState() 사용 시 render()가 setState()를 실행시키고, setState()가 또 render()를 실행시키는 무한 반복 발생하므로 절대 금지
  - setState()가 실행되면 state가 바뀌고, state가 바뀌면 컴포넌트가 리렌더링되므로 render() 함수가 실행됨 -> 무한 반복

### Function Component

- 함수 컴포넌트의 경우, state가 변화할 때 함수 컴포넌트 전체가 재실행됨
  - 즉, 아래의 모든 내용이 재실행되는 것

![](https://velog.velcdn.com/images/carmine/post/d4a6ca34-2431-4b20-a431-f2c48fa2ef3f/image.png)

![](https://velog.velcdn.com/images/carmine/post/131af419-bab5-4ce5-b491-0d7ea71e9670/image.png)

- 해당 부분에서 setState()가 네 번 발생하므로 총 네 번 리렌더링이 일어나는가? NO!
  - state가 변할 때는 비동기적으로 한 번에 처리되기 때문에 랜더링은 한 번만 발생
  - 만약, setState가 동기적으로 처리되었다면 총 네 번 리렌더링 되었을 것

#### Lazy Init

- 함수 컴포넌트에서 useState hook을 사용할 때 기본값으로 함수를 넣을 수 있음
  - 원래 컴포넌트가 랜더링될 때 마다 컴포넌트 내 코드가 전부 재실행되는데, 이렇게 함수를 useState의 초기값으로 넣으면 해당 함수는 딱 한 번만 실행되고 재실행되지 않음
  - 해당 함수를 처음 호출했을 때의 return값이 state의 초기값으로 설정됨

```jsx
const [number, setNumber] = useState(getNumber) // lazy init
```


# React의 불변성

## 불변성이란(Immutability)

### 불변성

- 불변성
  - 메모리 영역에서 상태나 값을 변경할 수 없는 것

### JavaScript 원시 타입과 참조 타입

- 자바스크립트의 원시 타입(String, Number, Bigint, Boolean, Undefined, Symbol, Null)
  - 메모리에 고정된 크기로 데이터가 저장되며 변수에 매칭된 주소의 메모리 공간에 해당 원시 데이터의 '값'을 저장함
  - 기존 선언 및 할당된 변수의 값을 변경할 시, 변수에 매칭된 메모리 공간의 값이 a에서 b로 바뀌는 것이 아닌, 다른 메모리 공간에 b가 저장된 후, 변수가 b의 메모리 주소와 매칭되는 방식
    - 메모리 공간 내에서 값을 변경 불가능 -> 완전히 새로운 메모리 공간에 새로운 값이 저장됨
    - 기존 값인 a는 메모리 청소기인 Garbage Collector에 의해 사라짐
  - 즉, 원시 타입의 값은 변경이 불가능하며, 이를 '불변성을 유지한다'고 표현
- 자바스크립트의 참조 타입(Object, Array, Function)
  - 크기가 정해져있지 않고 변수는 해당 데이터 자체를 저장하는 것이 아니라, 변수에 매칭된 주소의 메모리 공간에 해당 데이터가 저장된 메모리 블록의 '주소'를 저장함
    - 동적으로 크기가 변하는 데이터를 보관하기 위해 데이터를 메모리에 저장한 뒤 변수에 매칭된 주소의 메모리 공간에는 데이터가 저장된 메모리 블록의 주소를 할당
  - 참조 타입의 데이터들은 변할 수 있는 값이며, 새로운 값이 만들어지지 않고 해당 데이터를 직접적으로 변경할 수 있음
  - 배열에 push() 메소드를 사용하여 값을 추가할 때, 해당 배열이 저장된 메모리 공간 내에 추가된 값이 할당된 주소가 추가되는 방식
    - 메모리 공간 내에서 값을 변경할 수 있음
  - 즉, 참조 타입의 값은 변경이 가능하며, 불변성을 유지하지 않을 수 있음

```jsx
// 원시 타입
let num = 100 // 메모리에 Number 타입의 100이라는 값이 고정된 크기로 저장되며 num이 해당 원시 데이터의 값을 보관 = 변수에 할당된 메모리 블록에 100을 저장
num = 200 // 200이라는 새로운 값을 저장할 새로운 메모리 공간 확보 후 거기에 200이 저장되며 num은 200이 저장된 메모리 공간의 주소와 재매칭됨

let copy = num // 200이라는 값 자체를 복사하여 새로운 메모리 공간에 저장한 뒤, copy는 그 메모리 공간의 주소와 매칭됨
num = 300 // 300은 새로운 메모리 공간에 저장되며 num은 그 공간의 주소와 매칭됨
console.log(copy) // copy의 값은 그대로 200

// 참조 타입
```

## 불변성을 지켜야 하는 이유

- 예를 들어, [1, 2, 3]이라는 배열이 할당된 state가 있다면, 이 배열에 4를 추가로 push하면 리액트는 해당 state의 변화를 감지하지 못함
  - 리액트는 prevState !== currentState여야 state가 바뀌었다고 판단하여 재랜더링함 -> 예전 state와 현재 state의 참조가 달라야함
  - 리액트는 객체의 속성 하나하나를 비교하지 않고 참조값만 비교함 -> push() 메소드 사용 시 state가 참조하고 있는 메모리의 주소는 변화하지 않으며, 객체 자체에 값이 추가되어 불변성 지켜지지 않음
  - 따라서 리액트는 객체의 속성이나 값을 바꾸는 것을 'state가 변화되었다'고 인지하지 못함
- 리액트는 불변성을 지켜야 하므로 객체(배열, 함수 등)를 함부로 바꾸면 안됨
  - 객체를 함부로 바꾸지 말고 복사해야 함: 객체를 바꾸지 말고 기존 객체를 복사하여 새로운 객체를 만들어서 그것을 수정한 뒤, 수정된 객체로 기존 객체를 대체해야 함 = state가 참조하고 있는 주소값 자체를 바꿔야 함
  - 따라서 배열을 직접적으로 수정하는 pop, push, shift, unshift, splice 등의 메소드들이 아닌 새로운 배열을 만들어내는 concat, slice와 같은 메소드들을 사용해야 함
  - 리액트의 state를 변경할 때에도 state에 값을 직접 할당하는 방식이 아닌, setState()를 사용해야 함

```jsx
this.state.number = 2 //(X)
this.setState({ number: 2 }) //(O)
```

[참고1](https://www.youtube.com/playlist?list=PLcqDmjxt30RtqbStQqk-eYMK8N-1SYIFn)
[참고2](https://jungwoney.tistory.com/13)
[참고3](https://velog.io/@jma1020/%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EB%B6%88%EB%B3%80%EC%84%B1%EC%9D%B4%EB%9E%80)


# React의 Life Cycle

## 개요

- 리액트의 라이프 사이클

  - 컴포넌트의 수명 주기
  - 컴포넌트의 수명: 페이지에서 렌더링되기 전 준비 과정부터 페이지에서 사라질 때까지

    - 컴포넌트가 생성될 때(mounting), 업데이트될 때(updating), 제거될 때(unmounting)

      - mount: DOM이 생성되어 웹 브라우저 상에 나타나는 것
      - unmount: DOM에서 제거되는 것

![](https://velog.velcdn.com/images/carmine/post/a00de115-71da-4892-b2b5-e6e418eac121/image.png)

## 라이프 사이클 메소드

### constructor

- 생성자
  - 컴포넌트를 만들 때 처음으로 실행되며, 클래스 컴포넌트에서 초기 state를 설정할 때 사용됨
    - 함수 컴포넌트에서는 useState hook을 사용하여 초기 state 설정

### shouldComponentUpdate

- props나 state가 변경되었을 때의 리렌더링 여부를 결정하는 메소드이며, 반드시 true나 false를 반환
  - true일 경우 렌더링 발생 / false일 경우 렌더링 발생 X
- 성능 최적화를 위한 메소드
- 필요한 이유
  - 부모 컴포넌트에서 state를 변경하였지만, 그 영향을 받지 않아도 되는 자식 컴포넌트에서도 불필요한 리렌더링이 발생하는 것을 방지
  - state가 바뀌었는지 여부와 상관없이 setState()가 호출되기만 해도 리렌더링이 일어나므로, 리액트가 제공해주는 shouldComponentUpdate 메소드를 사용하여 어떨 때에 리렌더링이 발생할 지 직접 명시해서 필요한 경우에만 리렌더링 되도록 함

```jsx
onClick = () => {
	this.setState({}); // 리렌더링 발생
}

shouldComponentUpdate(nextProps, nextState, nextContext) {
	if (this.state.number !== nextState.number) {
		return true; // 기존 state와 바뀐 state가 다르면 state가 바뀌었으므로 true를 return
	}
	return false; // 같으면 false를 return
}
```

### render

- 컴포넌트를 렌더링하는 메소드
- 함수 컴포넌트에서는 render 메소드 없이 렌더링 가능

### componentDidMount

- render()가 처음 실행되고 컴포넌트가 성공적으로 렌더되었을 때만 실행됨
  - 리렌더링 시 실행되지 않음
  - componentDidMount를 사용하여 비동기 요청 많이 일어남
- 함수 컴포넌트에서는 useEffect hook을 활용

### componentDidUpdate

- 리렌더링 완료 후 실행됨

### componentWillUnmount

- 컴포넌트가 DOM에서 제거되기 직전에 실행
  - 부모에 의해 자식 컴포넌트가 제거될 때 실행됨
  - componentDidMount, componentDidUpdate에서 등록된 이벤트, 비동기 요청 등의 정리가 일어남
    - 예를 들어, setInterval을 componentDidMount에 등록해서 처음 성공적으로 렌더링된 이후부터 반복 작업을 실행했다면 그 반복 작업은 컴포넌트가 사라졌더라도 웹 브라우저를 종료하기 전까지 계속 실행됨 = 메모리 누수 발생
    - 따라서 해당 작업을 componentWillUnmout를 통해 컴포넌트가 DOM에서 제거되기 직전에 정리해야 함

## Class Component의 라이프 사이클

### Component Mount

- constructor에 의해 state나 메소드들이 초기화 및 등록됨 -> 첫 render() 메소드 실행 -> ref를 사용할 시 ref를 설정해주는 부분이 실행됨 -> componentDidMount 메소드 실행

### State or Props 변경

- shouldComponentUpdate가 true를 반환 = 리렌더링 필요 -> render() 메소드 실행(리렌더링 발생) -> componentDidUpdate 메소드 실행

### 부모에 의해 제거됨

- 부모에 의해 컴포넌트가 제거되기 전 componentWillUnmount 메소드 실행 -> 컴포넌트 소멸(화면에서 사라짐)

## Function Component의 라이프 사이클

- 클래스 컴포넌트와의 차이점
  - 클래스 컴포넌트의 경우 componentDidMount나 componentDidUpdate에서 모든 state를 조건문으로 분기 처리함
  - 함수 컴포넌트에는 라이프 사이클이 없지만 useEffect hook을 사용하여 유사하게 구현 가능
    - useEffect 내의 콜백 함수에서 컴포넌트가 성공적으로 렌더링되었을 때와 리렌더링이 완료되었을 때 실행될 내용을 구현
    - 콜백 함수가 return하는 clean up 함수에서 컴포넌트가 DOM에서 제거되기 직전에 싱행될 내용을 구현

```jsx
useEffect(() => {
  // componentDidMount, componentDidUpdate의 역할을 수행
  return () => {
    // componentWillUnmount 역할을 수행하는 clean up 함수
  }
}, [])
```

- useEffect에서 componentDidMount 말고 componentDidUpdate만 실행하고 싶을 때 방법

```jsx
const mounted = useRef(false);
useEffect(() => {
	if (!mounted.current) {
		mounted.current = true; // do nothing (componentDidMount)
	} else {
		// do something (componentDidUpdate)
	}
}, [바뀌는 값])
```
# Ref 사용하기

## Ref란

- render 메소드에 의해 생성된 DOM 노드나 리액트 엘리먼트에 접근하는 방법을 제공
  - HTML에서 DOM 요소에 접근하여 조작할 때에는 id를 사용
  - 리액트의 경우 ref가 DOM 요소에 직접 접근하여 조작하기 위한 이름표 역할을 수행
  - 전역적으로 작동하지 않으며 컴포넌트 내부에서만 유효함

## Class Component에서의 ref 사용

### 전통적인 방식

```jsx
input;

onRefInput = (c) => { this.input = c };

render() {
	return (
		<input ref={this.onRefInput} type="text" />
	)
}
```

### 발전된 방식

- createRef()
  - 함수 컴포넌트와 유사한 방식으로 ref를 사용할 수 있는 방식 -> 더 쉽고 간단

```jsx
inputRef = createRef();

render() {
	return (
		<input ref={this.inputRef} type="text" />
	)
}
```

## Function Component에서의 ref 사용

- useRef hook
  - useRef로 관리되는 변수는 값이 바뀌어도 컴포넌트가 리렌더링 되지 않음
  - ref는 객체라서 객체의 속성이나 값이 바뀌어도 참조할 때마다 같은 메모리 주소를 가지기 때문에 리렌더링이 발생하지 않음
  - 즉, 바뀌어도 렌더링이 다시 일어나지 않기를 원하는 값들은 useRef를 사용하여 화면에 영향 끼치지 않을 수 있음

```jsx
import React, { useState, useRef } from 'react'

const Component = () => {
  const inputRef = useRef()
  const number = useRef(0) // number.current의 초기값을 0으로 설정

  const increase = () => {
    number.current += 1 // 해당 함수가 실행되어 number.current의 값이 증가해도 리렌더링 일어나지 않음
  }
  return (
    <>
      <input ref={inputRef} type="text" />
      <div onClick={() => increase()}>숫자 증가</div>
    </>
  )
}
```
# 불필요한 Re-rendering 방지

## Class Component의 Pure Component

- PureComponent
  - shouldComponentUpdate가 장착된 컴포넌트
    - props나 state가 바뀌었는지 판단하여 달라졌을 때만 자식 컴포넌트가 리렌더링되도록 함
  - 클래스 컴포넌트에서만 사용 가능

```jsx
/*
- input에 뭔가를 입력하여 value state가 달라짐 -> 리렌더링 발생
- 그러나 자식 컴포넌트인 ChildComponent의 props는 달라지지 않았음에도 불필요하게 함께 리렌더링됨 -> ChildComponent가 pureComponent로 구현되었을 경우 다음과 같은 경우에 ChildComponent의 불필요한 리렌더링 일어나지 않음
*/
return (
  <div>
    <input value={value} />
    <ChildComponent childProps={childProps} />
  </div>
)
```

## Function Component의 React.memo

- React.memo
  - 함수 컴포넌트에서는 React.memo가 PureComponent와 동일한 역할을 수행
  - React.memo가 적용된 컴포넌트는 개발자 도구에서 확인했을 때 컴포넌트의 이름이 변경되므로 displayName을 통해 이름을 명시해서 설정해줘야 함

```jsx
import React, { memo } from 'react';

const ChildComponent = memo(( {childProps} ) => {
	return (
		...
	)
})

ChildComponent.displayName = 'ChildComponent';
```
# useMemo와 useCallback을 통한 최적화

## useMemo와 useCallback의 역할

- useMemo
  - 함수의 반환값을 기억함
- useCallback
  - 함수 자체를 기억함

## useMemo를 사용하여 연산값 재사용하기

- 함수 컴포넌트는 리렌더링 시 함수 전체가 재실행되므로 컴포넌트 함수 내의 함수들도 계속 재실행됨
  - 재실행될 때마다 반환하는 값이 달라지지 않는 함수는 useMemo를 통해 함수의 반환값을 기억하기
  - 아래의 경우, input에 내용을 입력할 때마다 컴포넌트가 리렌더링 되고, 그에 따라 sayHello()가 재실행되며 콘솔에 hello가 계속 출력됨
- useMemo를 사용하면 두번째 인자인 dependency array 내의 값이 바뀌지 않는 한 콜백 함수가 다시 실행되지 않음

```jsx
import React, { useState } from 'react'

function sayHello() {
  console.log('hello')
  return 'hello'
}

const Component = () => {
  const [input, setInput] = useState('')

  const onChangeInput = (e) => {
    const { value } = e.target
    setInput(value)
  }

  const hello = sayHello()
  return (
    <>
      <div>{hello}</div>
      <input onChange={(e) => onChangeInput(e)} />
    </>
  )
}
```

![](https://velog.velcdn.com/images/carmine/post/ce685c5e-c304-46c2-bb20-15777a14933f/image.png)

```jsx
import React, { useState } from 'react'

function sayHello() {
  console.log('hello')
  return 'hello'
}

const Component = () => {
  const [input, setInput] = useState('')

  const onChangeInput = (e) => {
    const { value } = e.target
    setInput(value)
  }

  const hello = useMemo(() => sayHello(), [])

  return (
    <>
      <div>{hello}</div>
      <input onChange={(e) => onChangeInput(e)} />
    </>
  )
}
```

- useMemo를 사용하여 컴포넌트 자체를 memoization 할 수도 있음

```jsx
return (
  <>
    <div>{hello}</div>
    {dataArr.map((data) => {
      useMemo(() => <Component data={data} />, [])
    })}
  </>
)
```

- useMemo를 사용하여 컴포넌트가 리랜더링될 때 return부는 한 번만 실행되도록 할 수 있음

```jsx
return useMemo(() => <div>// ...</div>)
```

## useCallback을 사용하여 함수 재사용하기

- 함수 컴포넌트가 재실행되면 컴포넌트 내의 함수가 새로 생성됨
  - 함수 생성 자체가 오래 걸린다면 useCallback을 사용하여 함수가 새로 생성되지 않게 할 수 있음
- useCallback 내에서 사용되는 state나 props는 꼭 dependency array에 넣어줘야 함
  - 이유: 함수 내에서 해당 값들을 참조할 때 가장 최신 값을 참조할 것이라고 보장할 수 없으므로 state나 props가 바뀔 때마다 useCallback을 새로 실행해줘야 함
- 자식 컴포넌트에 props로 함수를 넘길 때에도 useCallback 사용하는 것을 권장
  - useCallback으로 감싸주지 않으면 부모 컴포넌트가 리렌더링될 때마다 해당 함수가 매번 새로 생성되며 자식 컴포넌트에 매번 새로운 함수가 전달됨 -> 함수 자체는 변한 것이 없는데 자식 컴포넌트의 불필요한 리렌더링을 발생시킴

```jsx
import React, { useState } from 'react'

function sayHello() {
  console.log('hello')
  return 'hello'
}

const Component = () => {
  const [input, setInput] = useState('')

  const onChangeInput = useCallback((e) => {
    const { value } = e.target
    setInput(value)
  }, [])

  const hello = useMemo(() => sayHello(), [])

  return (
    <>
      <div>{hello}</div>
      <input onChange={(e) => onChangeInput(e)} />
    </>
  )
}
```

# ContextAPI

## action, dispatch, reducer의 관계

### action

- action의 type은 액션의 이름, 나머지는 데이터들

```jsx
// number라는 상태를 0으로 변경하는 액션 객체이며 액션의 이름은 'SET_NUMBER'
{type: 'SET_NUMBER', number: 0}
```

### dispatch

- 액션 객체 발행

  - dispatch를 통해 액션을 실행하는 것

```jsx
const onClickButton = useCallback(() => {
  dispatch({ type: 'SET_NUMBER', number: 0 })
}, [])

return (
  <>
    <div onClick={onClickButton}></div>
  </>
)
```

### reducer

- 디스패치한 액션을 해석하여 state를 직접 변경해주는 함수
  - 디스패치 할 때마다 reducer 실행됨
  - state를 수정하기 위해서는 이벤트가 실행될 때 액션을 실행(디스패치)해서 state를 바꿔야 하며, state를 어떻게 바꿀 것인지는 reducer에 기록
- 불변성 지키기

  - 기존 state를 직접 바꾸면 안되고, 새로운 state를 만들어서 바뀔 부분만 바꿔준 뒤, 그 새로운 state로 기존 state를 대체해야 함

```jsx
const reducer = (state, action) => {
  switch (action.type) {
    case 'SET_NUMBER':
      // state.number = action.number (x)
      return {
        ...state,
        number: action.number,
      }
  }
}
```

## ContextAPI 사용하기

### 사용법

- ContextAPI에서 접근 가능한 데이터들에 접근하고자 하는 컴포넌트들을 Provider로 묶어주기
  - Provider의 value로 state와 dispatch 함수를 넣어주면 감싸진 컴포넌트들에서 사용 가능함
- 성능 최적화

  - 해당 Provider 코드가 있는 컴포넌트가 새로 리랜더링 될 떄마다 value 객체도 새로 생성됨 -> ContextAPI를 사용하는 컴포넌트들도 매번 새로 리랜더링 됨
  - 따라서 useMemo를 사용한 캐싱 필요

```jsx
const NumberContext = createContext({
  number: 0,
  dispatch: () => {},
})

const value = useMemo(() => ({ number: state.number, dispatch }), [
  state.number,
])
// dispatch 함수는 절대 바뀌지 않기 때문에 useMemo의 dependency array에 넣지 않음

return (
  <NumberContext.Provider value={value}>
    <Table />
    <Form />
  </NumberContext.Provider>
)
```

- dispatch 함수를 하위 컴포넌트에서 사용하기

  - 우선 해당 함수를 초기값으로 갑고 있는 context를 export
  - 사용하고 싶은 하위 컴포넌트 파일 내에서 import -> useContext를 사용하여 변수에 할당하기

```jsx
// app.js
export const NumberContext = createContext({
  number: 0,
  dispatch: () => {},
})

// Form.js
import { NumberContext } from './app'

const Form = () => {
  const number = useState(10)
  const value = useContext(NumberContext)

  // ...
  const onClickButton = useCallback(() => {
    dispatch({ type: SET_NUMBER, number })
  }, [number])
}
```
