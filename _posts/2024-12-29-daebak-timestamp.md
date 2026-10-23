---
title: "DaeBak 타임스탬프로 영상 이동 기능 구현"
categories: [Project, DaeBak]
tags: [daebak, swiftui, youtube, troubleshooting]
redirect_from:
  - "/posts/Ios-App-timeStamp-기능/"
image: "/assets/img/posts/2024-12-29-daebak-timestamp/01-timestamp-demo.gif"
---

Script에서 타임스탬프를 누르면 해당 시간대로 유튜브 재생하는 기능을 추가

(자잘한 오류 찾고 수정하는데 6시간 걸렸다.. 이렇게 어려운 구현난이도는 아니였는데 .. ㅠㅠ)

## TroubleShooting

테스트 과정에서는 스탬프 누르면 정상적으로 youtubeView 가 이동하는걸 볼 수 있지만 실제 적용시 작동하지 않음.
디버그에서 찍히는걸 봐선 다른 youtubeView를 조작하는것 같음

<div style="display: flex; justify-content: space-around; align-items: center; width: 100%;">
  <!-- 첫 번째 이미지와 제목 -->
  <div style="text-align: center;">
    <img src="/assets/img/posts/2024-12-29-daebak-timestamp/02-test-works.gif" width="400" style="margin: 10px;" />
    <p style="font-size: 18px; font-weight: bold; margin-top: 10px;">테스트 - 작동 O</p>
  </div>

  <!-- 두 번째 이미지와 제목 -->
  <div style="text-align: center;">
    <img src="/assets/img/posts/2024-12-29-daebak-timestamp/03-actual-not-working.gif" width="400" style="margin: 10px;" />
    <p style="font-size: 18px; font-weight: bold; margin-top: 10px;">실제 - 작동 X</p>
  </div>
</div>

> 원인

DetailView 에서 YoutubeView , ScriptView를 합쳐지도록 구현해서 같은 객체를 참조하지 못하는 상태.

> 해결책 : DetailView에서 인스턴스 생성하고 하위 뷰에 뿌리기

```swift
struct DetailPage: View {
    @StateObject private var youTubePlayer = YouTubePlayer("") // YouTubePlayer 인스턴스 생성

    var body: some View {
        VStack {
            // YouTubePlayer 인스턴스를 YoutubeView에 전달
            YoutubeView(youtubeURL: script.youtube_url, youTubePlayer: youTubePlayer)
            
            // YouTubePlayer 인스턴스를 ScriptView에 전달
            ScriptView(script: script, youTubePlayer: youTubePlayer)
        }
    }
}
```
정상적으로 작동!
<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/posts/2024-12-29-daebak-timestamp/01-timestamp-demo.gif" width="400" />
</div>