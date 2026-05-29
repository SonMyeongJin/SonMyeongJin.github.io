---
title: "[OnBoarding] React Hooks"
categories: [Frontend, OnBoarding]
tags: [
  react,
  hooks,
  frontend,
  onboarding
]
---

# React Hooks 기본 정리

React Hooks는 함수형 컴포넌트에서 상태 관리, 값 계산, 생명주기 처리 같은 기능을 사용할 수 있게 해주는 문법이다.

처음 Hooks를 공부할 때 `useState`, `useMemo`, `useEffect`가 비슷해 보일 수 있다.
특히 `useMemo`와 `useEffect`는 둘 다 두 번째 인자로 `[]` 배열을 받기 때문에 헷갈리기 쉽다.

이번 글에서는 세 Hooks의 목적과 사용 방법을 비교해서 정리한다.

## 1. 의존성 배열이란?

`useMemo`와 `useEffect`에서 두 번째 인자로 전달하는 배열을 **의존성 배열(Dependency Array)**이라고 한다.

```tsx
useMemo(() => {
  return 계산된값;
}, [변수]);

useEffect(() => {
  실행할동작();
}, [변수]);
```

의존성 배열 안에 있는 값이 변경되면 React는 그 변화를 감지하고 함수를 다시 실행한다.

즉, 아래처럼 이해하면 된다.

```text
[변수] 안의 값이 바뀐다 → React가 감지한다 → 함수가 다시 실행된다
```

이 원리는 `useMemo`와 `useEffect` 모두 동일하다.
다만 두 Hooks의 목적이 다르다.

## 2. useState: 상태 만들기

`useState`는 컴포넌트 안에서 변하는 값을 관리할 때 사용한다.

```tsx
const [데이터, 세터함수] = useState(초기값);
```

예시 코드는 다음과 같다.

```tsx
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

### 핵심

- 상태의 시작값을 만든다.
- `setCount` 같은 세터 함수를 통해 값을 변경한다.
- 상태가 바뀌면 컴포넌트가 다시 렌더링된다.
- 의존성 배열을 사용하지 않는다.

`useState`는 무언가를 감시하는 Hook이 아니라, 컴포넌트가 기억해야 할 상태를 만드는 Hook이다.

## 3. useMemo: 값 기억하기

`useMemo`는 계산 결과를 기억해두었다가, 의존성 배열 안의 값이 바뀔 때만 다시 계산하는 Hook이다.

```tsx
const 결과값 = useMemo(() => {
  return 계산식;
}, [변수]);
```

`useMemo`는 반드시 계산된 값을 `return`하고, 그 값을 왼쪽 변수에 담아 사용한다.

```tsx
import { useMemo, useState } from "react";

function PriceCalculator() {
  const [count, setCount] = useState(1);
  const price = 1000;

  const totalPrice = useMemo(() => {
    return count * price;
  }, [count]);

  return (
    <div>
      <p>수량: {count}</p>
      <p>총 가격: {totalPrice}원</p>
      <button onClick={() => setCount(count + 1)}>수량 증가</button>
    </div>
  );
}
```

### 핵심

- 계산된 값을 기억한다.
- 의존성 배열 안의 값이 바뀌면 다시 계산한다.
- 의존성 배열 안의 값이 바뀌지 않으면 이전 계산 결과를 재사용한다.
- `const 결과값 = useMemo(...)`처럼 왼쪽에 값을 받을 변수가 있다.

## 4. useEffect: 행동 실행하기

`useEffect`는 렌더링 이후에 특정 행동을 실행할 때 사용한다.

```tsx
useEffect(() => {
  실행할동작();
}, [변수]);
```

예를 들어 상태가 바뀔 때마다 콘솔을 찍거나, 서버에서 데이터를 가져오거나, 이벤트를 등록할 때 사용할 수 있다.

```tsx
import { useEffect, useState } from "react";

function CounterLogger() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log(`count가 변경됨: ${count}`);
  }, [count]);

  return (
    <div>
      <p>현재 숫자: {count}</p>
      <button onClick={() => setCount(count + 1)}>증가</button>
    </div>
  );
}
```

### 핵심

- 특정 조건에서 행동을 실행한다.
- 의존성 배열 안의 값이 바뀌면 다시 실행된다.
- 보통 값을 리턴해서 변수에 담지 않는다.
- `const result = useEffect(...)`처럼 사용하지 않는다.

`useEffect`는 값을 계산하는 Hook이 아니라, 조건이 맞을 때 행동을 실행하는 Hook이다.

## 5. useMemo와 useEffect 비교

두 Hook은 문법이 비슷하다.

```tsx
const result = useMemo(() => {
  return value;
}, [dependency]);

