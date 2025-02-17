---
title:  "[AWS] 로컬 .jar 파일 EC2 인스턴스에서 실행하기"
categories: [Backend,DevOps]
tags:
  [
    DevOps,
    AWS,
    EC2
  ] 
image: "/assets/img/title/ec2.png"
---

## 1. 로컬에서 jar 파일 빌드

```bash
./gradlew build -x test 
```
* 빌드가 완료되면, 다음과 같이 jar 파일이 있는지 확인
    ```bash
    ls build/libs
    ```
    보통 build/libs 에 .jar 파일 생성됨

## 2. EC2 인스턴스 접속
* 터미널에서 cd 로 pem 인증서 있는곳까지 들어간다음 명령어 실행
    ```bash
    ssh -i "DBak.pem" ec2-user@ec2-54-.......3.ap-northeast-2.compute.amazonaws.com
    ```


## 3. jar파일을 ec2 인스턴스로 전송

* 인증서 있는곳에서 명령어 실행
    ```
    scp -i /path/to/your-key.pem target/your-app.jar ubuntu@your.ec2.public.ip:/home/ubuntu/
    ```
    ```bash
    scp -i "DBak.pem" build/libs/DBak-0.0.1-SNAPSHOT.jar ec2-user@ec2-54-180-90-233.ap-northeast-2.compute.amazonaws.com:/home/ec2-user/
    ```

## 4. EC2 인스턴스에 Java 설치 확인
```bash
java -version
```

## 5. 환경변수 필요하면 설정하기
```bash
export AWS_ACCESS_KEY_ID=your_access_key_id
export AWS_SECRET_ACCESS_KEY=your_secret_access_key
```

### 혹시 이미 8080 포트에서 배포중이면 종료하기
* 포트 사용주인거 확인하고
    ```
    sudo lsof -i :8080
    ```
* 포트 실행중인거 죽이고
    ```
    sudo kill -9 <PID>
    ```

## 6. jar 파일 실행
* .jar파일이 있는 디렉토리에 가서 
    ```bash
    java -jar DBak-0.0.1-SNAPSHOT.jar
    ```

* 터미널을 닫아도 계속 실행되도록 하려면 nohup을 사용하세요.
    ```bash
    nohup java -jar DBak-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
    ```