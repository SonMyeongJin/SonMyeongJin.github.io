---
title:  "[Ios App] [Server] 서버 설계"
categories: [Project, Personal]
tags:
  [ios,
  spring,
  java
  ] 
image: "/assets/img/title/ios.png"
---

## 기본 구조
* 스크립트 목록 매일 업데이트 해야하므로 서버 개별 운영
* 서버는 Java `SpringBoot` 사용
* Http 방식으로 JSON 파일로 주고받을것임

## 데이터베이스
따로 Mysql같은 DB 운영 보다는 `AWS의 S3` 를 사용해서 .json 파일 저장/불러오기

> ✅ S3에 JSON 파일 저장 방식의 장점
* 서버 부하 감소 → DB 대신 S3에서 파일을 가져오므로 서버 부담이 적음
* 비용 절감 → DB를 운영하는 것보다 S3에 JSON 파일을 저장하는 게 저렴할 수 있음
* 확장성 → JSON 파일을 업데이트하기 쉽고, CDN과 연계하면 빠른 배포 가능
* 캐싱 가능 → CloudFront 같은 CDN을 활용하면 JSON 데이터를 캐싱하여 성능 향상

> ❌ S3 방식의 단점
* 파일 업데이트 어려움 → 새로운 데이터를 추가할 때 JSON 파일을 직접 수정해야 함
* 검색 성능 저하 → 특정 조건으로 데이터를 검색하려면 전체 파일을 불러와야 함
* 데이터 변경 반영 속도 → 실시간으로 데이터가 자주 바뀌면 S3에서 매번 불러오는 게 비효율적
* ACID 보장 어려움 → DB와 다르게 동시 업데이트 시 충돌 해결이 어려울 수 있음

따라서 내 App은 이와같은 이유로 DB 보다 `AWS S3`를 이용할 것이다. 
* 데이터 변경이 적고, 정적인 데이터 제공이 목적임
* 실시간 검색, 사용자 맞춤 데이터 제공 같은 구현을 안함
* 데이터 한번 저장하면 수정할 일이 없음

## Request - Response

* URL 을 통한 Get 방식으로 요청
* JSON 형식으로 응답

    > ### ScriptListView 
    |요청|응답|
    |------|---|
    |GET /api/list/BTS|[{ "title": "Test Video1", "artist": "BTS", "youtube_url": "..." }, { "title": "Test Video2", "artist": "BTS", "youtube_url": "..." }]|

    
    > ### DetailPageView
    
    |요청|응답|
    |------|---|
    |GET /api/script/json?fileName=BTS_test1.json|{ "title": "Test Video1", "artist": "BTS", "youtube_url": "...", "script_KOR": "...", "script_JPN": "..." }|