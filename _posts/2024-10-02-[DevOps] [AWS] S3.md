---
title:  "[AWS] S3 버킷"
categories: [Backend,DevOps]
tags:
  [
    DevOps,
    AWS,
    S3
  ] 
image: "/assets/img/title/s3.png"
---

# AWS S3(Simple Storage Service)란?
Simple Storage Service의 약자로 파일 서버의 역할을 하는 서비스다. 일반적인 파일서버는 트래픽이 증가함에 따라서 장비를 증설하는 작업을 해야 하는데 S3는 이와 같은 것을 대행한다. 트래픽에 따른 시스템적인 문제는 걱정할 필요가 없어진다. 또 파일에 대한 접근 권한을 지정 할 수 있어서 서비스를 호스팅 용도로 사용하는 것을 방지 할 수 있다. 아래는 S3의 주요한 기능적인 특성들이다.

### AWS S3 의 특징
* 많은 사용자가 접속을 해도 이를 감당하기 위해서 시스템적인 작업을 하지 않아도 된다.
* 저장할 수 있는 파일 수의 제한이 없다.
* 최소 1바이트에서 최대 5TB의 데이터를 저장하고 서비스 할 수 있다.
* 파일에 인증을 붙여서 무단으로 엑세스 하지 못하도록 할 수 있다.
* HTTP와 BitTorrent 프로토콜을 지원한다.
* REST, SOAP 인터페이스를 제공한다.
* 데이터를 여러 시설에서 중복으로 저장해 데이터의 손실이 발생할 경우 자동으로 복원한다.
* 버전관리 기능을 통해서 사용자에 의한 실수도 복원이 가능하다.
* 정보의 중요도에 따라서 보호 수준을 차등 할 수 있고, 이에 따라서 비용을 절감 할 수 있다. (RSS)

### AWS S3 에서 사용되는 용어
* 객체 - object, AWS는 S3에 저장된 데이터 하나 하나를 객체라고 명명하는데, 하나 하나의 파일이라고 생각하면 된다.
* 버킷 - bucket, 객체가 파일이라면 버킷은 연관된 객체들을 그룹핑한 최상위 디렉토리라고 할 수 있다. 버킷 단위로 지역(region)을 지정 할 수 있고, 또 버킷에 포함된 모든 객체에 대해서 일괄적으로 인증과 접속 제한을 걸 수 있다.
* 버전관리 - S3에 저장된 객체들의 변화를 저장. 예를들어 A라는 객체를 사용자가 삭제하거나 변경해도 각각의 변화를 모두 기록하기 때문에 실수를 만회할 수 있다.
* RSS - Reduced Redundancy Storage의 약자로 일반 S3 객체에 비해서 데이터가 손실될 확률이 높은 형태의 저장 방식. 대신에 가력이 저렴하기 때문에 복원이 가능한 데이터, 이를테면 섬네일 이미지와 같은 것을 저장하는데 적합하다. 그럼에도 불구하고 물리적인 하드 디스크 대비 400배 가량 안전하다는 것이 아마존의 주장
* Glacier - 영어로는 빙하라는 뜻으로 매우 저렴한 가격으로 데이터를 저장 할 수 있는 아마존의 스토리지 서비스

### AWS S3 버킷 생성
s3 를 검색하고 들어간 후 버킷 만들기 

<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/posts/post/스크린샷 2025-02-11 오후 6.36.51.png" width="400" />
</div>

* 버킷 이름은 전세계 고유한 이름이여야 한다.
* 대문자 사용 불가

<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/posts/post/스크린샷 2025-02-11 오후 6.37.52.png" width="400" />
</div>

* 버전 관리의 경우, 같은 파일을 올리면서 계속 업데이트 과정을 거치더라도, 업데이트 이전의 내용을 복원할 수 있게 해준다

<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/posts/post/스크린샷 2025-02-11 오후 6.37.56.png" width="400" />
</div>

그 다음, 퍼블릭 액세스

가장 첫 번째 부분을 체크해두면, 공개 설정으로 해둔 파일을 업로드 할 때, 업로드가 거절이 된다. 체크를 해제하면 공개 파일을 업로드 할 때 업로드가 됩다. 두 번째의 경우, 첫 번째 체크를 해제 하더라도, 비공개로 인식해서 공개가 되지 않는다

​즉 bucket를 비공개로 사용하겠다고 하면 체크를 하는것이 좋고, 업로드하는 파일중 어떠한것들은 공개 하고 싶다 라고 하면 체크를 해제하는것이 좋다


<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/posts/post/스크린샷 2025-02-11 오후 6.39.37.png" width="400" />
</div>

먼저 생성한 bucket을 누르면 여러 태그들이 뜨게됩니다. 객체의 경우 업로드한 파일 리스트들을 나타낸다.

객체 탭에서 파일을 올리면 

<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/posts/post/스크린샷 2025-02-11 오후 6.49.37.png" width="400" />
</div>
그러면 여러 옵션 사항들을 줄 수 있는데, 먼저 ACL 액세스 제어 목록에는 현재 객체(파일)을 읽고 쓰는 권한을 누구에게 줄 것인지 설정할 수 있다. AWS 계정 소유자만 읽고 쓰기가 가능하도록 선택하고 넘겨준다.

<div style="display: flex; justify-content: space-around;">
  <img src="/assets/img/posts/post/" width="400" />
</div>