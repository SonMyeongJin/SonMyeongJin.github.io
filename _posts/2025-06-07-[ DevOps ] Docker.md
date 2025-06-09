---
title: "[CI/CD] Docker 설치"
categories: [Backend,DevOps]
tags:
  [
    DevOps,
    AWS,
    CI/CD,
    Docker
  ] 
---

## Docker 설치

Docker Desktop을 설치하려면 다음 링크를 참고하세요:
[https://docs.docker.com/desktop/install/mac-install/](https://docs.docker.com/desktop/install/mac-install/)

본인의 OS와 칩셋에 맞게 설치를 진행합니다.

### 설치 확인

설치가 완료되었으면 터미널에서 Docker 버전 정보를 확인할 수 있습니다:

```bash
docker -v
```

도커 프로그램을 실행하고 다음 명령어를 사용하면 Client와 Server에 대한 자세한 버전 정보도 확인할 수 있습니다:

```bash
docker version
```

## Docker 컨테이너의 기본 제어

설치를 완료하였으니 Docker 이미지를 제어하는 기본적인 방법에 대해 알아보겠습니다.

Docker 컨테이너는 Docker 명령으로 제어하고, 서브 명령(실질적 첫 번째 인수)으로 제어할 내용을 지정합니다.

### 대표적인 서브 명령

#### 라이프사이클 제어

| 서브 명령 | 의미 |
|----------|------|
| `run` | 배포, 실행 |
| `stop` | 실행 중인 컨테이너를 정지시킨다 |
| `start` | 정지 중인 컨테이너를 실행한다 |
| `rm` | 배포한 컨테이너를 삭제한다 |

#### 컨테이너 제어

| 서브 명령 | 의미 |
|----------|------|
| `exec` | 실행 중인 컨테이너에 명령을 실행 |
| `logs` | 컨테이너의 로그를 표시 |
| `inspect` | 컨테이너/이미지의 상세 정보를 표시 |

#### 이미지 제어

| 서브 명령 | 의미 |
|----------|------|
| `images` | 데몬에 있는 이미지 목록을 표시 |
| `rmi` | 데몬에 있는 이미지를 삭제 |

### run: 배포 및 실행

기본 사용법:
```bash
docker run [옵션] 이미지[:태그] [명령] [인수...]
```
