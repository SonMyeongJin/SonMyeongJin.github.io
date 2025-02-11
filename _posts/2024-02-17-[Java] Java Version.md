---
title:  "[Java] Java 버전 비교 (8,11,17,21)"
ccategories: [Backend,Java]
tags:
  [
    java,
    version
  ] 
image: "/assets/img/title/java.png" 
---

## Java 8
* 2014년 출시, LTS 버전(~2030.12 지원)
* 대규모 릴리즈, Lambda, Stream API 제공
* Optional, 새로운 날짜,시간 API 제공 (ex: LocalDateTime)
* Oracle이 Java를 인수한 후 첫번째 LTS 출시 버전

## Java 11
* 2018년 출시, LTS 버전(~2032.01 지원)
* String과 File 기능 향상
    * String: isBlank(), strip()    
    * File: writeString(), readString()
* var 키워드 사용 가능
* Open JDK와 Oracle JDK가 통합


## Java 17
* 2021년 출시, LTS 버전(~2029.09 지원)
* Spring Boot 3.x.x 버전은 JDK 17 이상 부터 지원
* Switch에 대한 패턴 매칭 (Preview), recode class도입, 텍스트 블록 기능(""" 사용)을 추가해 코드를 간결하고 효율적으로 작성할 수 있도록 도움


## Java 21
* 2023년 출시, LTS 버전(~2031.09 지원)
* Spring Boot 3.2 부터 지원
* 가상 스레드: Java 플랫폼에 경량 가상 스레드를 도입
    * 가상 스레드의 도입으로 몇 개의 운영 체제 스레드만 사용하여 수백만 개의 가상 스레드를 실행하는 것이 가능해짐. 기존 Java 코드를 수정할 필요 X
* UTF-8이 기본값으로 사용

# 버전 선택 기준
Java 버전 선택의 기준으로 들 수 있는 것들

1. Java 서포트 기간이 길어야 한다. -> 가급적 최신 LTS버전 선택

2. Spring Boot 상위 버전과 호환이 되어야 한다. -> 17 이상의 버전 선택

3. 최신 기능들을 사용하고 싶다. -> 버전 별 추가된 기능을 보고 선택

4. 마이그레이션이 수월했으면 좋겠다. -> 최신 이전 버전들 선택

>LTS와 non-LTS 버전

* LTS 버전: Long Term Support 의 약자이며 출시 후 일반적으로 8년 이라는 긴 기간동안 보안 업데이트와 버그 수정을 지원할 것임을 선언한 버전. Java 8(16년)과 Java 11(13년)은 사용자의 높은 수요로 지원 기간 연장

* non-LTS 버전: 일반적으로 6개월간 지원


> 일반 지원(General Support)과 확장 지원(Extended Support)

* 일반 지원: 소프트웨어의 주된 지원 기간으로, 정기적인 업데이트, 버그 수정, 보안 패치, 새로운 기능 추가

* 확장 지원: 일반 지원 기간 이후의 기간으로, 중요한 보안 패치와 긴급 버그 수정을 제공하지만, 새로운 기능 추가나 성능 개선은 거의 없으며, 추가 비용이 발생할 수 있음


