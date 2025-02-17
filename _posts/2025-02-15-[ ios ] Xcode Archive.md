---
title:  "[Ios] Xcode Archive"
categories: [Ios , Release]
tags:
  [
    swift,
    ios,
    release,
    archive,
    xcode
    ] 
image: "/assets/img/title/store.png"
---

앱스토어 커넥트에서 신규앱 생성을 마쳤다면, 실제 개발해놓은 프로젝트를 열어 Archive를 해보겠습니다.

1. 프로젝트를 열어 Signing & Capabilities 탭에서 Automatically manage signing 을 체크하면 자동으로 프로비저닝 프로파일이 연결된다.

    아마도 자동적으로 체크되어 있을 것이다. 혹시 안되거나 수동으로 하고 싶다면 체크를 해제하여 Provisioning Profile을 등록해주면 된다.

    ![](/assets/img/posts/post/스크린샷%202025-02-17%20오후%202.08.45.png)

2. Xcode 를 킨 상태에서 바탕화면의 맨 위 상단 메뉴 중 Product > Archive 를 선택한다.
![](/assets/img/posts/post/스크린샷%202025-02-17%20오후%202.08.53.png)

3. 아래 화면이 나오면 본인의 앱을 선택하고 'Distribute App'을 클릭한다.
![](/assets/img/posts/post/스크린샷%202025-02-17%20오후%201.57.10.png)

4. 앱스토어 배포용인 App Store Connect 선택
![](/assets/img/posts/post/스크린샷%202025-02-17%20오후%201.57.19.png)

5. 이 단계까지 완료가 되어야 앱스토어에 정상적으로 올라간 것이다.
![](/assets/img/posts/post/스크린샷%202025-02-17%20오후%202.07.48.png)

6. 앱 업로드에 성공했다면 App Store Connect 에 앱 빌드 버전이 올라와 있을 것이다.
    (약 30분 내외의 시간이 소요되는 듯 하다. 올라가면 이메일이 와있다.)
![](/assets/img/posts/post/스크린샷%202025-02-17%20오후%202.08.07.png)




