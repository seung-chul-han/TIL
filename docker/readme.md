# Docker

## 실습 환경 초기화

```sh
docker container rm -f $(docker container ls -aq)
```

## 내려받은 이미지가 차지한 용량 회수

```sh
docker image rm -f $(docker image ls -f reference='diamol/*' -q)
```

## flag

```sh
docker container run --interactive --tty diamol/base

# --interactive : 컨테이너에 접속된 상태
# --tty: 터미널 세션을 통해 컨데이너를 조작하겠다.


/ #    # 이것은 컨테이너 내부에 접속된 터미널 세션
```

```sh
# 현재 실행 중인 모든 컨테이너 정보를 확인
docker container ls

```

도커는 컨테이너를 실행할 때마다 무작위로 생성한 ID를 부여한다.
그리고 이 ID 값 중 일부분이 호스트명이 된다

```sh

# 대상 컨테이너에서 실행 중인 프로세스의 목록을 보여준다
# container ID => ab71f611da5c 에서 id의 앞 두글자만 사용해도 된다.
docker container top ab

# 대상 컨테이너에서 수집된 모든 로그 출력
docker container logs ab

# 대상 컨테이너의 상세한 정보를 보여준다.
docker container inspect ab

# 세션 종료
exit
```

```sh
# 상태와 상관없이 모든 컨테이너의 목록을 확인 한다
docker container ls --all
```

## 컨테이너가 백그라운드에서 동작하면서 네트워크를 주시(listen)하게 하려면 docker container run

뒤에 두개의 flag를 적용한다
--detach: 컨테이너를 백그라운드에서 실행하며 컨테이너 ID를 출력한다.
--publish: 컨테이너의 포트를 호스트 컴퓨터에 공개한다.

```sh
# 실행 중인 컨테이너의 상태를 확인할 수 있다.
docker container stats

# $()문법은  괄호 안 명력의 출력을 다른 명력으로 전달하는 역할
docker container rm --force $(docker container ls --all --quiet)
```

## 2.6 연습문제

```sh
# docker 실행
docker container run --detach --publish 8080:80 diamol/ch02-hello-diamol-web

# docker container의 상세 정보 보기
docker container instect <container ID>

# workingDir을 찾았다
# 하지만 직접 디렉토리에 접근을 못했다

# exec: 컨테이너에 명령어를 전달할 수 있게 해준다
# 현재 컨테이너 id에가 pwd라는 명령어를 전달
# pwd: 현재 경로를 알려달라
docker exec <container ID> pwd

# 현재 경로에 존재하는 파일 및 디렉토리 목록 출력
docker ls <container ID> ls

# htdocs안에 어떤 파일 및 폴더가 있는지 출력
docker exec <container ID> ls htdocs

# 현재 디렉토리에 있는 index.html을 htdocs의 index.html파일이 있는 위치로 복사 한다
docker cp index.html <container ID>:/usr/local/apache2/htdocs/index.html
```
