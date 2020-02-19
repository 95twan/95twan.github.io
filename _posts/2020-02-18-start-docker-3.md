---
title: "Docker 시작하기(3)"
date: 2020-02-18 02:59:30 +0900
categories:
  - Docker
tags:
  - Docker
classes: wide
---

## Dockerfile이란
- - -
앞 포스팅에서는 이미지를 만들기 위해 기존 컨테이너 안에서 직접 수정 후 커밋을 통한 새로운 이미지를 만드는 것이었습니다.   
이러한 방식은 일일이 직접 컨테이너 안에서 파일을 받고 프로그램을 설치하는 번거로움이 있습니다.   
도커는 이런 과정을 손쉽게 기록할 수 있는 **Dockerfile** 과 이 Dockerfile을 빌드 해 이미지로 만들어주는 `build`명령어가 있습니다.   
따라서 일일이 컨테이너 안에서 변경을 하는 것보다 Dockerfile에 변경사항들을 작성해 번거로움을 줄일 수 있고 개발 툴을 이용해 Dockerfile을 가지고 빌드 및 배포를 자동화 할 수 있습니다.

## Dockerfile 작성해보기
- - - 
우분트에 아파치 웹 서버를 설치하고, 로컬의 test.html을 컨테이너 /var/www/html 디렉토리에 복사하는 Dockerfile은 아래와 같습니다.   
도커의 `build` 명령어는 자동으로 현재 디렉토리의 Dockerfile을 찾아 빌드하기 때문에 파일 명은 Dockerfile로 했습니다.   

    FROM ubuntu:14.04
    LABEL owner="95twan"
    RUN apt-get update
    RUN apt-get install apache2 -y
    ADD index.html /var/www/html
    EXPOSE 80
    CMD apachectl -DEOREGROUND

명령어를 하나씩 살펴보면   
- FROM: 생성할 이미지의 베이스가 되는 이미지 입니다. 현재 베이스 이미지는 ubuntu입니다.   
- LABEL: 이미지에 메타데이터를 추가합니다. '키=값' 형태로 저장됩니다.   
- RUN: 이미지를 만들때 컨테이너 내부에서 실행할 명령어 입니다.   
- ADD: 파일을 이미지에 추가합니다. Dockerfile이 존재하는 디렉토리의 index.html을 컨테이너의 /var/www/html로 추가합니다.     
- EXPOSE: 이미지에서 노출할 포트를 설정합니다.    
- CMD: 컨테이너를 시작할 때마다 실행할 명령어 입니다.    

다음은 파이썬 Django로 만든 웹 어플리케이션을 image로 만든 것 입니다.   

    FROM python:3.7.4
    WORKDIR /DVBGServer
    COPY requirements.txt /DVBGServer
    RUN pip install -r requirements.txt
    COPY . /DVBGServer
    EXPOSE 8000
    CMD ["uwsgi", "--http", "0.0.0.0:8000", "--module", "DVBG.wsgi"]

- WORKDIR: 명령어를 실행할 위치를 나타냅니다. 셀의 cd 명령어와 비슷합니다. 디렉토리를 변경했기 때문에 RUN은 DVBGServer 디렉토리에서 실행됩니다.   
- COPY: ADD와 비슷한 역할은 합니다. 다만 COPY는 로컬의 파일만 추가할 수 있고 ADD는 외부 URL, tar 등 외부 파일을 추가할 수 있습니다.   

COPY, ADD, RUN, CMD는 위의 Django처럼 JSON 배열의 형태로 사용할 수 있습니다.   
CMD ["명령어", "인자 1", "인자 2", ...]  
ADD나 COPY를 통해 여러 파일은 한번에 추가할 때 그 중에 이미지에 추가하고 싶지 않은 파일이 있을 수 있습니다.   
그때에는 .gitignore와 비슷한 .dockerignore를 작성해 image에 담고싶지 않는 파일을 제외합니다.   

## Dockerfile 빌드하고 샐행하기
- - -
Dockerfile이 있는 디렉토리에서 `docker build -t firstbuild:0.1 ./`로 빌드가 가능합니다.   
끝에 `./`는 Dockerfile이 저장된 경로를 입력합니다.   
`-t`옵션은 생성될 이미지의 이름을 입력할 수 있습니다.  
만약 Dockerfile의 이름을 Dockerfile2라는 이름으로 만든다면 `-f Dockerfile2`옵션을 사용해 파일 이름을 지정해 사용할 수 있습니다.   
`docker run -d -P --name firstserver firstbuild:0.1`로 컨테이너를 실행해봅시다.   
`-d`옵션은 detached 모드로 컨테이너를 실행합니다
`-P`옵션은 EXPOSE에 설정한 포트 번호와 호스트에서 사용 가능한 포트에 연결 됩니다. 하지만 호스트의 몇번포트와 연결됬는지 알 수 없기 때문에 `docker port firstserver`로 확인해야합니다.   
원하는 포트에 연결하고 싶을 때는 `-p 8000:8000`으로 명시할 수 있습니다.   
`--name` 컨테이너의 이름을 정합니다. 사용하지 않으면 랜덤으로 이름이 정해집니다.   







