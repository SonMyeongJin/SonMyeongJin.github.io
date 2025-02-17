---
title:  "[Swift] Swift Grammer"
categories: [Ios , Swift ]
tags:
  [
    swift,
    ios,
    if,
    3항연산자,
    반복문,
    enum,
    mvvvm
  ] 
image: "/assets/img/title/ios.png"
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

## MVVM

### MVVM의 기본 역할

* Model:
데이터 및 비즈니스 로직을 포함합니다.
예를 들어, 네트워크에서 데이터를 가져오거나 데이터베이스와 상호작용하는 역할.

* ViewModel:
View와 Model 사이의 중재자 역할.
데이터 바인딩, 상태 관리, 변환 로직을 담당합니다.
View에서 요청을 받아 Model과 상호작용하고, 그 결과를 가공하여 View에 제공합니다.

* View:
UI를 구성하는 부분입니다.
ViewModel로부터 데이터를 받아 화면에 표시합니다.
사용자의 입력 이벤트를 ViewModel에 전달합니다.