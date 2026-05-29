---
title: "[OnBoarding] React"
categories: [Frontend, OnBoarding]
tags: [
  react,
  frontend,
  onboarding
]
---

# React 기본 정리

React는 사용자 인터페이스(UI)를 만들기 위한 JavaScript 라이브러리이다.
화면을 여러 개의 **컴포넌트**로 나누어 관리할 수 있어 재사용성과 유지보수성이 좋다.

## 1. React의 핵심 개념

React에서 중요한 개념은 다음과 같다.

- `Component`: 화면을 구성하는 독립적인 UI 조각
- `JSX`: JavaScript 안에서 HTML처럼 작성하는 문법
- `props`: 부모 컴포넌트가 자식 컴포넌트에게 전달하는 값
- `state`: 컴포넌트 내부에서 관리하는 변경 가능한 값

## 2. 컴포넌트 예시

React 컴포넌트는 보통 함수 형태로 작성한다.

```jsx
function Hello() {
  return <h1>안녕하세요 React!</h1>;
}

export default Hello;
```

컴포넌트는 다른 컴포넌트에서 태그처럼 사용할 수 있다.

```jsx
function App() {
  return (
	<div>
	  <Hello />
	</div>
  );
}
```

## 3. JSX

JSX는 JavaScript 코드 안에서 UI 구조를 표현하는 문법이다.

```jsx
const name = "React";

function Title() {
  return <h1>{name} 학습하기</h1>;
}
```

JSX에서는 JavaScript 값을 `{}` 안에 넣어 사용할 수 있다.

## 4. props 예시

`props`는 컴포넌트에 데이터를 전달할 때 사용한다.

```jsx
function UserCard(props) {
  return (
	<div>
	  <h2>{props.name}</h2>
	  <p>{props.job}</p>
	</div>
  );
}

function App() {
  return <UserCard name="민수" job="Frontend Developer" />;
}
```

구조 분해 할당을 사용하면 더 깔끔하게 작성할 수 있다.

```jsx
function UserCard({ name, job }) {
  return (
	<div>
	  <h2>{name}</h2>
	  <p>{job}</p>
	</div>
  );
}
```

## 5. state 예시

`state`는 화면에서 변경되는 값을 관리할 때 사용한다.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
	<div>
	  <p>현재 숫자: {count}</p>
	  <button onClick={() => setCount(count + 1)}>증가</button>
	</div>
  );
}
```

버튼을 클릭하면 `setCount`가 실행되고, 값이 변경되면서 화면도 다시 렌더링된다.

## 6. 정리

React는 컴포넌트 단위로 UI를 만들고, 데이터 변화에 따라 화면을 효율적으로 업데이트한다.
처음에는 컴포넌트, JSX, props, state를 중심으로 익히면 React의 기본 흐름을 이해하기 쉽다.

