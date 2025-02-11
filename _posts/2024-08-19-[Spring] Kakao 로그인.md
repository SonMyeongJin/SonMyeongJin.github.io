---
title:  "[Spring] Kakao 로그인 API"
categories: [Backend,Java]
tags:
  [
    java,
    spring,
    kakao,
    login,
    Thymeleaf
  ] 
image: "/assets/img/title/spring.png"
---
# 사전작업
1. 카카오 로그인 API REST API KEY 발급받기
    * https://developers.kakao.com/docs/latest/ko/kakaologin/rest-api
    ![](/assets/img/스크린샷%202025-02-09%20오후%2010.43.04.png)
    * Redirect URI 등록 (내 어플리케이션 > 앱 설정 > 플랫폼)
     ![](/assets/img/스크린샷%202025-02-09%20오후%2010.43.12.png)
    * 동의 항목 체크 (내 어플리케이션 > 제품 설정 > 카카오 로그인 > 동의항목)
    ![](/assets/img/스크린샷%202025-02-09%20오후%2010.43.25.png)
2. pom.xml에 라이브러리 추가
    ```
    <!--카카오 로그인-->
    <dependency>
        <groupId>com.google.code.gson</groupId>
        <artifactId>gson</artifactId>
        <version>2.8.6</version>
    </dependency>
    <dependency>
        <groupId>com.googlecode.json-simple</groupId>
        <artifactId>json-simple</artifactId>
        <version>1.1.1</version>
    </dependency>
    ```

# Kakao API 로그인 기능 구현

![](/assets/img/스크린샷%202025-02-09%20오후%2010.46.37.png)


## 1. 로그인 페이지에 `카카오 로그인 버튼` 만들기

* `memberLoginForm.html`

    ```html
    <!-- 카카오 스크립트 -->
    <script src="https://developers.kakao.com/sdk/js/kakao.js"></script>

    ...
    <div class="kakao-btn" onclick="kakaoLogin()">
        <a>카카오톡으로 간편로그인</a>
    </div>
    ...
    <script th:inline="javascript">
    function kakaoLogin() {
    $.ajax({
    url:'/memberLoginForm/getKakaoAuthUrl',
    type:'post',
    async: false,
    dataType: 'text',
    success: function (res) {
    location.href = res;
    }
    });
    }
    </script>
    ```
    memberLoginForm페이지에서 카카오 로그인 기능을 호출하므로 ajax url에 /memberLoginForm/getKakaoAuthUrl로 적는다.
    (getKakaoAuthUrl이 부분은 공통)

## 2. Controller에서 메소드 만들기

 * `LoginController.java`
    ```java
    //카카오 로그인 기능이 처리되는 페이지
    @RequestMapping(value = "/memberLoginForm/getKakaoAuthUrl")
    public @ResponseBody String getKakaoAuthUrl(HttpServletRequest request) throws Exception {

        String reqUrl =
                "https://kauth.kakao.com/oauth/authorize?client_id=발급받은 REST API 키&redirect_uri=redirect_uri설정한 주소&response_type=code";

        return reqUrl;
    }   
    ```

    `reqUrl`에 발급받은 api키와 대표 redirct_uri를 넣는다.
    ```java
    @RequestMapping(value = "/auth_kakao")
    public String oauthKakao(
            @RequestParam(value = "code",required = false) String code
            , HttpSession session, RedirectAttributes rttr) throws Exception {

        log.info("#######" + code);
        String access_Token = loginServ.getAccessToken(code);
        String view = loginServ.getuserinfo(access_Token, session, rttr);
        

        return view;
    }
    ```
    access_Token을 보내 인가 코드를 받고 `getuserinfo` 메소드로 사용자 정보를 가져와서 리턴한다.

## 3. Service에서 데이터 처리하기

