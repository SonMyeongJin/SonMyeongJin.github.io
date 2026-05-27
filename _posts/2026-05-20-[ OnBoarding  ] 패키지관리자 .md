---
title: "[OnBoarding] 패키지 관리자"
categories: [OnBoarding, CS]
tags: [
  package-manager,
  npm,
  cs,
  onboarding
]
---

# 패키지 관리자 기본 정리

패키지 관리자(Package Manager)는 프로젝트에서 사용하는 라이브러리와 도구를 **설치, 삭제, 업데이트, 관리**해주는 프로그램이다.

개발을 하다 보면 외부 라이브러리를 자주 사용하게 되는데, 패키지 관리자를 사용하면 필요한 의존성을 쉽게 관리할 수 있다.

## 1. 패키지란?

패키지는 재사용할 수 있도록 배포되는 코드 묶음이다.
라이브러리, 프레임워크, 개발 도구 등이 패키지 형태로 제공될 수 있다.

예를 들어 JavaScript 생태계에서는 다음과 같은 패키지를 사용할 수 있다.

- `react`: UI 라이브러리
- `axios`: HTTP 요청 라이브러리
- `vite`: 프론트엔드 개발 도구
- `eslint`: 코드 스타일 검사 도구

## 2. 패키지 관리자가 필요한 이유

패키지 관리자는 다음과 같은 일을 도와준다.

- 필요한 패키지를 설치한다.
- 사용하지 않는 패키지를 삭제한다.
- 패키지 버전을 관리한다.
- 프로젝트가 어떤 패키지에 의존하는지 기록한다.
- 다른 개발자도 같은 환경을 쉽게 구성할 수 있게 한다.

## 3. JavaScript의 패키지 관리자

JavaScript에서는 대표적으로 아래 패키지 관리자를 많이 사용한다.

- `npm`: Node.js를 설치하면 함께 제공되는 기본 패키지 관리자
- `yarn`: 빠른 설치와 안정적인 의존성 관리를 목적으로 만들어진 패키지 관리자
- `pnpm`: 디스크 공간을 효율적으로 사용하는 패키지 관리자

## 4. npm 사용 예시

### 프로젝트 초기화

```bash
npm init -y
```

위 명령어를 실행하면 `package.json` 파일이 생성된다.

### 패키지 설치

```bash
npm install axios
```

설치한 패키지는 `package.json`의 `dependencies`에 기록된다.

### 개발용 패키지 설치

```bash
npm install eslint --save-dev
```

개발 중에만 필요한 패키지는 `devDependencies`에 기록된다.

### 패키지 삭제

```bash
npm uninstall axios
```

## 5. package.json 예시

`package.json`은 프로젝트 정보와 의존성을 관리하는 파일이다.

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "scripts": {
	"start": "vite",
	"build": "vite build"
  },
  "dependencies": {
	"axios": "^1.6.0",
	"react": "^18.2.0"
  },
  "devDependencies": {
	"vite": "^5.0.0"
  }
}
```

### 주요 항목

- `scripts`: 자주 사용하는 명령어를 등록한다.
- `dependencies`: 실제 실행에 필요한 패키지 목록이다.
- `devDependencies`: 개발할 때만 필요한 패키지 목록이다.

## 6. package-lock.json이란?

`package-lock.json`은 설치된 패키지의 정확한 버전을 기록하는 파일이다.

같은 `package.json`이 있어도 설치 시점에 따라 세부 버전이 달라질 수 있는데, `package-lock.json`을 사용하면 다른 환경에서도 동일한 버전의 패키지를 설치할 수 있다.

## 7. 정리

패키지 관리자는 프로젝트의 외부 의존성을 관리하는 중요한 도구이다.
특히 협업 프로젝트에서는 `package.json`과 lock 파일을 통해 같은 개발 환경을 맞추는 것이 중요하다.
