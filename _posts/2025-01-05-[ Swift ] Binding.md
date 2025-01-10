---
title: "[ Swift ] Binding"
categories: [Ios , Swift ]
tags:
  [
    swift,
    ios,
    swiftUI,
    state,
    binding
  ] 
---

## 바인딩
데이터를 양뱡향으로 연결하는 메커니즘

* 부모 뷰에서 자식 뷰로 데이터를 전달하고, 자식 뷰에서 변경된 값을 다시 부모 뷰로 전달
* 보통 부모 뷰에서는 @State로 선언된 변수를 자식뷰에 Binding형태로 전달한다.

## 기본구조
```swift
import SwiftUI

struct ParentView: View {
    @State private var isOn: Bool = false

    var body: some View {
        VStack {
            Toggle("Switch", isOn: $isOn) // Binding 사용
            ChildView(isOn: $isOn)       // Binding을 자식 뷰로 전달
        }
    }
}

struct ChildView: View {
    @Binding var isOn: Bool // 부모의 State와 바인딩

    var body: some View {
        Text(isOn ? "Switch is ON" : "Switch is OFF")
    }
}

```

## 코드 흐름
1. ParentView:
* @State로 isOn 변수를 선언.
* $isOn을 사용해 Binding을 생성하고, 자식 뷰와 Toggle에 전달.

2. ChildView:
* @Binding으로 데이터를 받고, isOn을 사용해 UI를 업데이트.

3. 동작:
* Toggle을 켜거나 끌 때 isOn 값이 변경됩니다.
* 이 변경은 ParentView와 ChildView에 즉시 반영됩니다.

### 즉 언제 바인딩을 쓰냐
* 부모 뷰에서 관리하는 상태를 자식뷰에서 수정할 때
* Toggle같은 UI요소랑 데이터 모델을 연결할 때 
* 데이터가 양방향으로 흐를 필요가 있을 때 