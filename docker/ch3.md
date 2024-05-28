# Ch 3

```sh
docker container run -d --name web-ping diamol/ch03-web-ping

# --name : 컨테이너에 원하는 이름을 붙이고 이 이름으로 컨테이너를 지칭할 수 있다
```

## 환경변수

운영체제에서 제공하는 키-값 쌍.
도커 컨테이너도 별도의 환경변수를 가질 수 있다. 그러나 이 환경변수는 호스트 운영체제의 것을 가져오는 것이 아닌
컨테이너의 호스트명이나 IP 주소처럼 도커가 부여해 준다.

## Dockerfile

애플리케이션을 패키징하기 위한 간단한 스크립트
일련의 인스트럭션(FROM, ENV, WORKDIR, COPY, CMD)으로 구성되어 있다.
인스트럭션은 소문자로 작성해도 무방하다.

```
# FROM: 모든 이미지는 다른 이미지로부터 출발한다. 이 이미지는 diamol/node이미지를 시작점으로 지정
# diamol/node 이미지에는 web-ping 애플리케이션을 실행하는 데 필요한 런타임인 Node.js가 설치돼 있다.
FROM diamol/node

# ENV: 환경 변수 값을 지정하기 위한 인스트럭션
ENV TARGET='blog.six.com'
ENV METHOD="HEAD"
ENV INTERVAL="3000"

# WORKDIR: 컨테이너 이미지 파일 시스템에 디렉터리를 만들고, 해당 디렉터리를 작업 디렉터리로 지정하는 인스트럭션
WORKDIR /web-ping

# COPY: 로컬 파일 시스템의 파일 혹은 디렉터리를 컨테이너 이미지로 복사하는 인스트럭션
# [원본경로] [복사경로] 형식으로 지정
# 이 파일은 로컬 파일 시스템의 app.js파일을 이미지의 작업 디렉터리로 복사
COPY app.js .

# CMD: 도커가 이미지로부터 컨테이너를 실행했을 때 실행할 명령을 지정하는 인스트럭션
# 여기서는 node.js 런타임이 애플리케이션을 시작하도록 app.js를 지정했다.
CMD ["node", "/web-ping/app.js"]

```

## 컨테이너 이미지 빌드

이미지를 빌드하려면 `Dockerfile`, `이미지의 이름`, `패키징에 필요한 파일의 경로`

```sh
# --tag의 인잣값(web-ping)은 이미지 이름, 이어지는 인자는 Dockerfile 및 이미지에 포함시킬 파일이 위차한 경로
# 도커에서는 이 디렉터리를 컨텍스트라고 한다. 마지막 .은 현재 작업 디렉터리 라는 뜻
docker image build --tag web-ping .
```

빌드 명령에서 오류 발생시

- 도커 엔진이 정상 동작 중인지 확인
- 현재 작업 디렉터리가 정확한지
- 빌드 명령을 정확하게 입력했는지

```sh
# w로 시작하는 태그명을 가진 이미지 목록을 확인하라.
docker image ls 'w*'
```

## 도커 이미지와 이미지 레이어 이해하기

도커 이미지에는 우리가 패키징에 포함시킨 모든 파일이 들어 있다.
이들 파일은 나중에 컨테이너의 파일 시스템을 형성한다.
이 외에도 이미지에는 자신에 대한 여러 메타데이터 정보도 들어있다.
이 정보 중에는 이미지가 어떻게 빌드됐는지에 대한 간단한 이력도 포함.
(이를 이용하면 이미지를 구성하는 각 레이어는 무엇이고 이들 레이어가 어떤 명령으로 빌드 됐는지 알 수 있다.)

```sh
docker image history web-ping
```

도커 이미지는 이미지 레이어가 모인 논리적 대상이다. 레이어는 도커 엔진의 캐시에 물리적으로 저장된 파일이다.
이미지 레이어는 여러 이미지와 컨테이너에서 공유되기 때문이다. 만약 Node.js 애플리케이션이 실행되는 컨테이너를 여러 개 실행한다면
이들 컨테이너는 모두 Node.js 런타임이 들어 있는 이미지 레이어를 공유한다.

```sh
docker image ls

# SIZE에 나온 용량은 이미지의 논리적 용량으로 공유된 레이어의 용량이 반영 되지 않은 것
REPOSITORY             TAG       IMAGE ID       CREATED          SIZE
web-ping               latest    8b5070429163   18 minutes ago   75.5MB
diamol/ch03-web-ping   latest    bfce5d697312   3 years ago      75.5MB
```

```sh

# 이미지 저장에 실제 사용된 디스크 용량 확인
docker system df

TYPE            TOTAL     ACTIVE    SIZE      RECLAIMABLE
Images          2         2         75.49MB   75.49MB (99%)
Containers      2         0         0B        0B
Local Volumes   0         0         0B        0B
Build Cache     22        0         5.533MB   5.533MB
```

## Dockerfile 스크립트 최적화

Dockerfile을 수정하고 이미지를 다시 빌드하면 새로운 이미지 레이어가 생긴다.
도커의 이미지 레이어가 특정 순서대로만 배치된다고 가정한다. 그래서 이 순서 중간에 있는
레이어가 변경되면 변경된 레이어보다 위에 오는 레이어를 재사용할 수 없다.

Dockerfile 스크립트의 인스트럭션은 각각 하나의 이미지 레이어와 1:1로 연결된다.
그러나 인스트럭션의 결과가 이전 빌드와 같다면, 이전에 캐시된 레이어를 재사용 한다.

도커는 캐시에 일치하는 레이어가 있는지 확인하기 위해 해시를 사용
일치 하는 해시값이 없으면 캐시 미스가 발생하고 해당 인스트럭션이 실행되고 이후 오는 인스트럭션은 수정된 것이 없어도 모두 실행된다.

이런 이유로 잘 수정하지 않는 인스트럭션은 앞으로
자주 수정되는 인스트럭션이 되에 오도록 배치

위 Dockerfile의 인스트럭션은 7개 이지만 최적화 할 수 있다.

- CMD 인스트럭션은 스크립트 마지막에 둘 필요가 없다. FROM 인스트럭션 뒤라면 어디든 가능하다. 또한 수정할 일이 잘 없을 것이므로 초반부에 배치
- ENV 인스트럭션은 하나로 여러 개의 환경 변수 정의 가능

```Dockerfile
FROM diamol/node
CMD ["node", "web-ping/app.js"]

ENV TARGET="bloc.sixeyed.com" \
    METHOD="HEAD" \
    INTERVAL="3000"

WORKDIR "web-ping"
COPY app.js .
```