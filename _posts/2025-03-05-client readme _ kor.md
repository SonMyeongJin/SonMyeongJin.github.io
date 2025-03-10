---
title:  "[Client - Readme(KOR)] DataX Project "
categories: [Project, Personal]
tags:
  [node.js,
  vue.js,
  aws,
  ngnix,
  ] 
image: "/assets/img/title/vue.png"
---

# -- Cors error 미해결 -- 
아직 서버와 Cors error 해결이 안되어 Cors 확인 없는 브라우저에서 접속확인 가능합니다.

[ Safari 개발자 모드에서 CORS 비활성화 하는법 ]
1. 사파리(Safari) 열기
2. "개발자 모드(Developer Mode)" 활성화
    * 상단 메뉴에서 Safari → 설정(Preferences) → 고급(Advanced) 클릭
    * "메뉴 막대에서 개발자용 메뉴 보기(Show Develop menu in menu bar)" 체크
3. 개발자 메뉴에서 CORS 비활성화
    * 메뉴 바에서 "개발(Develop) → 모든 크로스 오리진 제한 비활성화(Disable Cross-Origin Restrictions)" 클릭Restrictions)" 클릭

# プロジェクトの概要
이 프로젝트는 Ruby on Rails와 Vue.js를 사용하여 구현된 블로그 플랫폼입니다. 사용자 인증, 기사 관리, 검색 필터링 등의 기능을 포함합니다.

[Server Github](https://github.com/SonMyeongJin/DataX_Project_Server-)


[배포중]
http://54.180.239.200

## 開発環境
- Development Environment: macOS
- node.js : 23.9.0
- vue.js : 3.5.13
- Deploy : AWS EC2 , ngnix

# プロジェクトのセットアップ手順

- 개발 플로우
    1. JWT 토큰 사용을 위해 Axios를 우선 설정
    2. 로그인 페이지 구현
    3. 회원가입 페이지 구현
    4. 글 작성,상세 페이지 구현
    5. 카테고리,검색을 이용한 필터링 기능 추가
    6. 글 삭제,수정 구현 ( 작성자만 삭제가능하도록 )
    7. 태그를 이용한 글 이동 구현
    8. UI 다듬기
    9. AWS,Nginx 를 통한 배포 
    10. Rails 서버와 연결

# 実装した機能の説明

- 로그인 로그아웃 상태
    - 로그인 로그아웃 상태에 따라 보여지는 화면이 다릅니다.
    - PostList 는 로그아웃상태에서도 볼수잇지만, 글 작성 페이지는 로그인상태에서만 접근가능합니다. (토큰 확인)

- 글 수정,삭제 버튼 작성자에게만 활성화
    - 로그인시 상태의 user_id 값과 글 작성자의 user_id 값이 같아야 수정,삭제 버튼이 보이도록 구현했습니다.
    - ![](/assets/img/posts/post/datax_post.jpeg)

- Category 및 검색박스로 검색기능
    - PostList 페이지에서 카테고리를 선택하면 같은 카테고리의 글들을 필터링합니다
    - 검색박스에서 검색하면 제목, 내용에 검색한 단어가 포함된 글들을 반환합니다

- 태그기능
    - PostDetail 페이지에서 태그를 누르면 같은 태그의 글들을 모아서 보여줍니다.
    - 글작성시 태그는 , 로 구분하여 서버에 배열로 요청합니다.
    ex) 태그1,태그2 -> ["태그1", "태그2"]

- 모바일버전 UI
    - 화면이 768px 이하로 작아지면 메뉴바가 모바일에 맞추어 변형됩니다.
    - ![](/assets/img/posts/post/datax_mobile.gif)
