---
title: "Jenkins로 배포자동화 하기(1) - 설치 및 기본 설정"
date: 2020-01-05 15:14:30 +0900
categories:
  - Jenkins
tags:
  - Jenkins
  - CI/CD
  - 배포 자동화
classes: wide
---

토이 프로젝트를  진행하면서 
빌드, 테스트, 배포 과정을 수동으로 반복하면서 시간이 점점 늘어났습니다.
시간 단축과 빌드 및 배포 자동화를 위해 CI 툴을 사용해보려고 합니다.

CI 툴은 circleCI, Jenkins, Travis CI, Bamboo 등이 있습니다.
그중에서 	Jenkins를 사용해보려고 합니다.



## Jenkins 설치하기
- - - -
제 개발 환경은 MacOS로 현재 패키지 관리자인 Homebrew가 설치되어있습니다.

[Homebrew 설치하기](https://brew.sh/index_ko)

Homebrew가 설치됐다면 [Jenkins 홈페이지](https://jenkins.io)에서 원하는 버전을 받으면 됩니다.
![](/assets/images/Jenkins_start/1-01.jpeg)

저는 Jenkins-LTS 버전을 선택해  

```shell
brew install jenkins-lts
```

로 설치했습니다.

설치중에 이런 오류가 나오면   
![](/assets/images/Jenkins_start/1-02.png)   

```shell
brew cask install homebrew/cask-versions/adoptopenjdk8
```

로 자바를 설치해 주면 됩니다.   

설치가 끝나 후 터미널에 `jenkins-lts`로 직접 실행하거나
`brew services start jenkins-lts`를 입력해 백그라운드 서비스로 등록해도 됩니다.   

Jenkins를 실행 하면 기본적으로 `http://localhost:8080`으로 접속이 가능합니다.   

![](/assets/images/Jenkins_start/1-03.png)   

로딩을 기다리면 비밀번호를 입력하라고 하는데 가려놓은 붉은 색 부분에 비밀번호가 있는 파일이 있습니다.   
`cat` 명령어를 사용해 해당 비밀번호를 확인 후 입력하면 됩니다.   
![](/assets/images/Jenkins_start/1-04.png)   

플러그인 설치 화면이 나오면 일반적으로 사용되는 플러그인들을 설치해주는 왼쪽을 클릭해 설치를 진행하면 됩니다. 나중에 원하는 플러그인을 추가로 설치 할 수 있습니다.   
![](/assets/images/Jenkins_start/1-05.png)   
![](/assets/images/Jenkins_start/1-06.png)   

플러그인 설치가 끝나면 관리자 계정을 만드는 화면이 나옵니다.   
Jenkins에 접속할 때 필요하므로 자신에게 맞는 정보를 입력합니다.   
![](/assets/images/Jenkins_start/1-07.png)

정보등록이 끝나면 Jenkins로 접속할 수 있습니다.   
![](/assets/images/Jenkins_start/1-08.png)   

## Jenkins 설정하기
- - - -
github를 이용해 배포를 진행하기 위해서는 추가로 설정을 해줘야 됩니다.   
젠킨스 메인의 `Jenkins 관리`에서, `Global Tool Configuration` 메뉴로 들어갑니다.   
![](/assets/images/Jenkins_start/1-09.png)   

git을 설정해 줍니다. Name은 원하는대로 설정해 주고 밑에는 git이 설치되어있는 Path를 적어주면 됩니다.   
설치 위치를 모르면 터미널에 `where git`으로 찾으면 됩니다.   
![](/assets/images/Jenkins_start/1-10.png)   
