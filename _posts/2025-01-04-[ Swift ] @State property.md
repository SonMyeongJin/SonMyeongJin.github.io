---
title: "[ Swift ] @State @Observable @Environment"
categories: [ios , swift ]
tags:
  [
    swift,
    ios,
    swiftUI,
    state,
    observable,
    environment
  ] 
---

SwiftUI 의 상태 프로퍼티를 사용하면 기본 데이터의 변경에 따른 처리 코드를 작성하지 않아도 뷰가 업데이트 된다.

## @State
상태에 대한 가장 기본적인 형태, 다음과같은 뷰 레이아웃의 상태를 저장하기 위해서만 사용
* 사례 : 토글 버튼 활성 여부
* 텍스트 필드 입력값
* 피커 뷰의 현재 선택

String이나 Int 값처럼 간단한 데이터 저장하기 위해 사용

* 상태 값은 해당 뷰에 속한것이라서 private 로 선언
* 상태 프로퍼티에 대한 바인딩 사용해서 조작

```swift
struct ContentView: View {
	@State private var wifiEnabled = true
    @State private var userName = ""
    
    var body: some View {

        	TextField("Enter user name", text: $userName)
    }
}
```
userName에 변화가 생길때마다 뷰 계층 구조는 SwiftUI에 의해 다시 랜더링 됨

## @Observable
* 상태 프로퍼티는 일시적이라 부모 뷰가 사라지면 그 상태도 사라짐
* 반면 observable은 다른 외부 뷰에서 접근 가능한 지속적인 데이터 
* 사례 : 여러 뷰에서 상태를 동기화(공유데이터)

## Enviroment
* 앱 전체에서의 전역상태를 참조할때 사용
* 사례 : 앱 전체 테마, 설정
* 구조 :  @Environment(어떤 클래스의 모델인지참조해줘여됨.self)

## 예제

```swift
@Observable
class ThemeModel {
    var isDarkMode = false
}
```

```swift
@Observable
class CounterModel {
    var count = 0
}
```

```swift
struct CounterView: View {
    @Environment(ThemeModel.self) var theme // 전역 상태 참조
    @Environment(CounterModel.self) var counter // 공통 데이터 참조
    @State private var showSettings = false // 로컬 상태 관리

    var body: some View {
        VStack {
            // 전역 테마 적용
            Text("Dark Mode: \(theme.isDarkMode ? "On" : "Off")")
                .padding()
                .background(theme.isDarkMode ? Color.black : Color.white)
                .foregroundColor(theme.isDarkMode ? Color.white : Color.black)

            // 공통 데이터 사용
            Text("Count: \(counter.count)")
                .font(.largeTitle)
                .padding()

            // 로컬 상태 사용
            Toggle(isOn: $showSettings) {
                Text("Show Settings")
            }
            .padding()

            // 공통 데이터 업데이트
            Button("Increment") {
                counter.count += 1
            }
            .padding()
            .background(theme.isDarkMode ? Color.gray : Color.blue)
            .foregroundColor(.white)
            .cornerRadius(10)
        }
        .padding()
    }
}

```

```swift
@main
struct MyApp: App {
    @StateObject private var themeModel = ThemeModel()
    @StateObject private var counterModel = CounterModel()

    var body: some Scene {
        WindowGroup {
            CounterView()
                .environment(themeModel) // 전역 테마 상태 주입
                .environment(counterModel) // 공통 데이터 주입
        }
    }
}

```
### 내가이해한부분
* @State는 그 뷰에서만 사용. 즉 showSettings가 바뀌면 counterView가 새로고침됨
* @Enviromnet 변수인 theme,counter는 값이 변하면 그 부분의 view만 새로고침됨. 예를 들면 Text(background(theme.isDarkMod)) 부분만.
* 근데 이 값이 변하는걸 어떻게 아냐? class 선언한 부분을 보면 @Observable을 이용하여 값을 추적하는거임.

* ### 즉, @Environment가 참조하는 클래스는 번드시 @Observable를 가지고있어야 된다

## 오류 해결 깨닳은 점
@Environment는 부모뷰에서 하위뷰로 전달됨.


```swift
@Observable
class ModelData {
    var landmarks: [Landmark] = load("landmarkData.json")
}
```

```swift
struct ContentView: View {
    var body: some View {
        LandmarkList()
    }
}

#Preview {
    ContentView()
        .environment(ModelData()) // <- 부모에서 환경변수 전해줘야 자식에서도 사용가능
}
```

```swift
struct LandmarkList: View {

    @Environment(ModelData.self) var modelData

    var body: some View {
    }
}

#Preview {
    LandmarkList()
        .environment(ModelData())
}
```
* 마지막 LandmarkList 에서 modelData는 class modelData에서 @Environment, @Observable 로 연결되어있으니까 바로 데이터를 가져온다고 생각했음.
* 오류나는 이유는 "부모 : ContentView -> 자식 : LandmarkList" 이기 때문에 ContentView에서 .environment(ModelData())를 받아와야 자식 뷰들도 ModelData 전부 사용가능임