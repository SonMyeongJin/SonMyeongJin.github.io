---
title: "[ Swift ] SwiftUI"
categories: [Ios , Swift ]
tags:
  [
    swift,
    ios,
    List,
  ] 
image: "/assets/img/title/swift2.png"
---

## List

* 일단 SwiftUI에서 List는 View를 여러개 반환함

### 정적리스트

```swift
struct FamilyRow: View {
  var name: String
  
  var body: some View {
    Text("Family: \(name)")
  }
}

struct ContentView: View {
  var body: some View {
    List {
      FamilyRow(name: "A")
      FamilyRow(name: "B")
      FamilyRow(name: "C")
    }
  }
}
```

### 동적리스트

```swift
struct Fruit: Identifiable {
    let id = UUID() // 고유 ID
    var name: String
}

struct FruitListView: View {
    
    let fruits = [
        Fruit(name: "Apple"),
        Fruit(name: "Banana"),
        Fruit(name: "Cherry")
    ]

    var body: some View {
        List(fruits , id) { fruit in
            Text(fruit.name)
        }
    }
}
```

* 리스트 괄호안에 있는 fruits는 배열
* 그 다음 옆에 fruit는 배열에 들어가는 매개변수 한 개 의 변수이름
* 다음줄은 매개변수이름을 이용한 실행문작성

* 여기서 fruits 배열은 리스트로 뽑아낼려면 id값이 있어야 구분이가능한데 배열선언할때 Identifiable 이 프로토콜 상속받으면 id 지정안해줘도 됨.