useEffect(() => {
  doSomething();
}, [dependency]);
```

하지만 목적은 다르다.

| Hook | 목적 | 반환값 사용 | 의존성 배열 의미 |
| --- | --- | --- | --- |
| `useMemo` | 값을 계산하고 기억한다 | 사용한다 | 값이 바뀌면 다시 계산한다 |
| `useEffect` | 행동을 실행한다 | 보통 사용하지 않는다 | 값이 바뀌면 다시 실행한다 |

쉽게 말하면 다음과 같다.

- `useMemo`: 값을 만드는 계산기
- `useEffect`: 행동을 실행하는 실행기

## 6. 포켓몬 예시로 이해하기

아래 예시는 `useState`, `useMemo`, `useEffect`를 한 번에 비교하기 위한 코드이다.

```tsx
import { useEffect, useMemo, useState } from "react";

const Pikachu = {
  name: "피카츄",
  hp: 35,
  attack: 55,
};

function PokemonStatus() {
  // 1. 상태를 선언한다.
  const [isMegaSinka, setMegaSinka] = useState(false);
  const [hp, setHp] = useState(Pikachu.hp);

  // 2. isMegaSinka가 바뀌면 포켓몬 데이터를 새로 계산한다.
  const pokemonData = useMemo(() => {
    if (isMegaSinka) {
      return {
        ...Pikachu,
        name: "메가 피카츄",
        hp: 60,
        attack: 75,
      };
    }

    return { ...Pikachu };
  }, [isMegaSinka]);

  // 3. pokemonData가 바뀌면 hp를 다시 세팅하는 행동을 실행한다.
  useEffect(() => {
    setHp(pokemonData.hp);
  }, [pokemonData]);

  return (
    <div>
      <h2>{pokemonData.name}</h2>
      <p>HP: {hp}</p>
      <p>공격력: {pokemonData.attack}</p>

      <button onClick={() => setMegaSinka(!isMegaSinka)}>
        {isMegaSinka ? "원래대로" : "메가진화"}
      </button>
    </div>
  );
}
```

이 코드를 기준으로 보면 역할이 명확해진다.

- `useState`: `isMegaSinka`, `hp`라는 상태를 만든다.
- `useMemo`: `isMegaSinka`가 바뀌면 `pokemonData` 값을 다시 계산한다.
- `useEffect`: `pokemonData`가 바뀌면 `setHp`를 실행한다.

## 7. 의존성 배열 사용 시 주의할 점

의존성 배열에는 Hook 내부에서 사용하는 외부 값을 넣어야 한다.

```tsx
useEffect(() => {
  console.log(count);
}, [count]);
```

만약 `count`를 사용하면서 의존성 배열에 넣지 않으면, 오래된 값을 참조하는 문제가 생길 수 있다.

```tsx
// 좋지 않은 예시
useEffect(() => {
  console.log(count);
}, []);
```

반대로 의존성 배열을 생략하면 렌더링될 때마다 실행된다.

```tsx
useEffect(() => {
  console.log("렌더링될 때마다 실행");
});
```

## 8. 정리

`useState`, `useMemo`, `useEffect`는 목적이 서로 다르다.

| Hook | 사용법 | 역할 |
| --- | --- | --- |
| `useState` | `const [state, setState] = useState(초기값)` | 상태를 만든다 |
| `useMemo` | `const value = useMemo(() => 계산식, [변수])` | 값을 계산하고 기억한다 |
| `useEffect` | `useEffect(() => 실행할동작, [변수])` | 조건에 따라 행동을 실행한다 |

헷갈릴 때는 다음 기준으로 구분하면 된다.

- 화면에서 바뀌는 값을 저장해야 한다면 `useState`
- 어떤 값을 계산해서 변수에 담아야 한다면 `useMemo`
- 값이 바뀐 뒤 어떤 행동을 실행해야 한다면 `useEffect`

의존성 배열 `[]` 안의 값이 바뀌면 Hook의 함수가 다시 실행된다는 점은 `useMemo`와 `useEffect` 모두 동일하다.
다만 `useMemo`는 값을 리턴하고, `useEffect`는 행동을 실행한다는 차이가 있다.
