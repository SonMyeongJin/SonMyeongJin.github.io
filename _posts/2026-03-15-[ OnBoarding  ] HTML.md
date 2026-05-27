---
title: "[OnBoarding] HTML"
categories: [OnBoarding, Frontend]
tags: [
  html,
  frontend,
  onboarding
]
---

# HTML 기본 정리

HTML(HyperText Markup Language)은 웹 페이지의 **구조**를 만드는 마크업 언어이다.
브라우저는 HTML 문서를 읽고 제목, 문단, 이미지, 링크, 버튼 같은 요소를 화면에 표시한다.

쉽게 말하면 HTML은 웹 페이지의 뼈대 역할을 한다.

## 1. HTML 문서 기본 구조

HTML 파일은 보통 아래와 같은 형태로 작성한다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>HTML 예제</title>
</head>
<body>
  <h1>안녕하세요</h1>
  <p>HTML로 작성한 첫 번째 문장입니다.</p>
</body>
</html>
```

### 주요 구성

- `<!DOCTYPE html>`: HTML5 문서임을 브라우저에 알려준다.
- `<html>`: HTML 문서 전체를 감싸는 태그이다.
- `<head>`: 문서 정보, 제목, 문자 인코딩 등을 작성한다.
- `<body>`: 실제 화면에 보이는 내용을 작성한다.

## 2. 자주 사용하는 태그

### 제목과 문단

```html
<h1>가장 큰 제목</h1>
<h2>두 번째 제목</h2>
<p>문단 내용입니다.</p>
```

- `<h1>` ~ `<h6>`: 제목을 표현한다.
- `<p>`: 문단을 표현한다.

### 링크와 이미지

```html
<a href="https://www.google.com">Google로 이동</a>

<img src="profile.png" alt="프로필 이미지">
```

- `<a>`: 다른 페이지로 이동하는 링크를 만든다.
- `<img>`: 이미지를 표시한다.
- `alt`: 이미지가 보이지 않을 때 대체 텍스트를 제공한다.

## 3. 리스트와 버튼 예시

```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

<button>클릭</button>
```

- `<ul>`: 순서가 없는 목록이다.
- `<li>`: 목록의 각 항목이다.
- `<button>`: 클릭 가능한 버튼을 만든다.

## 4. 정리

HTML은 웹 페이지의 구조를 담당한다.
CSS는 디자인, JavaScript는 동작을 담당하기 때문에 HTML을 먼저 이해하면 웹 개발의 흐름을 잡기 쉽다.

