---
title: "Jenkins로 배포자동화 하기(2) - github 와 젠킨스 연동 설정"
date: 2020-01-16 22:24:30 +0900
categories:
  - Jenkins
tags:
  - Jenkins
  - Github
  - CI/CD
  - 배포 자동화
classes: wide
---

## Github 설정하기
- - -
Github와 Jenkins를 연동하려면 Access token이 필요합니다.   
[github홈페이지](https://github.com/)에 들어가서 로그인을 한 후   
Settings -> Developer settings -> Personal access tokens로 들어갑니다.   

![](/assets/images/Jenkins_start/2-01.png)   

새로운 토큰의 이름과 원하는 스코프를 선택해 발급받고
빨간 박스로 가려둔 내용을 복사해 둡니다.   

![](/assets/images/Jenkins_start/2-02.png)   

![](/assets/images/Jenkins_start/2-03.png)   

![](/assets/images/Jenkins_start/2-04.png)   

## Jenkins 설정하기
- - -

다시 Jenkins로 돌아와서 `Jenkins 관리`에서, `시스템 설정` 메뉴로 들어갑니다.   
![](/assets/images/Jenkins_start/2-05.png)   

`Add Github Server` 눌러서 Server를 추가하고 원하시는 Name을 입력하시고 Credintial를 추가해줍니다.   

![](/assets/images/Jenkins_start/2-06.png)   

도메인과 종류를 바꾸고 Secret에 아까 복사에 둔 Github access token을 붙혀넣으면 됩니다.   
ID에는 원하시는 ID 값을 입력하면 됩니다.   

![](/assets/images/Jenkins_start/2-07.png)   

Test connention을 눌러 정상적으로 작동되는지 확인할 수 있습니다.   

![](/assets/images/Jenkins_start/2-08.png)   

그 다음으로 제일 중요한 `Jenkins URL` 설정을 해 주셔야합니다.   
이 설정을 하지 않으면 Github에서 아무리 요청을 보내도 Jenkins는 받지 못합니다.
저는 공유기의 포트포워딩을 사용해 외부IP와 제 노트북IP를 연결시켜 주었습니다.   
이렇게 설정하면 공유기 안에서만 github의 요청을 받습니다.   

![](/assets/images/Jenkins_start/2-09.png)   
