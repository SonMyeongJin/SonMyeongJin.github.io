---
title:  "[Github] Actions "
layout: post 
categories: [github]
tags:
  [
    github,
    actions
    ] 
image: "/assets/img/title/github_logo_black.png"
---


GitHub Pages에서 GitHub Actions 설정은 GitHub Actions가 배포 과정을 관리하도록 역할을 부여하는 것
이를 통해 자동화된 CI/CD(Continuous Integration/Continuous Deployment)를 구현 가능

## GitHub Pages 설정에서 Actions의 역할

GitHub Pages 설정에서 Actions를 활성화하면:

1. 빌드 및 배포 관리:
* Actions가 Jekyll이나 Hugo 같은 빌드 프로세스를 수행합니다.
* 이 과정에서 소스 코드(markdown, scss 등)를 변환해 최종적으로 필요한 정적 파일만 생성.
* 생성된 파일을 GitHub Pages가 호스팅할 경로에 배포합니다.

2. 자동화된 워크플로우:
* 새로운 커밋이나 푸시가 발생하면 Actions가 정의된 워크플로우에 따라 자동으로 실행됩니다.
* 수동 작업 없이 배포가 진행되므로 생산성이 향상됩니다.

3. 복잡한 프로젝트 관리:
* JavaScript나 CSS 빌드처럼 복잡한 처리 과정이 필요한 프로젝트도 Actions로 자동화 가능.
* 예를 들어, webpack, babel 등 빌드 도구와의 연동도 가능합니다.

## 결론적으로 Actions를 설정하지 않으면?
* GitHub Pages는 소스 파일을 직접 읽어 호스팅하며, 빌드 과정은 실행되지 않습니다.
* Jekyll, Sass 변환, Markdown 렌더링 등이 자동으로 이루어지지 않습니다.
* Actions가 없는 경우 수동으로 빌드한 파일을 브랜치에 커밋해야 합니다(비효율적).

## 간단히 말하면
Actions를 설정하지 않으면, GitHub Pages는 "완성된 결과물만 보여주는 갤러리"와 같습니다.
하지만 Actions를 설정하면, "갤러리에서 작품을 만드는 공방"이 추가된다고 볼 수 있습니다.
즉, Actions는 코드를 빌드하고 최종 결과를 자동으로 갤러리에 배치하는 역할을 합니다.