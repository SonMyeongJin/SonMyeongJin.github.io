---
title: "[ Swift ] Dictionary"
categories: [ios , swift ]
tags:
  [
    swift,
    ios,
    dictionary
  ] 
---

자바의 Map 배열과 유사
* key 와 value 로 데이터를 저장

|특징|Swift Dictionary|Java Map|
|------|---|---|
|키-값 쌍 저장|Dictionary<Key, Value>|Map<Key, Value>|
|키는 고유|중복 불가|중복 불가|
|값 중복 가능|가능|가능|
|값 접근|dict[key]|map.get(key)|
|값 변경|dict[key] = newValue|map.put(key, value)|

1. 딕셔너리 생성
```swift
var fruits: [String: Int] = [
    "Apple": 3,
    "Banana": 5,
    "Cherry": 7
]
```
* key : String 타입
* value : Int 타입

2. 값 읽기
```swift
let appleCount = fruits["Apple"] // Optional(3)
print(appleCount)                // 출력: Optional(3)
print(appleCount!)               // 출력: 3 (강제 언래핑)
```
* 값 날것그대로 가져오려면 !로 언래핑해서 가져오기

3. 값 추가 및 수정
```swift
fruits["Orange"] = 4 // 키 "Orange"와 값 4 추가
fruits["Banana"] = 10 // 키 "Banana"의 값을 10으로 수정
```

4. key와 value 반복문
```swift
for (key, value) in fruits {
    print("\(key): \(value)")
}
// 출력:
// Apple: 3
// Banana: 10
// Orange: 4
```

### 반환값이 옵셔널인 이유
```swift
let unknown = fruits["Pineapple"] // nil
```
key가 존재하지 않는 값일 수 있기 때문에

# Grouping Dictionary

일반 Dictionary와 key,Value 로 저장한다는것은 같지만 생성 방법, 구조 가 다름 (다른 배열이라 생각하자)

### 구조

```swift
Dictionary(grouping: <배열>, by: { <기준 클로저> })
```

예제
```swift
let fruits = [
    "Apple",
    "Banana",
    "Cherry",
    "Blueberry",
    "Avocado"
]
// 일 때 

let groupedFruits = Dictionary(grouping: fruits, by: { $0.first! })
// $0.first!는 각 문자열의 첫 글자를 기준으로 그룹화
```

```swift
[
    "A": ["Apple", "Avocado"],
    "B": ["Banana", "Blueberry"],
    "C": ["Cherry"]
]
// A,B,C가 key , []이 value
```
