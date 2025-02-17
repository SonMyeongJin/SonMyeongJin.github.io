---
title:  "[Ios App] [Server] S3 버킷 저장방식 "
categories: [Project, Personal]
tags:
  [ios,
  spring,
  java,
  S3,
  aws
  ] 
image: "/assets/img/title/s3.png"
---

>> 아티스트명.json 으로 구현 시

json 파일을 BTS.json ASTRO.json 이런식으로 저장하니까 스크립트를 불러올 때 시간이 너무 걸림

따라서 영상 별로 json 파일을 분리하기로 함.

>> 영상한개.json 으로 구현 시

근데 이러면 영상List 불러올 때 문제가 생김.
목록은 아티스트별로 제목과 썸네일만 가져와야 하는데

```json
{
   "title": "Test Video4",
    "artist": "BTS"
}
```
이런식으로 artist 를 필터링해서 찾아오면 한번 호출할 때마다 S3에 있는 모든 json을 읽어와야함

## 종합적으로 고민해서 찾아낸 해결방안 

파일명을 BTS_Test1.json, BTS_Test2.json 이런식으로 구현하고 파일명 앞에 아티스트명_ 으로 필터링해서 목록을 보여주면 될것같음.

```
BTS_Test1.json
BTS_Test2.json
BLACKPINK_Test1.json
BLACKPINK_Test2.json
```

이렇게하면 

* 특정 아티스트 데이터만 로드하므로 속도 개선
* 영상 한개씩 호출하므로 DetailPageView에서도 로딩속도 개선

<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/스크린샷 2025-02-11 오전 2.58.13.png" width="400" />
</div>

* S3에 Artistname _ file.json 형식으로 저장
* 앞에 Artistname 부분이 필터링 조건부분


<div style="display: flex; justify-content: space-around; align-items: center; width: 100%;">
  <!-- 첫 번째 이미지와 제목 -->
  <div style="text-align: center;">
     <img src="/assets/img/스크린샷 2025-02-11 오전 2.59.26.png" width="400" style="margin: 10px;" />
    <p style="font-size: 18px; font-weight: bold; margin-top: 10px;">DetailScript 요청시</p>
  </div>

  <!-- 두 번째 이미지와 제목 -->
  <div style="text-align: center;">
     <img src="/assets/img/스크린샷 2025-02-11 오전 3.00.43.png" width="400" style="margin: 10px;" />
    <p style="font-size: 18px; font-weight: bold; margin-top: 10px;">List 요청시</p>
  </div>
</div>