---
title: "[Swift] List와 VStack"
categories: [Ios , Swift ]
tags:
  [
    swift,
    ios,
    swiftUI,
    list,
    vstack
  ] 
image: "/assets/img/title/swift2.png"
---

## List 와 VStack 의 차이

|특징|List|VStack|
|------|---|---|
|주된목적|데이터 목록 표시|뷰를 세로로 정렬|
|동적 데이터 지원|지원(배열자동생성)| X|
|스크롤 가능|기본 제공|X (ScrollView필요)|
|항목 간 구분선|O|X|
|편집 기능|O (삭제, 이동 등)|X|
|레이아웃 유연성|데이터 중심|고정된 뷰 배치|

* VStack : View 쌓기
* List : 데이터 목록으로 보여줄 때