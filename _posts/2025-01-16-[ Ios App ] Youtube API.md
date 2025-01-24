---
title:  "[Ios App] Youtube API "
categories: [Project, Personal]
tags:
  [ios,
  swift,
  ] 
published: true
---

유튜브 영상을 가져오는 방법으로 SwiftUI 에서 WebKit을 사용하여 구현하였더니 문제가 생겼다. 

<img src="/assets/img/webview1.png" width="400" />
<img src="/assets/img/webview2.png" width="400" />

web형식이기 떄문에 재생버튼을 누르면 전체화면으로 재생된다.
스크립트를 보면서 영상 재생을 위해서는 뷰 크기에서 그대로 재생되면서 조작이 가능해아한다. 

그래서 YouTubePlayerKit 라이브러리를 이용하기로 했다

![4](/assets/img/webview4.png)

이 라이브러리를 이용하면 

![3](/assets/img/webview3.png)


* 유튜브 플레이어 라이브러리를 사용하면 전체화면 없이 재생하면서 밑에 스크립트도 같이 볼 수 있다.