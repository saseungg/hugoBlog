---
title: "[TIL] 230220-230226"
date: 2023-02-20T11:50:00+09:00
categories:
  - TIL
tags:
  - TIL
---

# 2/20

## MySQL character set 변경

도커로 mysql 설치, 실행 후 bash 접속하여 locale 설정 후 'my.cnf'파일을 수정하여 utf-8로 변경하려고했으나 vim 명령이 안먹음. 추가적으로 vim install, apt update를 했으나 command not found가 나왔다. (vim 설치, apt 업데이트 적용 안됨)

{{< image src="https://user-images.githubusercontent.com/115215178/220033824-ad97f7ef-3d57-40fe-a2e2-e64acc08bfcc.png" caption="터미널 화면 캡쳐" width="50%" >}}

다른 해결 방안으로 도커 컨테이너를 실행하면서 utf-8로 설정해줄 수 있도록 명령어를 입력했다.

```
docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=password mysql:5.7 --character-set-server=utf8 --collation-server=utf8_general_ci
```

아래와 같이 입력 후 mysql 서버 접속 후 status를 확인해보면 server, db characterset은 utf-8로 나오지만 클라이언트는 latin1으로 되어있어서 추가적으로 아래와 같이 명령어를 입력하여 최종적으로 utf-8로 변경할 수 있었다.

```
mysql> SET NAMES 'utf8';
```

{{< image src="https://user-images.githubusercontent.com/115215178/220034637-2a2cd85f-6db6-4417-bc9e-6a5244fdb207.png" caption="utf-8로 전부 변경됐다." width="50%" >}}
