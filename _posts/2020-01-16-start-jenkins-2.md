---
title: "Jenkins로 배포자동화 하기(2)"
date: 2020-01-16 22:24:30 +0900
categories:
  - Jenkins
tags:
  - Jenkins
  - CI/CD
  - 배포 자동화
classes: wide
---

## Github 설정하기
- - - -
Github와 Jenkins를 연동하려면 Access token이 필요합니다.
[github홈페이지](https://github.com/)에 들어가서 로그인을 한 후
Settings -> Developer settings -> Personal access tokens로 들어갑니다.

![](/assets/images/Jenkins_start_2-01.png)   

새로운 토큰의 이름과 원하는 스코프를 선택해 발급받고
빨간 박스로 가려둔 내용을 복사해 둡니다.

![](/assets/images/Jenkins_start_2-02.png)
- - -
![](/assets/images/Jenkins_start_2-03.png)
- - -
![](/assets/images/Jenkins_start_2-04.png)

다시 Jenkins로 돌아와서 `Jenkins 관리`에서, `시스템 설정` 메뉴로 들어갑니다.
![](/assets/images/Jenkins_start_2-05.png)

`Add Github Server` 눌러서 Server를 추가하고 원하시는 Name을 입력하시고 Credintial를 추가해줍니다.
![](/assets/images/Jenkins_start_2-06.png)

도메인과 종류를 바꾸고 Secret에 아까 복사에 둔 Github access token을 붙혀넣으면 됩니다.
ID에는 원하시는 ID 값을 입력하면 됩니다.
![](/assets/images/Jenkins_start_2-07.png)

Test connention을 눌러 정상적으로 작동되는지 확인할 수 있습니다.
![](/assets/images/Jenkins_start_2-08.png)