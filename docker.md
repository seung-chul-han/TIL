# 로컬에서 docker 돌려볼 때 상세한 오류를 보고 싶으면

```bash
docker build --tag support -f apps/support/docker/alpha/Dockerfile . 2>&1 | tee errorlog.txt
```

errorlog.txt파일로 로그를 남겨준다.


# Image 생성 오류 시
gyp Error발생
Python버전을 올리라는 오류 발생시
Docker 파일의
node 버전을 확인해 볼것
docker의 node 버전은 마이너 버전까지 픽스를 해야 됌
`node:20.10.0-alpine`에서 alpine는 경량화 버전이라는 뜻
.nvmrc의 버전도 같이 맞출것
