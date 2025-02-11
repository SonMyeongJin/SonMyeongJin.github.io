---
title: "[ Swift ] List와 ForEach"
categories: [Ios , Swift ]
tags:
  [
    swift,
    ios,
    swiftUI,
    list,
    forEach
  ] 
---
# List 와 ForEach 

SwiftUI에서 데이터의 배열 목록을 보여주는 방법에는 List랑 ForEach가 있다.

이 두개의 구조체는 이니셜라이저로 data source 매개변수로 입력받는다는 특징이 있다.

예를들어
```swift
struct Coffee {

  let name: String
  var isFavorite: Bool = false
}
```

```swift
struct CoffeeListView : View {

  @State private var coffees: [Coffee] = [
    .init(name: "아메리카노")
    .init(name: "카푸치노")
    .init(name: "카라멜 마키아또")
  ]

  var body: some View{
    List(coffees) { coffee in //coffee는 상수
      
      Text(coffee.name)
      Image(systemName: coffee.isFavorite ? "빨간하트" : "빈 그림")
        .onTapGesture{
          coffee.isFavorite.toggle() // 따라서 함수호출로 변경 불가능
        }
    }
  }
}

```

![](https://miro.medium.com/v2/resize:fit:1168/format:webp/1*iCiV7IabIoiTkoi7ZrcYEg.png)

여기서 오류나는 이유는 coffee in ~ 에서 coffee가 상수라서 수정이 불가능함. 그래서 toggle함수를 호출이 불가능함

따라서 coffee를 **바인딩** 해줘야함 

coffee -> $coffee

바인딩은 List (X) ForEach (O)

```swift
var body: some View {
        List {
            // 정적 뷰
            Text("Select your favorite coffee")
                .font(.headline)

            // 동적 뷰
            ForEach($coffees) { $coffee in
                HStack {
                    Text(coffee.name)
                    Spacer()
                    Image(systemName: coffee.isFavorite ? "heart.fill" : "heart")
                        .foregroundColor(coffee.isFavorite ? .red : .gray)
                        .onTapGesture {
                            coffee.isFavorite.toggle()
                        }
                }
            }
        }
    }
```

## 정리
* List는 간단한 데이터를 나열할때 사용, 데이터 수정에는 제약
* ForEach는 더 세밀한 데이터 제어와 동적/정적 뷰 조합에 사용
* List는 바인딩 안되지만(읽기전용) , ForEach는 $로 바인딩하여 데이터 조작 ,함수호출로 상태 관리 가능(읽기/쓰기)

따라서 목록 보여주는 단순한건 List, 즐찾같은 토글은 ForEach 필요

# list 색상 입히는 법
*  Row : `.listRowBackground()`
*  Background : `.scrollContentBackground(.hidden)` 으로 기존 배경 숨기고 다시 다른 색으로 덮어씌우기

1. Row
    * list 행은 일반 background() 로 색상 수정이 안됨
      ```swift
      struct TestRow: View {

          var body: some View {
              Text("This is a row!")
              .listRowBackground(Color.green)
          }
      }
      ```
      이런식으로 `listRowBackground()` 로 수정해줘야됨 
      ```swift
      List {
          TestRow()
          TestRow()
          TestRow()
      }
      ```
2. Background
    * .scrollContentBackground(.hidden) 으로 리스트의 무적 하얀색 배경을 지우고 내가 덮어씌우고싶은 함수 호출해서 배경입히면 됨
      ```swift
      List(filteredScripts) {
      }
      .scrollContentBackground(.hidden)
      .globalBackground()
      ```
      ![](/assets/img/Feb-02-2025%2022-23-01.gif)
      