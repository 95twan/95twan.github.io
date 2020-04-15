---
title: "HTTP 통신"
date: 2020-04-15 19:14:30 +0900
categories:
  - network
tags:
  - http
  - https
classes: wide
---

## 1. HTTP란

- Hypertext Transfer Protocol의 약자로 인터넷상에서 클라이언트와 서버간 데이터를 주고받기 위한 통신 규약을 말한다.
- HTTP는 텍스트 교환 형식이므로 누군가 해당 텍스트를 중간에 가로채면 내용이 노출 될 수 있다.
- 기본 PORT는 80번 PORT를 사용하고 있다.

## 2. HTTPS와의 차이점

- HTTP의 보안이 강화된 버전이다.
- HTTPS는 통신에서 일반 텍스트를 이용하는 대신에, SSL이나 TLS 프로토콜을 통해 세션 데이터를 암호화해 데이터를 보호해 준다.
- 기본 PORT는 443번 PORT를 사용하고 있다.

## 3. SSL이란

- SSL(Secure Socket Layer) 프로토콜은 처음에 웹서버와 브라우저 사이의 보안을 위해 만들었다. SSL은 Certificate Authority(CA)라 불리는 서드 파티로부터 서버와 클라이언트의 인증을 하는데 사용된다.
- SSL이 작동하는 방법을 짧게 요약하면
  1. 클라이언트가 SSL로 암호화된 페이지를 요청한다.
  2. 서버는 Public Key를 인증서와 함께 전송한다.
  3. 클라이언트의 인증서가 자신이 신용있다고 판단한 CA로부터 서명된 것인지 확인한다. 또한 날짜가 유효한지, 그리고 인증서가 접속하려는 사이트와 관련되어 있는지 확인한다.
  4. 클라이언트의 Public Key를 사용해서 랜덤 대칭 암호화키를 비릇한 URL, http 데이터들을 암호화해서 전송한다.
  5. 서버의 Private Key를 이용해서 랜덤 대칭 암호화키와 URL, http 데이터를 복호화한다.
  6. 서버가 요청받은 URL에 대한 응답을 웹브라우저로부터 받은 랜덤 대칭 암호화키를 이용하여 암호화해서 브라우저로 전송한다.
  7. 클라이언트가 대칭 키를 이용해서 http 데이터와 html문서를 복호화하고, 화면에 정보를 뿌려준다.

## 4. HTTP 통신 과정

1. 클라이언트가 URL 주소로 요청을 보낸다.
2. 클라이언드가 입력한 URL 주소 중에서 도메인 네임을 DNS 서버에서 검색한다.
3. DNS 서버에서 해당 도메인 네임에 해당하는 IP 주소를 찾아 사용자가 입력한 URL 정보와 함께 전달한다.
4. URL 정보와 전달받은 IP 주소는 HTTP 프로토콜을 사용하여 HTTP 요청 메시지를 생성한다.
5. HTTP 요청 메시지는 TCP 프로토콜을 사용하여 인터넷을 거쳐 해당 IP 주소의 서버로 전송된다.
6. 도착한 HTTP 요청 메시지는 HTTP 프로토콜을 사용하여 URL 정보로 변환된다.
7. 서버는 도착한 URL 정보에 해당하는 데이터를 응답한다.
8. 서버는 데이터를 다시 HTTP 프로토콜을 사용하여 HTTP 응답 메시지를 생성한다.
9. HTTP 응답 메시지는 TCP 프로토콜을 사용하여 인터넷을 거쳐 클라이언트로 전송된다.
10. 도착한 HTTP 응답 메시지는 HTTP 프로토콜을 사용하여 데이터로 변환된다.

## 5. HTTP 메세지 형식

1. HTTP 요청 메세지 형식

   ```
   GET /api/board/ HTTP/1.1
   Host: 15.165.206.181:8000
   Content-Type: application/json
   ```

   - 헤더
     - 첫번째 줄은 요청 메서드(ex. GET, POST) + 요청 URI + HTTP 프로토콜 버전
     - 두번째 줄부터 헤더 정보들
   - 빈 줄
     - 요청에 대한 모든 메타 정보가 전송된걸 알리는 빈 줄이 삽입된다.
   - 바디
     - GET, HEAD, DELETE, OPTIONS처럼 리소스를 가져오는 요청은 보통 본문이 필요없다.
     - 요청에 필요한 데이터

2. HTTP 응답 메세지 형식

   ```
   HTTP/1.1 200 OK
   content-length: 212
   content-type: application/json
   x-content-type-options: nosniff
   x-frame-options: DENY

   [
       {
           "id": 1,
           "name": "test1",
           "is_hidden": false,
           "created_at": "2020-01-24T23:45:06Z",
           "deleted_at": null
        },
       {
        "id": 6,
        "name": "test2",
        "is_hidden": false,
        "created_at": "2020-02-06T11:40:33Z",
        "deleted_at": null
       }
   ]
   ```

   - 상태줄
     - HTTP 프로토콜 버전 + 응답 코드 + 응답 메시지
   - 헤더
     - 헤더 정보들
   - 빈 줄
     - 요청에 대한 모든 메타 정보가 전송된걸 알리는 빈 줄이 삽입된다.
   - 바디
     - 실제 응답 데이터

<br/>
<br/>
<br/>
<br/>

**참고:**

1. https://gmlwjd9405.github.io/2019/04/17/what-is-http-protocol.html
2. https://developer.mozilla.org/ko/docs/Web/HTTP/Session
3. http://tcpschool.com/webbasic/works
