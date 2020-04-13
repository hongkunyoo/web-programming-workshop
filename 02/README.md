# Linux 기초


## 리눅스 OS란?

- 데스크탑용 OS: Windows OS 많이 사용
- 서버용 OS: 리눅스 OS 많이 사용

리눅스는 정확히는 OS 이름이 아니라 Kernel 이름임. 리눅스 진영에는 다양한 배포판이 존재.
- Ubuntu
- CentOS
- RedHat
- Mint
- Debian
- 등등 수 없이 많음.

한가지 배포판만 잘 사용하면 나머지는 쉽게 확장할 수 있음. 해당 워크샵에서는 Ubuntu (우분트) 리눅스를 기준으로 사용할 예정
Ubuntu 18.04 (18.04는 우분트 OS의 버전 이름이 Windows XP, 7, 10 등, 18년도에 나온 버전을 의미)


## 리눅스 접속 방법

ssh 프로토콜을 이용하여 접속. ssh도 클러이언트, 서버 구조로 되어 있다.

1. ssh 클라이언트 설치 - [MobaXterm](https://mobaxterm.mobatek.net/)
2. Session 버튼 클릭
3. SSH 클릭
4. Remote host
5. Specifiy username
6. OK
7. 세션 더블클릭


## 리눅스 기본 개념

### 유저 관리
리눅스는 개인적으로 사용하는 OS라기 보단 여러 사람이 같이 사용하는 OS라 유저 관리가 윈도우에 비해 멀티 유저 개념이 더 강하다.

- 나의 홈 폴더: `/home/<USER>` - 윈도우를 생각하자면 나의 바탕화면 정도
- `whoami`: 접속한 유저가 누군지 확인	

### 파일시스템
리눅스는 모든 것이 파일시스템으로 이루어져 있다. 프로세스끼리의 통신, 파일공유, 메모리 공유가 전부 파일 시스템으로 이루어진다.

### 프로세스
프로그램을 실행하면 프로세스라는 것이 생성된다. 이것은 프로그램이 메모리 위에 로딩된 상태로 볼 수 있다.

### 실행 파일 (executable file)
파일 중에 실행할 수 있는 파일이 존재한다. 윈도우의 exe 파일과 유시하게 프로그램을 실행시킬 수 있다. 이것을 실행 파일이라고 부른다.



## 리눅스 기초 명령어

### ls
파일 디렉토리 구조를 리스팅한다.

```bash
ls
ls -alh
ls -alh /home
```

### pwd

현재 working 디렉토리를 보여준다.

```bash
pwd
```

### cd

working 디렉토리를 이동시켜준다.

```bash
cd /home
pwd
ls -alh
```

### cat
특정 파일을 읽는다.

```bash
cat .bashrc
```

### echo
std (표준 출력)으로 글자를 출력한다.

```bash
echo abc
```

### redirection (>>)
출력값을 std (표준 출력)에서 다른 파일로 이동 시킨다.

```bash
# >> 이 redirection 명령임
echo abc >> abc.txt  # append    (추가하기)
echo abc > abc.txt   # overwrite (덮어쓰기)
```

### ps
현재 실행 중인 프로세스 리스팅

```bash
ps
ps aux
```

### grep
특정 문자열을 잡는다. (grep)

```bash
ps aux | grep ssh
```

### cp
파일 복사

```bash
cp abc.txt 123.txt
cat 123.txt
```

### mv
파일 옮기기

```bash
mv 123.txt 123.txt.moved
```

### chown
파일 소유자 수정

```bash
ls -alh .
chown ubuntu abc.txt

ls -alh .
```

### sudo
root 권한을 부여 받아서 실행

```bash
ls -alh .
sudo chown ubuntu abc.txt
ls -alh .
```

### chmod
파일 권한 수정

```bash
ls -alh .
chmod 777 abc.txt
ls -alh .
```

```bash
-rwxrwxrwx
```

- 첫번째: 디렉토리 or 파일
- `rwx`: Owner 권한
- `rwx`: Group 권한
- `rwx`: Other 권한


### which
실행 파일의 위치를 알 수 있음

```bash
which ls

ls -alh /bin/sh
```

### mkdir
폴더 생성

```bash
mkdir test_dir
```

### tar
zip 압축 생성/풀기

```bash
tar -cvf test_dir.tar test

tar -xvf test_dir.tar
```

### date
현재 날짜 출력

```bash
date
```

### bash

실행 파일 실행

```bash
echo "date; echo abc" > date.sh

bash date.sh
```


### curl

http 통신할 수 있게 해주는 client

```bash
curl naver.com
```

### apt

새로운 패키지 설치하게 해주는 명령 (google play 스토어, apple app store 같은 역할)

```bash
sudo apt update

sudo apt install curl
```

### wget

인터넷상의 파일 다운로드

```bash
wget "https://news.naver.com/main/read.nhn?mode=LSD&mid=shm&sid1=100&oid=047&aid=0002266113"
```

### ssh

ssh 접속할 수 있는 client

```bash
ssh USER@HOST
```


## 리눅스 확장


### VIM 사용법

리눅스 editor (eclipse, jetbrain과 같은 에디터)

#### Mode

- normal 모드: `esc` 진입
- edit 모드: `i` 진입
- command 모드: `:` 진입


### 환경변수 (environment variable)

OS나 특정 프로세스에서 어떤 임의의 값을 전달할 수 있는 메커니즘. (자주 사용함)

```bash
# vim env-test.sh

echo $my_env
date
ls
```

```bash
my_env=123 bash env-test.sh
```

```bash
my_env=123
echo $abc
```

### tmux 사용법

Terminal MUltipleXer라고 하며 한개 화면을 여러개로 분할 시켜서 볼 수 있게 해준다.


#### 세팅
먼저 아래와 같이 tmux 세팅을 해준다.

```bash
vim ~/.tmux.conf
```

```bash
set -g default-terminal "xterm-256color"
setw -g xterm-keys on
setw -g mode-keys vi
set -g prefix C-a
unbind C-b
bind C-a send-prefix

bind '"' split-window -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"
bind c new-window -c "#{pane_current_path}"

set -g history-limit 100000
set -g base-index 1
setw -g pane-base-index 1
set -g status-fg green
set -g status-bg black
```

#### 사용법

```bash
# 실행
tmux 

# 화면 나누기 (가로)
# ctrl + A + "

# 화면 나누기 (세로)
# ctrl + A + %   

# 화면간 이동
# ctrl + A + 이동커서

# tmux 임시 탈출
# ctrl + A + d

# tmux 다시 attach
tmux a

# tmux 종료
# tmux 안에 있는 상태에서
exit
```


## nginx 설치해보기

### nginx란?
html파일과 같은 웹 페이지를 제공해주는 웹 서버


### 설치 방법

```bash
sudo apt update && sudo apt install -y nginx
curl localhost
```

### 웹 사이트 수정

```
# 내 마음대로 바꾸기
sudo vim /var/www/html/index.nginx-debian.html

```






nslookup
systemctl
crontab