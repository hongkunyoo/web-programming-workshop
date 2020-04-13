# 웹 프로그래밍 기초

## 웹 서버 구조

![](https://media.geeksforgeeks.org/wp-content/uploads/20190927155217/webserver.png)


### 클라이언트 - 서버

- 클라이언트: 요청을 보내는 주체 --> Request
- 서버: 요청에 대해서 응답을 보내는 주체 --> Response

#### Asynchronous vs Synchronous

![](https://camo.githubusercontent.com/a05fd290b0ad342a6721ca3fc66d7ed65c004fa4/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f313630302f312a36306975674742484d46375050536e2d6664517248512e706e67)

### 웹 프론트 vs 웹 백엔드

보통 클라이언트단에서 실행되는 프로그램을 웹 프론트, 서버단에서 실행되는 프로그램을 백엔드라고 부른다.

- 웹 프론트의 대표적인 언어로, html, css, javascript가 있다.
- 백엔드 언어로는 다양하게 존재한다. java, javascript, python, ruby, php, go 등 다양하다. 본 워크샵에서는 파이썬을 기준으로 설명한다.


### 웹, 앱, DB 서버

![](https://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/images/inst_top_was_nd_sa_1machine_en.gif)

- 웹 서버: 실제 클라이언트 브라우저에서 스크립트가 실행되나 앱 서버에서 스크립트를 제공함
- 앱 서버: 백엔드 로직이 동작하는 서버
- DB 서버: 데이터를 저장하는 서버 (RDB, mongoDB 등)


### IP, PORT

IP: 인터넷상의 호스트를 찾는 식별자
PORT: 동일한 호스트 내에서 특정 프로세스를 찾는 식별자

#### Private vs Public IP

- Private IP: 특정 네트워크 안에서만 접근 가능한 IP
- Public IP: 전세계 어디서나 접근 가능한 IP


### HTTP란?

1. 네트워크 프로토콜 중에 하나
2. http 뿐만 아니라 samba, nfs, sftp 등 다른 프로토콜도 많지만 가장 많이 알려진 프로토콜
3. text 기반 (다른 프로토콜은 Request와 Response가 텍스트가 아닌 binary (01010110) 혹은 hex (0FFA9C) 인 경우도 있지만 http는 Request와 Response 둘다 텍스트임)
4. Header와 Body로 이루어짐
5. http method (혹은 verb - 동사)
	- GET
	- POST
	- PUT
	- DELETE
	- PATCH

![](https://blog.catchpoint.com/wp-content/uploads/2017/09/header6.jpg)
