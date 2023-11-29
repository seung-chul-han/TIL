# 로컬에서 docker 돌려볼 때 상세한 오류를 보고 싶으면

```bash
docker build --tag support -f apps/support/docker/alpha/Dockerfile . 2>&1 | tee errorlog.txt
```

errorlog.txt파일로 로그를 남겨준다.
