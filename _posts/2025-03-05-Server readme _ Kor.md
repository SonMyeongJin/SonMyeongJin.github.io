# プロジェクトの概要
이 프로젝트는 Ruby on Rails와 Vue.js를 사용하여 구현된 블로그 플랫폼입니다. 사용자 인증, 기사 관리, 검색 필터링 등의 기능을 포함합니다.

[Client Github](https://github.com/SonMyeongJin/DataX_Project_Client)

[API 방식으로 배포중]
http://43.203.118.99:3000/
- HTTP 방식으로 요청을 받으면 HTTP Body에 JSON형식으로 담아서 응답한다.

## 開発環境
- Development Environment: macOS
- ruby 3.2.6
- Rails 7.2.2.1
- Database: Mysql  9.2.0 
- Deploy : AWS EC2

# プロジェクトのセットアップ手順

- 프로젝트 환경 설치
    - Ruby 3.2.6 설치
    - Bundler 설치
    - 데이터베이스(MySQL) 설치
    - Rails 설치

- 개발 플로우
    1. ERD 작성
        - ![](/assets/img/posts/post/datax_erd.png)
    2. Mysql을 통한 Rails 프로젝트와 DB 연결
    3. ERD 데이터의 Model 작성 ( 속성값 )
    5. API명세서 작성
         - [Notion](https://son-myeongjin.notion.site/datax-project-api?v=1aa07b1a3de181e38b81000cf2237f46)

        - ![](/assets/img/posts/post/datax_notion.png)
    5. 로그인기능 + JWT 토큰방식 구현
        - Rails의 Devise 라이브러리 이용.
    6. 글작성,삭제,수정 로직 구현 
    7. 태그 기능 구현
    8. AWS 를 통한 배포 
    9. Vue 클라이언트와 연동

# 実装した機能の説明

- 회원가입 기능
    - 이름, 이메일, 비밀번호 를 요청받는다.
    - 회원가입에 성공하면 이름, 이메일, 비밀번호를 DB에 저장.
    - 응답 : 이름, 이메일, 생성날짜, 회원Id
    (회원ID는 추후 게시글 수정 삭제시, 본인이 작성한 글인지 확인할때 쓴다)

- 로그인 로그아웃 기능
    - 로그인 기능
        - email 값과 password 값을 요청받고 DB에서 확인과정을 거칩니다.
        - 로그인이 성공하면 token 값을 반환합니다.
        - 해당 Token 은 Http Header 에 포함되어 요청되어야 다른 기능을 응답받을수있습니다. Ex) 글쓰기, 로그아웃 등 
    - 로그아웃 기능 (토큰필요)
        - 토큰값을 확인하고 로그인 상태이면 메세지를 통해 로그아웃됐음을 응답합니다. 
        - 해당 Token 값을 읽고 jti 값을 찾아내어 앞으로 오는 요청(로그아웃된 토큰)은 거부함.

- Posting 기능 (토큰필요)
    - Create Post
    - Delete Post
    - Edit Post
    - Get Post List

- 태그기능
    - Create Tags
    태그는 글을 작성할 때 추가가능합니다.
    이때, 태그를 요청받으면 같은 태그가 존재하면 해당 Id값을 반환하고, 존재하지 않는 태그를 요청하면 새로운 Id값을 부여하고 반환합니다.

    - Filtering with tags
    Get 방식으로 태그의 Id값을 요청 받으면 같은 태그의 글들을 배열로 반환합니다.

    - ![](/assets/img/posts/post/datax_tag.jpeg)


# 任意で工夫したポイント
- 로그인시 보안을 위한 JTI
JWT 토큰만 이용하여 로그인을 구현할 경우 로그아웃 한 뒤에도 토큰은 유효하여 접근이 가능하다는 점을 생각했습니다. 따라서 JTI 방식을 이용해 JWT 토큰을 거부할수있도록 추가적인 보안에 신경썼습니다. 

- ![](/assets/img/posts/post/datax_login.jpeg)