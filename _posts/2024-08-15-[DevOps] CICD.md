---
title:  "[DevOps] CI/CD 개념"
categories: [Backend,DevOps]
tags:
  [
    DevOps,
    CI/CD,
    AWS
  ] 
---

## CI/CD 개요
 CI/CD 환경이 구축되어 있지 않다면 애플리케이션 변경 사항이 발생할 때 매번 로컬에서 빌드하고, 빌드된 jar 파일 config 파일 등을 직접 서버에 SFTP로 개발/운영 다수의 서버에 배포를 해야한다.

 ## CI/CD 란

> CI(Continuous Integration) - 지속적 통합

 CI란 병렬적으로 작업한 새로운 소스 코드에 대해 자동으로 빌드 -> 테스트를 통해 검증한 뒤 코드 검증이 끝나면, 변경사항을 공유 레포지토리에 통합하는 것을 의미한다.  

 CI를 도입함으로써, 소스코드의 품질을 유지하고, 여러 개발자들이 협업하는 과정에서 생길 수 있는 오류를 최소화 하는데 도움 되고, 개발자들은 안정적이고 신뢰할 수 있는 애플리케이션을 빠르게 제공할 수 있다.  

![](/assets/img/스크린샷%202025-02-04%20오후%201.27.02.png)


1. 각 브랜치 별로 새로운 코드에 대해서 commit & push를 진행

2. 미리 구축되어 있는 ci pipline을 통해 빌드 - 테스트 등 작업을 자동으로 진행

3. 빌드 - 테스트가 성공적으로 끝나면 review를 통해 소스 검증 뒤 승인되면 통합 branch에 통합 

> CD(Continous Deliver | Continuous Deployemnt) - 지속적 제공(배포) 

변경된 서비스를 실제 사용자 환경(production)에 제공해야 한다.

Continuous Delivery는 소프트웨어를 지속적으로 릴리스할 수 있는 프로세스를 의미한다. 

Continuous Deployment는 Continuous Delivery의 한 유형으로, 테스트 및 검증이 완료된 모든 변경사항이 자동으로 production 환경에 배포되는 것을 의미한다.

![](/assets/img/스크린샷%202025-02-04%20오후%201.29.29.png)

실제 서비스를 제공해야 할 브랜치를 main으로 가정하자.

1. ci를 적용하여 코드를 검증

2. production 환경에 배포하기 전 production 환경과 유사한 staging 환경해서 검증

3. 검증된 서비스를 실제 production 환경에 배포 

CI/CD를 적용하면 빌드 - 테스트 배포 과정이 자동화 되어 있기 때문에 개발자는 배포보다 개발에 더욱 신경쓸 수 있다.
