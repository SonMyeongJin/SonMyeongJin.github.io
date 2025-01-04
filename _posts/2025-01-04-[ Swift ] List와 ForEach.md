---
title: "[ Swift ] List와 ForEach"
categories: [swift, ios]
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
