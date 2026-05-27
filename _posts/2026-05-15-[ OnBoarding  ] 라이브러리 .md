---
title: "[OnBoarding] 라이브러리"
categories: [OnBoarding, Frontend]
tags: [
  library,
  frontend,
  vanilla-extract,
  biome,
  storybook,
  vitest,
  onboarding
]
---

# 프론트엔드 라이브러리 기본 정리

프론트엔드 프로젝트에서는 화면을 만드는 코드뿐만 아니라 스타일 관리, 코드 품질 관리, 컴포넌트 문서화, 테스트를 위한 도구도 함께 사용한다.

이번 글에서는 실무 프론트엔드 프로젝트에서 자주 볼 수 있는 `vanilla-extract`, `Biome`, `Storybook`, `Vitest`에 대해 간단히 정리한다.

## 1. vanilla-extract

`vanilla-extract`는 TypeScript 기반의 **CSS-in-TypeScript** 라이브러리이다.
CSS를 `.css.ts` 파일에서 작성하고, 빌드 시점에 실제 CSS 파일로 추출한다.

즉, JavaScript 런타임에서 스타일을 계산하는 방식이 아니라 빌드할 때 CSS를 만들어내기 때문에 타입 안정성과 성능 측면에서 장점이 있다.

### 특징

- TypeScript로 스타일을 작성할 수 있다.
- 클래스 이름 충돌을 줄일 수 있다.
- 런타임이 아니라 빌드 타임에 CSS가 생성된다.
- 디자인 토큰, 테마 시스템을 구성하기 좋다.

### 예시 코드

```typescript
// button.css.ts
import { style } from "@vanilla-extract/css";

export const button = style({
  padding: "12px 16px",
  borderRadius: "8px",
  border: "none",
  backgroundColor: "#3182f6",
  color: "white",
  cursor: "pointer",
});
```

```tsx
// Button.tsx
import { button } from "./button.css";

function Button() {
  return <button className={button}>확인</button>;
}
```

## 2. Biome

`Biome`은 JavaScript와 TypeScript 코드를 위한 **포매터(Formatter)**이자 **린터(Linter)**이다.

기존에는 코드 포맷팅에 `Prettier`, 코드 검사에 `ESLint`를 함께 사용하는 경우가 많았다.
Biome은 이 기능들을 하나의 도구로 제공하는 것을 목표로 한다.

### 특징

- 코드 스타일을 자동으로 정리한다.
- 잠재적인 코드 문제를 검사한다.
- 설정이 비교적 단순하다.
- 실행 속도가 빠른 편이다.

### 명령어 예시

```bash
# 코드 포맷팅
npx biome format --write .

# 코드 검사
npx biome lint .

# 포맷팅과 린트를 함께 실행
npx biome check --write .
```

### 설정 예시

```json
{
  "formatter": {
    "enabled": true,
    "indentStyle": "space",
    "indentWidth": 2
  },
  "linter": {
    "enabled": true
  }
}
```

## 3. Storybook

`Storybook`은 UI 컴포넌트를 독립적으로 개발하고 문서화할 수 있게 도와주는 도구이다.

일반적으로 컴포넌트는 실제 페이지 안에서 확인하지만, Storybook을 사용하면 페이지와 분리된 환경에서 컴포넌트의 여러 상태를 확인할 수 있다.

### 특징

- 컴포넌트를 독립적으로 확인할 수 있다.
- 버튼, 모달, 카드 같은 UI 상태를 문서화하기 좋다.
- 디자이너, 기획자와 UI를 공유하기 쉽다.
- 컴포넌트 단위 개발에 유용하다.

### 예시 코드

```tsx
// Button.tsx
type ButtonProps = {
  label: string;
};

export function Button({ label }: ButtonProps) {
  return <button>{label}</button>;
}
```

```tsx
// Button.stories.tsx
import type { Meta, StoryObj } from "@storybook/react";
import { Button } from "./Button";

const meta = {
  title: "Components/Button",
  component: Button,
} satisfies Meta<typeof Button>;

export default meta;

type Story = StoryObj<typeof meta>;

export const Primary: Story = {
  args: {
    label: "확인",
  },
};
```

## 4. Vitest

`Vitest`는 Vite 기반의 JavaScript/TypeScript 테스트 프레임워크이다.
React, Vue 같은 프론트엔드 프로젝트에서 단위 테스트를 작성할 때 자주 사용한다.

Jest와 비슷한 문법을 사용하기 때문에 Jest를 사용해 본 경험이 있다면 비교적 쉽게 익힐 수 있다.

### 특징

- Vite 프로젝트와 잘 어울린다.
- 실행 속도가 빠른 편이다.
- Jest와 유사한 테스트 문법을 제공한다.
- TypeScript 지원이 좋다.

### 예시 코드

```typescript
// sum.ts
export function sum(a: number, b: number) {
  return a + b;
}
```

```typescript
// sum.test.ts
import { describe, expect, it } from "vitest";
import { sum } from "./sum";

describe("sum", () => {
  it("두 숫자를 더한다", () => {
    expect(sum(2, 3)).toBe(5);
  });
});
```

## 5. 네 가지 도구의 역할 비교

| 도구 | 역할 | 주로 사용하는 상황 |
| --- | --- | --- |
| `vanilla-extract` | 스타일 작성 | 타입 안정성 있는 CSS를 작성할 때 |
| `Biome` | 포맷팅, 린트 | 코드 스타일과 품질을 관리할 때 |
| `Storybook` | 컴포넌트 문서화 | UI 컴포넌트를 독립적으로 확인할 때 |
| `Vitest` | 테스트 | 함수나 컴포넌트 동작을 검증할 때 |

## 6. 정리

`vanilla-extract`, `Biome`, `Storybook`, `Vitest`는 각각 담당하는 역할이 다르다.

- `vanilla-extract`는 스타일을 타입 안전하게 관리한다.
- `Biome`은 코드 포맷팅과 린트를 담당한다.
- `Storybook`은 UI 컴포넌트를 독립적으로 개발하고 문서화한다.
- `Vitest`는 코드가 의도대로 동작하는지 테스트한다.

이 도구들을 함께 사용하면 프론트엔드 프로젝트의 코드 품질, UI 관리, 테스트 안정성을 높일 수 있다.
