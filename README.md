# FastAPI tutorial

## Install FastAPI

pip를 이용해서 `fastapi` 와 `uvicorn` 을 설치합니다.

```bash
pip install fastapi uvicorn
```

## Hello World

`GET /` 요청 시 `Hello World` 를 응답하는 코드를 작성합니다.

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```

### FastAPI 실행 명령어

`uvicorn` 을 통해 FastAPI를 실행합니다.

```bash
uvicorn --host 0.0.0.0 --reload main:app
```

---

## Deploy

프로세스 매니저를 통해 배포할 수 있습니다.

`Supervisor` 를 설치합니다.

```bash
apt install supervisor
```

`/etc/supervisor/conf.d/fastapi.conf` 파일을 작성합니다.

```bash
[fcgi-program:fastapi]
socket=tcp://0.0.0.0:8000
directory=/home/ubuntu/PlayFastAPI
command=uvicorn --fd 0 main:app
user=ubuntu
autostart=true
autorestart=true
```

`supervisor` 에서 등록한 서비스를 읽고 실행합니다.

```bash
supervisorctl reread # 등록된 서비스를 읽습니다.
supervisorctl update # 등록된 서비스를 supervisor에 추가합니다.
---
supervisorctl status {서비스}  # 서비스의 상태를 확인합니다.
supervisorctl stop {서비스}    # 서비스를 중지합니다.
supervisorctl start {서비스}   # 서비스를 실행합니다.
supervisorctl restart {서비스} # 서비스를 재실행합니다.
```

---

## 참고 URL

---

## 참고 URL

>   [FastAPI](https://fastapi.tiangolo.com)
>
>   [Uvicorn Deployment](https://www.uvicorn.org/deployment/)