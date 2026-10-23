---
title:  "[Ios App] [Server] EC2 서버 배포 "
categories: [Project, Personal]
tags:
  [ios,
  spring,
  java,
  ec2,
  aws
  ] 
image: "/assets/img/title/ec2.png"
---

## AWS EC2 서버 배포 

1. ### EC2 생성 
    ![](/assets/img/posts/2025-01-10-ios-server-ec2/01-security-group.png)
    * 보안 sh 22 포트로 접속

2. ### EC2 인스턴스에 Java 17 버전 설치
![](/assets/img/posts/2025-01-10-ios-server-ec2/02-install-java.png)

3. ### 로컬에서 .jar 파일 생성후 EC2 인스턴스로 .jar 파일 전송
![](/assets/img/posts/2025-01-10-ios-server-ec2/03-upload-jar.png)

4. ### 환경변수 설정
    ![](/assets/img/posts/2025-01-10-ios-server-ec2/04-env-variables.png)
    * 서버 개발할때 S3 접속하기 위한 접근키, 비밀키 환경변수 설정해준 과정 동일하게 EC2 에서도 설정

5. ### 배포 완료후 http://퍼블릭ip/도메인 으로 테스트 
    ![](/assets/img/posts/2025-01-10-ios-server-ec2/05-deploy-complete.png)

### 정상적인 접근 가능! 배포 완료!