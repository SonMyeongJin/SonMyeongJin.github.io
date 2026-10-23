---
title: "DaeBak 화면 구조 설계 (NavigationStack)"
categories: [Project, DaeBak]
tags: [daebak, swiftui, navigation, grid]
redirect_from:
  - "/posts/Ios-App-List뷰-아키텍쳐/"
image: "/assets/img/title/ios.png"
---

###  NavigationStack 을 이용해
### ArtistListView -> ScriptListView -> Detailpage

# ArtistListView 
<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/posts/2024-12-15-daebak-view-architecture/01-artist-list-view.png" width="400" />
</div>

* Grid 를 이용해 구현
* 아이콘 마크 누르면 ScriptListView로 이동

# ScriptListView 
<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/posts/2024-12-15-daebak-view-architecture/02-script-list-view.png" width="400" />
</div>

* 썸네일과 영상제목을 동시에 호출


