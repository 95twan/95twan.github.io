---
title: "Docker 시작하기(2) - 컨테이너와 이미지 다루기"
date: 2020-02-18 01:58:30 +0900
categories:
  - Docker
tags:
  - Docker
classes: wide
---

## Docker Container 다루기
- - -
**1. 도커 컨테이너 생성하기**   
실행하고 싶은 이미지를 [Docker Hub](https://hub.docker.com/)에서 찾거나 또는 이미지를 직접 만들어서 터미널을 열고
```shell
docker run [저장소/이미지 이름:태그]
```
를 입력합니다.   
`run` 명령어는 해당이미지가 로컬에 있지 않다면 이미지 저장소에서 이미지를 받고 해당 이미지를 사용해 컨테이너를 만들고 실행시킵니다.   

**2. 생성한 컨테이너 확인하기**   
터미널에 `docker ps`를 입력하면 현재 실행되고 있는 컨테이너 목록을 확인할 수 있습니다.   

![](/assets/images/docker_start/02-01.png)   

실행을 멈춘 컨테이너를 포함한 모든 컨테이너를 확인할 때는 `docker ps -a`를 사용합니다.   

![](/assets/images/docker_start/02-02.png)   

**3. 컨테이너 삭제**   
```shell
docker rm [컨테이너 아이디 또는 이름]
```
을 입력하면 컨테이너를 삭제할 수 있습니다.   

![](/assets/images/docker_start/02-03.png)   
![](/assets/images/docker_start/02-04.png)   

실행중인 컨테이너는 그냥 삭제할 수 없기 때문에 삭제하기전
```shell
docker stop [컨테이너 이름 또는 아이디]
```
로 컨테이너를 정지 한 뒤 삭제합니다.   
또는 `docker rm -f [컨테이너 이름 또는 아이디]`를 사용해 강제로 삭제할 수 있습니다.

## Docker 이미지 다루기
- - -
**1. 도커 저장소에 이미지 받고 받은 이미지 확인하기**   
도커 저장소에서 이미지를 받을 때는 `docker pull`을 사용해 이미지를 받을 수 있습니다.   
저장된 이미지들은 `docker images`로 확인할 수 있습니다.    

![](/assets/images/docker_start/02-05.png)   

**2. 기존의 컨테이너로 이미지 만들기**   
실행중인 컨테이너를 수정해 기존 이미지로부터 변경사항을 만든 후
```shell
docker commit [옵션] [기존 컨테이너] [생성될 이미지 이름]
```
으로 이미지를 만들 수 있습니다.   
`-m` 옵션을 사용하면 커밋 메세지를 남길 수 있습니다.

**3. 이미지 개인 저장소에 올리기**   
[Docker Hub](https://hub.docker.com/)에서 개인 저장소를 만들어 이미지를 저장 할 수 있습니다. 저장소의 이름은 `회원 이름/이미지 이름` 이기도 하고 저장될 이미지의 이름이기도 합니다.   
![](/assets/images/docker_start/02-06.png)   
올리고 싶은 이미지를 
```shell
docker tag [기존 이미지 이름] [새롭게 생성될 이미지 이름]
```
으로 만들어 놓은 저장소 이름으로 바꿉니다.   
그 후 개인 저장소에 올릴때는 login을 해야하기 때문에 터미널에 `docker login`을 입력해 로그인 후   
```shell
docker push [새롭게 생성된 이미지 이름]
```
을 입력하면 저장소에 저장이 됩니다.   
![](/assets/images/docker_start/02-07.png)

**4. 이미지 삭제하기**
```shell
docker rmi [이미지 아이디]
```
를 사용해 이미지를 삭제할 수 있습니다.

<br/>
<br/>
<br/>
<br/>

**참고:**
https://book.naver.com/bookdb/book_detail.nhn?bid=15917544