* `LoginService.java`
    ```java
    public String getAccessToken(String authorize_code) {
    String access_Token = "";
    String refresh_Token = "";
    String reqURL = "https://kauth.kakao.com/oauth/token";

    try {
        URL url = new URL(reqURL);

        HttpURLConnection conn = (HttpURLConnection) url.openConnection();

        //    POST 요청을 위해 기본값이 false인 setDoOutput을 true로 변경을 해주세요

        conn.setRequestMethod("POST");
        conn.setDoOutput(true);

        //    POST 요청에 필요로 요구하는 파라미터 스트림을 통해 전송
        // BufferedWriter 간단하게 파일을 끊어서 보내기로 토큰값을 받아오기위해 전송

        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(conn.getOutputStream()));
        StringBuilder sb = new StringBuilder();
        sb.append("grant_type=authorization_code");
        sb.append("&client_id=");  //발급받은 key
        sb.append("&redirect_uri=");     // 본인이 설정해 놓은 redirect_uri 주소
        sb.append("&code=" + authorize_code);
        bw.write(sb.toString());
        bw.flush();

        //    결과 코드가 200이라면 성공
        // 여기서 안되는경우가 많이 있어서 필수 확인 !! **
        int responseCode = conn.getResponseCode();
        System.out.println("responseCode : " + responseCode + "확인");

        //    요청을 통해 얻은 JSON타입의 Response 메세지 읽어오기
        BufferedReader br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
        String line = "";
        String result = "";

        while ((line = br.readLine()) != null) {
            result += line;
        }
        System.out.println("response body : " + result + "결과");

        //    Gson 라이브러리에 포함된 클래스로 JSON파싱 객체 생성
        JsonParser parser = new JsonParser();
        JsonElement element = parser.parse(result);

        access_Token = element.getAsJsonObject().get("access_token").getAsString();
        refresh_Token = element.getAsJsonObject().get("refresh_token").getAsString();

        System.out.println("access_token : " + access_Token);
        System.out.println("refresh_token : " + refresh_Token);

        br.close();
        bw.close();
    } catch (IOException e) {

        e.printStackTrace();
    }
    return access_Token;
    ```

    access_Token을 컨트롤러로 리턴하고 이 access_Token으로 사용자 정보를 처리한다.

    ```java
     public String getuserinfo(String access_Token, HttpSession session, RedirectAttributes rttr) {
    HashMap<String, Object> userInfo = new HashMap<>();
    log.info("getuserinfo()");

    String requestURL = "https://kapi.kakao.com/v2/user/me";
    String view = null;
    String msg = null;

    try {
        URL url = new URL(requestURL); //1.url 객체만들기
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        //2.url 에서 url connection 만들기
        conn.setRequestMethod("GET"); // 3.URL 연결구성
        conn.setRequestProperty("Authorization", "Bearer " + access_Token);

        //키 값, 속성 적용
        int responseCode = conn.getResponseCode(); //서버에서 보낸 http 상태코드 반환
        System.out.println("responseCode :" + responseCode + "여긴가");
        BufferedReader buffer = new BufferedReader(new InputStreamReader(conn.getInputStream()));
        // 버퍼를 사용하여 읽은 것
        String line = "";
        String result = "";
        while ((line = buffer.readLine()) != null) {
            result += line;
        }
        //readLine()) ==> 입력 String 값으로 리턴값 고정

        System.out.println("response body :" + result);

        // 읽었으니깐 데이터꺼내오기
        JsonParser parser = new JsonParser();
        JsonElement element = parser.parse(result); //Json element 문자열변경
        JsonObject properties = element.getAsJsonObject().get("properties").getAsJsonObject();
        JsonObject kakao_account = element.getAsJsonObject().get("kakao_account").getAsJsonObject();

        String mnickname = properties.getAsJsonObject().get("nickname").getAsString();
        String mmail = kakao_account.getAsJsonObject().get("email").getAsString();
        
		//userInfo에 사용자 정보 저장
        userInfo.put("mid", mmail);
        userInfo.put("mnickname", mnickname);
        userInfo.put("mmail", mmail);

        log.info(String.valueOf(userInfo));

    } catch (Exception e) {
        e.printStackTrace();
    }

    MemberDto member = memberDao.findkakao(userInfo);
    // 저장되어있는지 확인
    log.info("S :" + member);

    if (member == null) {
        //member null 이면 정보가 저장 안되어있는거라서 정보를 저장.
        memberDao.kakaoinsert(userInfo);
        //저장한 member 정보 다시 가져오기 HashMap이라 형변환 시켜줌
        member = loginnDao.selectMember((String)userInfo.get("mid"));
        session.setAttribute("member", member);
		
        //로그인 처리 후 메인 페이지로 이동
        view = "redirect:/";
        msg = "로그인 성공";
    } else {
        session.setAttribute("member", member);
        view = "redirect:/";
        msg = "로그인 성공";

    }
    rttr.addFlashAttribute("msg", msg);
    return view;
    ```
    userInfo를 HashMap으로 초기화했는데, member 정보를 다시 반환시켜주기 위해 select로 검색할 때는 (String)으로 변환시켜서 데이터를 가져온다.
    * userInfo데이터로 조회해서 이미 데이터베이스에 등록된 회원일 경우 회원정보 저장없이 세션에 담아 로그인 처리한다.
    * 회원 테이블에 없는 userInfo일 경우 insert 처리

## 4. 데이터베이스에 저장하기

* `MemberDao.java`
    ```java
    @Mapper
    public interface MemberDao {

        //이미 가입된 회원인지 확인하는 메소드
        MemberDto findkakao(HashMap<String, Object> userInfo);

        //카카오 로그인 회원정보 저장
        void kakaoinsert(HashMap<String, Object> userInfo);

        }
    ```
* `MemberDao.xml`
    ```java
    <mapper namespace="com.project.ohgym.dao.MemberDao">

        <select id="findkakao" resultType="MemberDto" parameterType="HashMap">
            select * from member where mid=#{mid} and mmail=#{mmail} and mnickname=#{mnickname}
        </select>

        <insert id="kakaoinsert">
        insert into member
        values (null, #{mid}, null, #{mmail}, null, null, null, null, #{mnickname},
                null, null, null, null, null, null, null, null, null, null)
        </insert>

    </mapper>
    ```
