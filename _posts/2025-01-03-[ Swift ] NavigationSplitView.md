---
layout: archive
title:  "[swift] SwftUI - NavigationSplitView"
author_profile: true
---

![](이미지_소스_URL)

## NavigationSplitView

* 자주 보이는 목록같은 뷰 만들 때 쓰는거

### UI 예시
* 아이패드
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsJrEf%2Fbtsp8zivrj1%2FMdvxAJkbhan8rjkElFkZH0%2Fimg.png)

* 아이폰
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdNSsaU%2Fbtsp6qNw5CY%2FV731k8g2R8FNVMRtxYDkT0%2Fimg.png)

* 맥북
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoLOEx%2Fbtsp35iovrL%2FdzwiTDVIC107yTyq98U3S0%2Fimg.png)

### 코드구조
```swift
 NavigationSplitView(columnVisibility: $visibility, 
                            preferredCompactColumn: $columns) {
             // 사이드 바 영역
        } content: {
             // 컨텐트 영역
        } detail: {
             // 디테일 영역
        }
```