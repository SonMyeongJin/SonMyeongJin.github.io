---
title: "[OnBoarding] JavaScript"
categories: [OnBoarding, Frontend]
tags: [
  javascript,
  frontend,
  onboarding
]
---

# JavaScript 기본 정리

JavaScript는 웹 페이지에 **동작**을 추가하는 프로그래밍 언어이다.
HTML이 구조, CSS가 디자인을 담당한다면 JavaScript는 클릭 이벤트, 데이터 처리, 화면 변경 같은 기능을 담당한다.

## 1. JavaScript 사용 방법

HTML 파일에서 JavaScript 파일을 연결할 수 있다.

```html
<script src="app.js"></script>
```

간단한 코드는 HTML 안에 직접 작성할 수도 있다.

```html
<script>
  console.log("Hello JavaScript!");
</script>
```

## 2. 변수

변수는 데이터를 저장하는 공간이다.

```javascript
const name = "Son";
let age = 20;

console.log(name);
console.log(age);
```

- `const`: 다시 할당하지 않는 값에 사용한다.
- `let`: 값이 변경될 수 있을 때 사용한다.

## 3. 함수

함수는 특정 동작을 재사용하기 위해 만든 코드 묶음이다.

```javascript
function greeting(name) {
  return `안녕하세요, ${name}님!`;
}

console.log(greeting("민수"));
```

화살표 함수로도 작성할 수 있다.

```javascript
const add = (a, b) => {
  return a + b;
};

console.log(add(3, 5));
```

## 4. 조건문

조건에 따라 다른 코드를 실행할 수 있다.

```javascript
const score = 85;

if (score >= 90) {
  console.log("A");
} else if (score >= 80) {
  console.log("B");
} else {
  console.log("C");
}
```

## 5. DOM 조작 예시

JavaScript는 HTML 요소를 선택하고 내용을 바꿀 수 있다.

```html
<h1 id="title">Hello</h1>
<button id="changeButton">변경</button>
```

```javascript
const title = document.querySelector("#title");
const button = document.querySelector("#changeButton");

button.addEventListener("click", () => {
  title.textContent = "JavaScript로 변경했습니다!";
});
```

## 6. 정리

JavaScript는 웹 페이지를 정적인 문서에서 동적인 애플리케이션으로 만들어준다.
처음에는 변수, 함수, 조건문, 반복문, DOM 조작 순서로 학습하면 좋다.

