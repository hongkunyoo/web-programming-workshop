# 웹 프로그래밍 기초

## 웹 서버 구조

![](https://media.geeksforgeeks.org/wp-content/uploads/20190927155217/webserver.png)


### 클라이언트 - 서버

- 클라이언트: 요청을 보내는 주체 --> Request
- 서버: 요청에 대해서 응답을 보내는 주체 --> Response

#### Asynchronous vs Synchronous

![](https://camo.githubusercontent.com/a05fd290b0ad342a6721ca3fc66d7ed65c004fa4/68747470733a2f2f63646e2d696d616765732d312e6d656469756d2e636f6d2f6d61782f313630302f312a36306975674742484d46375050536e2d6664517248512e706e67)


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
5. verb (동사)가 있음
	- GET
	- POST
	- PUT
	- DELETE
	- PATCH

![](https://blog.catchpoint.com/wp-content/uploads/2017/09/header6.jpg)
