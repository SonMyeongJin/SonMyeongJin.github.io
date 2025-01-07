---
title:  "[ios] Swift Grammer - Day1"
categories: [swift, ios]
tags:
  [
    swift,
    ios,
    if,
    3항연산자,
    반복문,
    enum
  ] 
---

* ; 세미클론 생략가능 
* var : 변수 , let : 상수
* print(" \\(변수)") : 따옴표 안에서 string 이 아닌 변수로 인식

### if문
```swift
if (조건) {
    참
} else{
    거짓
}
```
```swift
if (isDarkMode == true) {
    print("다크모드 입니다.")
} else {
    print("다크모드 아닙니다.")
}
```
* 조건문 부분은 괄호 생략가능




### 3항연산자
```swift
var 변수명 : 조건 ? 참 : 거짓
```
```swift
var title : String = isDarkMode == true ? "다크모드 입니다" : "다크모드가 아닙니다."
var title2 : String = isDarkMode ? "다크모드 입니다" : "다크모드가 아닙니다."
var title3 : String = !isDarkMode ? "다크모드가 아닙니다." : "다크모드 입니다"
```

### 반복문
```swift
for 변수명 in 콜렉션 where 조건 {
    실행문
}
```

```swift
for i in 0...<5 where 조건 {
    실행문
}
```
* i 사용하지 않을땐 _ 쓰면 됨

### enum
```swift
enum School {
    case elementary
    case middle
    case high
    또는
    case elementary, middle, high
}

- 타입 지정도 가능
enum Grade : Int {
    case first = 1
    case second = 2
}

- 매개변수 받기도 가능
enum School {
    case elementary(name: String)
    case middle(name: String)
    case high(name: String)
}
```