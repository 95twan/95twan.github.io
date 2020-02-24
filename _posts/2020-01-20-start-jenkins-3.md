---
title: "Jenkins로 배포자동화 하기(3) - github webhook으로 젠키스 빌드 자동화"
date: 2020-01-20 20:55:30 +0900
categories:
  - Jenkins
tags:
  - Jenkins
  - Github
  - CI/CD
  - 배포 자동화
classes: wide
---

## New Item 생성
- - -
Jenkins 메인에서 새로운 Item을 선택합니다.   
Item 이름을 입력하고 `Freestyle project`를 선택합니다.   

![](/assets/images/Jenkins_start/3-01.png)   

GitHub project를 선택해주시고 Project url에
자신이 배포하고 싶은 레파지토리 url을 입력합니다.   

![](/assets/images/Jenkins_start/3-02.png)   

아래 소스 코드 관리에서 Git을 선택해주시고
Repository URL에 clone에 쓰이는 url을 입력해줍니다.   
Branch는 원하는 것으로 바꿔주고
Credentials에 Add버튼을 클릭합니다.   

![](/assets/images/Jenkins_start/3-03.png)   

Kind를 `Username and password`로 선택하고
Username에 자신의 github 아이디를 password에는 github 비밀번호를 입력합니다.   
ID는 원하는 값을 입력합니다.   

![](/assets/images/Jenkins_start/3-04.png)   

빌드 유발에서 `Github hook trigger for GITScm polling`을 체크해주시고
빌드와 빌드 후 조치는 자신이 개발하고 있는 언어나 배포 환경에 맞게 작성해주면 됩니다.   

![](/assets/images/Jenkins_start/3-05.png)   

## Github Repository hook 설정
- - -
마지막으로 Item에 적은 github repository에 Settings -> Webhooks 페이지로 들어갑니다.   
Add webhook 버튼을 눌러 새로운 webhook을 만들어 줍니다.   
URL은 자신의 컴퓨터에 접근 할 수 있는 외부IP를 적어주시고 뒤에 /github-webhook/ 을 붙여줍니다.   
type은 json타입으로 바꿔주시고 event는 push할 때만 hook을 쏠거기 때문에 `Just the push event.`를 선택해 주면 끝납니다.   

![](/assets/images/Jenkins_start/3-06.png)   

해당 branch로 push를 테스트 해보면
github에서는 초록색 체크가 나오면 정상적으로 보내진겁니다.   
그리고 Jenkins에서는 자동으로 빌드가 시작됩니다.   

![](/assets/images/Jenkins_start/3-07.png)   

![](/assets/images/Jenkins_start/3-08.png)   
