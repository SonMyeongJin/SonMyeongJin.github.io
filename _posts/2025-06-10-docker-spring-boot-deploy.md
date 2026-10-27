---
title: "Docker로 Spring Boot 프로젝트 EC2에 배포하기"
categories: [DevOps, Docker]
tags: [docker, docker-hub, spring-boot, ec2]
image: "/assets/img/title/docker.png"
redirect_from:
  - "/posts/DevOps-Docker2/"
---

# 🐋 Docker를 활용한 배포 Flow

## 배포 프로세스 개요

1. Dockerfile을 작성한 후, 빌드하여 docker image를 생성한다.
2. Docker image 파일을 docker hub에 push한다.
3. 서버(AWS EC2)에서 docker hub에 있는 docker image를 pull 받아온다.
4. `docker run` 명령어로 docker image를 실행한다.

## 1️⃣ Spring Boot 프로젝트 생성

배포를 할 스프링 부트 프로젝트를 생성한다.
스프링 부트 프로젝트 생성 방법에 대해 궁금한 사람은 [인텔리제이로 스프링부트 시작하기]를 참고하자.

## 2️⃣ Dockerfile 생성

폴더 최상단에 `Dockerfile`을 생성하고 아래와 같이 내용을 채워준다.

```dockerfile
# open jdk 11 버전의 환경을 구성
FROM adoptopenjdk/openjdk11:latest

# build가 되는 시점에 JAR_FILE이라는 변수 명에 build/libs/*.jar 선언
# build/libs - gradle로 빌드했을 때 jar 파일이 생성되는 경로
ARG JAR_FILE=build/libs/*.jar

# JAR_FILE을 app.jar로 복사
COPY ${JAR_FILE} app.jar

# 운영 및 개발에서 사용되는 환경 설정을 분리
ENTRYPOINT ["java", "-jar", "-Dspring.profiles.active=prod", "/app.jar"]
```

## 3️⃣ Gradle Build

```bash
./gradlew build -x test
```

빌드를 하여 jar 파일을 생성한다.

## 4️⃣ Docker Hub Repository 생성

Docker Hub에 들어가 Repository를 만들어준다.
이 때, visibility는 Public으로 한다.

## 5️⃣ Docker Image Build

```bash
# docker build --build-arg DEPENDENCY=build/dependency -t (도커 허브 ID)/(Repository 이름) --platform linux/amd64 .
docker build --build-arg DEPENDENCY=build/dependency -t leeeeeyeon/docker-test --platform linux/amd64 .
```

맥북의 경우 `--platform linux/amd64` 옵션을 추가해주어야 한다.

## 6️⃣ Docker Image Push

```bash
docker push leeeeeyeon/docker-test
```

방금 생성한 Repository의 Tag 부분을 통해 push가 잘 된 것을 확인할 수 있다.

> 앞서 언급한 Docker를 활용한 배포 Flow 중, 하늘색 박스 친 부분까지 완료되었다.
> 이제 나머지 부분을 진행해보자 😄

## 7️⃣ EC2에 Docker 설치 및 실행

### Ubuntu 환경

```bash
# 패키지 업데이트
sudo apt-get update -y

# 기존에 있던 도커 삭제
sudo apt-get remove docker docker-engine docker.io -y

# 도커 설치
sudo apt-get install docker.io -y

# docker 서비스 실행
sudo service docker start

# /var/run/docker.sock 파일의 권한을 666으로 변경하여 그룹 내 다른 사용자도 접근 가능하게 변경
sudo chmod 666 /var/run/docker.sock

# ubuntu 유저를 docker 그룹에 추가
sudo usermod -a -G docker ubuntu
```

### Linux 환경

```bash
# 패키지 업데이트
sudo yum update -y

# docker 설치
sudo yum install docker -y

# docker 서비스 실행
sudo service docker start

# ec2-user를 docker 그룹에 추가
sudo usermod -a -G docker ec2-user
```

## 8️⃣ Docker Image Pull 및 애플리케이션 배포

```bash
sudo docker pull (도커 허브 ID)/(Repository 이름)
sudo docker run -p 8080:8080 (도커 허브 ID)/(Repository 이름)
```

이제 Docker를 활용한 완전한 배포 플로우가 완성되었다! 🎉
