---
title: "[Ios App] (Ver 1.1.0) sheet 팝업창"
categories: [Ios , Swift ]
tags:
  [
    swift,
    ios,
    swiftUI,
    sheet,
  ] 
image: "/assets/img/posts/post/Mar-13-2025%2022-51-59.gif"
---

# 기능 설명
DBak 서비스가 영상을 검색하는 방식이 아닌 개발자인 내가 영상을 추가하는 방식이기 때문에 `사용자가 원하는 영상을 요청할 수 있는 기능`이 필요하다고 생각

-> 사용자가 영상제목이나 YoutubeUrl을 신청하면 나의 메일로 요청을 받을 수 있는 기능

-> HomeView에서 SwiftUI의 `Sheet 팝업창` 기능을 이용하기로 결정

## 코드 방식
- ArtistListView 에서 신청하기 버튼을 만들고 @State isRequestSheetPresented 값을 boolen 값으로 sheet 창을 호출
  ```swift
  struct ArtistListView: View {
      @State private var isRequestSheetPresented: Bool = false
      var body: some View {
          NavigationView {
              VStack {
                // 다른 컴포넌트
                
                // 신청하기 버튼
              RequestButton(action: {
                      isRequestSheetPresented = true
                })
                .padding(.bottom, 20)
              }
              .globalBackground()
              .sheet(isPresented: $isRequestSheetPresented) {
                  RequestFormView()
              }
          }
      }
  }
  ```

- Sheet 창인 RequestFormView 를 만들고 MessageUI를 이용하여 메일 앱을 호출할수 있도록 구현.



![](/assets/img/posts/post/Mar-13-2025%2022-31-51.gif)


## 최종 기능 테스트

<div style="display: flex; justify-content: center; gap: 20px;">
  <div style="text-align: center;">
    <img src="/assets/img/posts/post/IMG_6096.PNG" width="200" />
    <p>신청 메세지 작성</p>
  </div>
  <div style="text-align: center;">
    <img src="/assets/img/posts/post/IMG_6097.PNG" width="200" />
    <p>메일 앱 호출 후 자동으로 입력</p>
  </div>
</div>

- 앱 내에서 작성한 요청 내용을 아이폰의 기본 Mail 앱 호출 후 자동으로 채워서 전송.

![](/assets/img/posts/post/스크린샷%202025-03-13%20오후%2011.04.08.png)
- 정상적으로 메일이 온것을 확인할 수 있다.