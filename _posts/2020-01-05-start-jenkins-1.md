---
title: "Jenkins로 배포자동화 하기(1)"
date: 2020-01-05 15:14:30 +0900
categories:
  - Jenkins
tags:
  - Jenkins
  - CI/CD
classes: wide
---

토이 프로젝트를  진행하면서 
빌드, 테스트, 배포 과정을 수동으로 반복하면서 시간이 점점 늘어났다.
시간 단축과 빌드 및 배포 자동화를 위해 CI 툴을 사용해보려고 한다.

CI 툴은 circleCI, Jenkins, Travis CI, Bamboo 등이 있다.
그중에서 	Jenkins를 사용해보려고 한다.



## 1. Jenkins 설치하기
- - - -
내 개발 환경은 MacOS로 현재 패키지 관리자인 Homebrew가 설치되어있다.

[Homebrew 설치하기](https://brew.sh/index_ko)

Homebrew가 설치됐다면 [Jenkins 홈페이지](https://jenkins.io)에서 원하는 버전을 받으면 된다.
![](/assets/images/IMG_0109.jpeg)

저는 Jenkins-LTS 버전을 선택해 `brew install jenkins-lts`로 설치했다.