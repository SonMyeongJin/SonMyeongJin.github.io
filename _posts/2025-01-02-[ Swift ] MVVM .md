---
title:  "[swift] Swift Grammer - Day2"
categories: [swift, ios]
tags:
  [
    swift,
    ios,
    mvvm
  ] 
---

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