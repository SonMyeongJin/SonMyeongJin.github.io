---
title:  "[AWS] EC2 배포하기"
categories: [Backend,DevOps]
tags:
  [
    DevOps,
    AWS,
    EC2
  ] 
image: "/assets/img/title/ec2.png"
---

# 🚀 Spring Boot 서버를 AWS EC2에 배포하는 방법
## 1️⃣ AWS EC2 인스턴스 생성
1. AWS 로그인 후 EC2 서비스로 이동
2. 인스턴스 시작 버튼 클릭
3. 아래 설정으로 인스턴스 생성
    * AMI: Ubuntu 22.04 LTS (Amazon Linux도 가능)
    * 인스턴스 유형: t2.micro (프리티어 가능)
    * 스토리지: 기본 8GB SSD
    * 보안 그룹 설정
        * 8080 포트 열기 (Custom TCP Rule, 0.0.0.0/0)
        * 22 포트 열기 (SSH 접속용)
4. 키 페어 (pem 파일) 다운로드
    * 나중에 EC2에 접속할 때 필요하니 보관

## 2️⃣ EC2 서버에 SSH 접속
다운로드한 .pem 파일을 사용하여 EC2에 접속

```bash
chmod 400 your-key.pem  # 키 파일 권한 설정
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

## 3️⃣ Java & 필요한 패키지 설치
EC2에서 Java 17 설치 (Spring Boot 3.x 기준)
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install openjdk-17-jdk -y
java -version  # 설치 확인
```

## 4️⃣ Spring Boot 프로젝트 빌드
1) ### 로컬에서 Jar 파일 생성
    EC2에서 실행할 .jar 파일을 빌드
    ```bash
    ./mvnw clean package -DskipTests  # Maven 사용 시
    # 또는
    ./gradlew bootJar  # Gradle 사용 시
    ```
    📌 target/ 또는 build/libs/ 폴더에 your-app.jar 파일이 생성됨.

2) ### EC2로 전송
    로컬에서 EC2로 .jar 파일 전송
    ```bash
    scp -i your-key.pem target/your-app.jar ubuntu@your-ec2-public-ip:~
    ```
## 5️⃣ Spring Boot 애플리케이션 실행
EC2에서 .jar 파일 실행
```bash
nohup java -jar your-app.jar > log.txt 2>&1 &
```
* ✅ nohup 사용하면 백그라운드 실행됨
* ✅ 로그는 log.txt에서 확인 가능

앱이 실행됐는지 확인
```bash
ps aux | grep java  # 실행 중인 Java 프로세스 확인
```

## 6️⃣ 방화벽 설정 & API 테스트
1) EC2 보안 그룹에서 8080 포트 열었는지 확인
    * AWS 콘솔 → EC2 → 보안 그룹 → 인바운드 규칙 → 8080 열려 있는지 확인
2) Spring Boot 서버 접속 확인
로컬에서 아래 명령 실행
```bash
curl http://your-ec2-public-ip:8080/api/videos/BTS
```
🚀 정상적으로 JSON 데이터가 반환되면 성공!

## 7️⃣ Spring Boot 서버를 백그라운드에서 자동 실행
지금은 nohup으로 실행했지만, EC2가 재부팅되면 서버가 꺼져. 자동 실행을 위해 systemd 서비스 등록하면 좋다

1) 서비스 파일 생성
    ```bash
    sudo nano /etc/systemd/system/daebak.service
    ```
    다음 내용 추가
    ```ini
    [Unit]
    Description=Spring Boot DaeBak Server
    After=network.target

    [Service]
    User=ubuntu
    WorkingDirectory=/home/ubuntu
    ExecStart=/usr/bin/java -jar /home/ubuntu/your-app.jar
    SuccessExitStatus=143
    Restart=always
    RestartSec=5
    StandardOutput=append:/home/ubuntu/app.log
    StandardError=append:/home/ubuntu/error.log

    [Install]
    WantedBy=multi-user.target
    ```
2) 서비스 등록 & 실행
    ```bash
    sudo systemctl daemon-reload
    sudo systemctl enable daebak
    sudo systemctl start daebak
    sudo systemctl status daebak  # 실행 확인
    ```
이제 EC2를 재부팅해도 서버가 자동으로 실행됨! 🚀

## 8️⃣ 고정 IP & 도메인 연결 (선택)
* 고정 IP 설정: Elastic IP 할당 (AWS 콘솔에서 가능)
* 도메인 연결: Route 53에서 도메인 구매 후 Elastic IP 연결
* 무료 도메인: Cloudflare를 사용해 서브도메인 적용 가능



# EC2 생성 시 - `보안그룹`
### 인바운드 규칙
* 외부 → EC2 인스턴스로 들어오는 트래픽을 허용하는 규칙.
* 예제
    *  SSH (22번 포트): 내 PC에서 EC2에 접속하기 위해 허용 (내 IP만 허용하는 게 안전함)
    * HTTP (80번 포트): 웹사이트 요청을 받기 위해 허용
    * HTTPS (443번 포트): SSL/TLS를 통한 보안 요청을 받기 위해 허용
    * Spring Boot API (8080번 포트): 클라이언트(예: Swift 앱)가 API를 호출하기 위해 필요

✅ 즉, "서버로 들어오는 요청을 허용하는 포트"를 설정하는 것.

### 아웃바운드 규칙
* EC2 인스턴스 → 외부로 나가는 트래픽을 허용하는 규칙.
* 기본적으로 AWS EC2는 아웃바운드 트래픽을 모두 허용하지만, 특정 환경에서는 필요할 수도 있음.
* 예제
    * 인터넷 액세스 허용 (80, 443): 서버에서 외부 API 호출 가능하도록 함.
    * DB 연결 (3306): RDS(MySQL)와 연결할 때 필요.
    * S3 접근 (443): EC2에서 S3 파일을 업로드/다운로드할 때 필요.

✅ 즉, "서버에서 외부로 나가는 요청을 허용하는 포트"를 설정하는 것.

### 🔥 EC2에서 Spring Boot API 운영할 때 필요한 보안 그룹 설정
✅ 인바운드 규칙
* `EC2접속용` : SSH - TCP - 22포트 - 내 IP
* `Spring 접근` : HTTP - TCP - 8080포트 - 0.0.0.0/0(모든 트래픽)

✅ 아웃바운드 규칙 (기본 설정)
* 모든 트래픽 허용 (0.0.0.0/0)

>⚠️ 주의
* SSH(22)는 **반드시 "내 IP"**만 허용해야 보안이 강해짐. (0.0.0.0/0은 절대 금지 ❌)
* 8080 대신 80 포트에서 API를 제공하고 싶으면, Nginx 같은 리버스 프록시를 설정해야 함.