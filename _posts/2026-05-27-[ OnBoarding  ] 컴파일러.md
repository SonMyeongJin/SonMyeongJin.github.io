---
title: "[OnBoarding] 컴파일러"
categories: [OnBoarding, CS]
tags: [
  compiler,
  cs,
  onboarding
]
---

# 컴파일러 기본 정리

컴파일러(Compiler)는 사람이 작성한 소스 코드를 컴퓨터가 이해할 수 있는 형태로 변환해주는 프로그램이다.

개발자는 Java, C, TypeScript 같은 언어로 코드를 작성하지만, 컴퓨터는 이 코드를 그대로 이해하지 못한다.
그래서 컴파일러가 코드를 분석하고 실행 가능한 형태 또는 다른 언어의 코드로 변환한다.

## 1. 컴파일이란?

컴파일(Compile)은 소스 코드를 다른 형태의 코드로 변환하는 과정이다.

예를 들어 Java 코드는 컴파일을 거쳐 바이트코드(`.class`)가 되고, TypeScript 코드는 JavaScript 코드로 변환된다.

```text
소스 코드 → 컴파일러 → 실행 가능한 코드 또는 변환된 코드
```

## 2. 컴파일러가 하는 일

컴파일러는 보통 다음과 같은 작업을 수행한다.

- 문법이 올바른지 검사한다.
- 변수나 함수 사용이 맞는지 확인한다.
- 코드를 더 효율적인 형태로 최적화한다.
- 컴퓨터나 실행 환경이 이해할 수 있는 코드로 변환한다.

컴파일 단계에서 오류가 발견되면 실행 전에 문제를 알 수 있다.

## 3. Java 컴파일 예시

아래는 간단한 Java 코드이다.

```java
public class Main {
  public static void main(String[] args) {
	System.out.println("Hello Compiler!");
  }
}
```

Java 파일을 컴파일하면 `.class` 파일이 생성된다.

```bash
javac Main.java
java Main
```

실행 흐름은 다음과 같다.

```text
Main.java → javac → Main.class → JVM에서 실행
```

## 4. TypeScript 컴파일 예시

TypeScript는 JavaScript에 타입 문법을 추가한 언어이다.
브라우저는 TypeScript를 직접 실행하지 못하기 때문에 JavaScript로 변환해야 한다.

```typescript
const message: string = "Hello TypeScript";
console.log(message);
```

컴파일하면 타입 정보가 제거된 JavaScript 코드가 만들어진다.

```javascript
const message = "Hello TypeScript";
console.log(message);
```

## 5. 컴파일러와 인터프리터의 차이

컴파일러와 인터프리터는 모두 코드를 실행하기 위해 사용되지만 방식이 다르다.

### 컴파일러

소스 코드를 실행 전에 한 번에 변환한다.

- 실행 전에 오류를 찾기 쉽다.
- 컴파일 결과물이 따로 생성될 수 있다.
- 대표 언어: C, Java, TypeScript

### 인터프리터

소스 코드를 한 줄씩 읽고 바로 실행한다.

- 실행 과정이 비교적 간단하다.
- 코드를 바로 실행하며 테스트하기 쉽다.
- 대표 언어: Python, JavaScript

## 6. 정리

컴파일러는 개발자가 작성한 코드를 실행 환경이 이해할 수 있는 형태로 변환하는 도구이다.
컴파일 과정을 이해하면 에러 메시지를 해석하거나 빌드 과정을 파악하는 데 도움이 된다.
