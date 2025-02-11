---
title: "[ Swift ] Project 생성 환경"
categories: [Ios , Swift ]
tags:
  [
    swift,
    ios,
    swiftUI
  ]
image: "/assets/img/title/swift2.png" 
---

## Testing System
![](/assets/img/testingSystem.png)
* XCTest for Unit and UI Tests
* Swift Testing with XCTest UI Tests

    둘중하나 고르면 프로젝트 파일 밑에 Test 파일 두개 생김
![](/assets/img/Testing2.png)

> ### XCTest for Unit and UI Tests
* 유닛 테스트(Unit Test)와 UI 테스트(UI Test)를 모두 수행한다는 의미
> ### Swift Testing with XCTest UI Tests
* XCTest를 사용한 UI 테스트(UI Tests)만을 강조

    * Unit Test
        * 앱의 개별 기능, 메서드, 클래스, 모듈이 올바르게 작동하는지 테스트.
        * 예: 특정 함수가 예상하는 값을 반환하는지 확인.
        * 빠르고 가볍기 때문에 코드의 논리를 검증하는 데 적합.
        * 보통 앱의 내부 로직(비즈니스 로직 등)을 검증할 때 사용.
    * UI Test
        * 사용자 인터페이스(UI)가 올바르게 작동하는지 확인.
        * 예: 버튼을 클릭하면 올바른 화면으로 전환되는지, 텍스트 입력 필드가 잘 동작하는지 등.
        * 전체 앱의 실행 흐름을 시뮬레이션하며 사용자 경험을 검증.


## Storage
![](/assets/img/storage.png)
* Swift Data
    * Item.swift 파일 생성
* Core Data 
    * persistence.swift 파일 생성
    * 프로젝트명.xcdatamodeld 파일 생성

> Core Data

* 기본 작동 방식
    * Objective-C 기반 API에서 유래한 프레임워크로, SQLite 데이터베이스를 백엔드로 사용하며, 관계형 데이터 구조를 관리하는 데 최적화되어 있습니다.
    * 프로젝트의 복잡한 데이터 모델 관리에 적합.

* persistence.swift:
    * Core Data 스택을 설정하는 파일입니다.
    * 이 파일에는 NSPersistentContainer를 설정하고 Core Data 저장소와의 상호작용을 처리하는 기본 코드가 포함됩니다.
    * 앱이 Core Data를 사용할 준비를 하는 핵심 구성 파일입니다.

* 프로젝트명.xcdatamodeld:

    * Core Data의 데이터 모델을 정의하는 파일입니다.
    * 이 파일에서 엔티티(Entity), 속성(Property), 관계(Relationship) 등을 시각적으로 정의할 수 있습니다.
    * Xcode에서 제공하는 데이터 모델 편집기를 통해 작업합니다.

> Swift Data
* 기본 작동 방식
    * SwiftData는 Swift 언어로 데이터 모델을 선언하는 최신 방식입니다.
    * Core Data의 복잡한 설정을 줄이고 Swift의 선언형 스타일에 맞게 설계되었습니다.
    * 보다 간결하고 직관적인 코드 작성을 지원하며, 데이터베이스 관리를 쉽게 할 수 있도록 개선된 API를 제공합니다.
* Item.swift:
    * SwiftData에서 데이터를 관리하기 위한 모델 정의 파일입니다.
    * 데이터 모델은 @Model 속성을 사용하여 Swift 언어로 직접 정의됩니다.

> 간단히 말하면
* Core Data:
    * 복잡한 데이터 모델을 시각적으로 정의하고 관리하려는 경우에 적합.
    * 기존 앱이나 Objective-C 기반 코드와의 호환성을 유지해야 할 때 유용.

* SwiftData:
    * Swift 언어에 최적화된 최신 방식으로, 간단한 데이터 모델을 코드로 정의하려는 경우에 적합.
    * 최신 프로젝트에서는 SwiftData가 더 간결하고 효율적일 가능성이 높습니다.

##  "host in cloud kit" 체크하면
![alt text](/assets/img/cloudkit.png)

* info.plist 파일 생성
    * CloudKit 설정에 필요한 정보파일

> CloudKit 이란
* 데이터베이스 즉,백앤드과정 필요없음 
* 앱데이터를 직접 호스팅하므로 별도의 서버 운영필요없음

* 데이터는 Container(앱의 데이터베이스 역할) 안에 저장
* public database에 대해 일정량 이상의 트래픽이 발생하면 추가요금 

### Private Database 랑 Public Database가있음
* Private Database : 사용자의 즐겨찾기, 단어장 등 개인 Icloud에 저장하고 기기간 동기화
* Public Database : 영상 리스트 , 추천데이터
