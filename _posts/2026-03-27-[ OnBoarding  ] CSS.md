---
title: "[OnBoarding] CSS"
categories: [OnBoarding, Frontend]
tags: [
  css,
  frontend,
  onboarding
]
---

# CSS 기본 정리

CSS(Cascading Style Sheets)는 HTML 요소에 **디자인과 레이아웃**을 적용하는 스타일 언어이다.
HTML이 웹 페이지의 구조를 만든다면, CSS는 색상, 크기, 간격, 배치 등을 담당한다.

## 1. CSS 작성 방법

CSS는 HTML 안에 직접 작성할 수도 있고, 별도의 `.css` 파일로 분리해서 작성할 수도 있다.

### HTML에서 CSS 파일 연결하기

```html
<link rel="stylesheet" href="style.css">
```

### CSS 예시

```css
h1 {
  color: blue;
  font-size: 32px;
}

p {
  color: #333;
  line-height: 1.6;
}
```

## 2. 선택자

선택자는 어떤 HTML 요소에 스타일을 적용할지 정하는 문법이다.

```css
/* 태그 선택자 */
p {
  color: gray;
}

/* 클래스 선택자 */
.title {
  font-weight: bold;
}

/* 아이디 선택자 */
#main {
  width: 800px;
}
```

```html
<h1 class="title">제목</h1>
<main id="main">
  <p>본문입니다.</p>
</main>
```

## 3. 박스 모델

HTML 요소는 화면에서 하나의 박스처럼 취급된다.

```css
.card {
  width: 300px;
  padding: 20px;
  border: 1px solid #ddd;
  margin: 16px;
}
```

- `width`: 요소의 너비
- `padding`: 내용과 테두리 사이의 여백
- `border`: 테두리
- `margin`: 요소 바깥쪽 여백

## 4. 간단한 카드 UI 예시

```html
<div class="card">
  <h2>CSS Card</h2>
  <p>CSS로 간단한 카드 디자인을 만들 수 있습니다.</p>
</div>
```

```css
.card {
  width: 280px;
  padding: 20px;
  border-radius: 12px;
  background-color: #f8f9fa;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.card h2 {
  margin-top: 0;
  color: #222;
}
```

## 5. 정리

CSS는 웹 페이지를 보기 좋게 만들고, 사용자가 편하게 볼 수 있도록 배치하는 역할을 한다.
기본 선택자, 박스 모델, 색상과 간격 속성부터 익히면 실제 화면을 빠르게 구성할 수 있다.

