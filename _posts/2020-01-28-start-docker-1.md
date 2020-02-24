---
title: "Docker 시작하기(1) - Docker 설치 및 이미지와 컨테이너 개념"
date: 2020-01-28 17:40:30 +0900
categories:
  - Docker
tags:
  - Docker
classes: wide
---

## Docker란
- - -
도커는 컨테이너 기반의 오픈소스 가상화 플랫폼 입니다.    
컨테이너는 프로세스를 격리된 공간에서 동작하시키는 기술입니다.   
기존에 사용하던 VMware나 VirtualBox과 같은 가상머신에 Host OS 위에 Guest OS를 가상화하는 방식과는 다르게 추가적인 OS를 설치하지 않는 **프로세스 격리 방식**을 사용합니다.   

![](/assets/images/docker_start/01-01.png)   

**Docker를 사용하는 이유는**   
서버를 만들고 배포하다 보면은 서버의 OS마다 명령어와 환경이 다르기 때문에 고생을 하는 경우가 있습니다.   
하지만 해당 OS에 Docker를 설치하고 원하는 어플리케이션을 이미지로 만들어 컨테이너를 실행하면 간단하게 어플리케이션을 실행할 수 있습니다.   

## Docker 설치하기
- - -
**1. Mac에 설치하기**   

OSX나 Windows는 [Docker 홈페이지](https://www.docker.com/)에서 회원가입 후 간단하게 Docker for mac/windows 설치 파일을 받아 실행하면 간단하게 설치가 완료됩니다.   

설치가 완료되면 상단 바에 도커 아이콘을 확인할 수 있습니다.   

![](/assets/images/docker_start/01-02.png)   

그리고 터미널에 
```shell
docker -v
```
를 입력하면 도커 버전을 확인 할 수 있습니다.   

![](/assets/images/docker_start/01-03.png)   

**2. ununtu에 설치하기**   

apt 패키지를 업데이트 한 후 docker를 설치하기 위한 패키지들을 설치합니다.
```shell
apt-get update
apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

아래의 명령어로 도커의 공식 GPG 키와 저장소를 추가합니다.
```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

그 다음 아래 명령어로 도커 CE 버전을 설치합니다.
```shell
sudo apt update
sudo apt install docker-ce
```

마지막으로 sudo 명령어 없이 일반 사용자가 사용할 수 있도록 권한을 줍니다.
```shell
sudo usermod -aG docker $USER
```

설치 및 설정이 끝나고 `docker --version`으로 확인하면 현재 설치된 도커 버전이 나옵니다.   

## Docker 이미지와 컨테이너
- - -
**Docker 이미지**

이미지는 컨테이너를 만들때 필요한 요소이고 여러 레이어로 구성된 파일입니다.   
이미지의 이름은 기본적으로 **[저장소 / 이미지 이름 : 태그]** 의 형태 입니다.   
- 저장소: 이미지를 만들땐 저장소는 생략가능하며 저장소가 없는 이미지는 도커가 제공하는 이미지 저장소인 도커 허브의 공식 이미지 입니다.   
- 이미지 이름: 말그대로 이미지가 어떤 이미지인지 나타내는 역할을 합니다.   
- 태그: 이미지의 버전 관리에 사용되고 생략하면 docker가 자동으로 latest로 인식합니다.   

**Docker 컨테이너**

원하는 이미지를 선택해 컨테이너를 생성하면 격리된 시스템 자원을 사용할 수 있는 독립된 공간이 만들어집니다.    
하나의 이미지로 여러개의 컨테이너를 만들 수 있고 만들어진 컨테이너로 무엇을 하든지 원본 이미지에는 아무런 영향도 미치지 않습니다.    
또한 저장공간을 따로 공유하지 않는 이상 특정 컨테이너에서 프로그램을 설치하거나 삭제해도 다른 컨테이너에 영향을 미치지 않습니다.  

<br/>
<br/>
<br/>
<br/>

**참고:**
https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html
https://hiseon.me/linux/ubuntu/install-docker/
https://book.naver.com/bookdb/book_detail.nhn?bid=15917544

