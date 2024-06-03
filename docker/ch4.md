# ch4

```sh
# AS 를 이용해 이름을 붙일 수 있다.
# 각 빌드 단계는 독립적으로 실행 된다.
FROM diamol/base AS build-stage
RUN echo 'Building....' > /build.txt 

FROM diamol/base AS test-stage
# --from 인자를 사용해host 컴퓨터의 파일 시스템이 아니라 이전 빌드 단계의 파일 시스템에
# 있는 파일음을 알려준다.
COPY --from=build-stage /build.txt /build.txt

# RUN은 빌드 중에 컨테이너 안에서 명령어를 실행한 다음
# 그 결과를 이미지 레이어에 저장하는 기능을 한다.
# RUN인스트럭션에서 실행할 수 있는 명령에는 특별한 제한은 없지만
# FROM인스트럭션에서 지정한 이미지에서 실행할 수 있는 것이어야 한다.
RUN echo 'Testing...' >> /build.txt

FROM diamol/base
COPY --from=test-stage /build.txt /build.txt
CMD cat /build.txt
```
