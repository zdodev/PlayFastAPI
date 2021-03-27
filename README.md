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

## Deploy

---

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

## Path Paramters

경로에 파라미터를 전달할 수 있으며, 서버에서 받아서 사용할 수 있습니다.

```python
@app.get("/items/{item_id}")
async def read_item(item_id):
    return {"item_id": item_id}
```

### Path parameters with types

파라미터에 타입을 지정할 수 있습니다.

```python
@app.get("/items/{item_id}")
async def read_item(item_id: int):
    return {"item_id": item_id}
```

### Older matter

파라미터를 전달받는 함수와 고정 경로를 지정한 함수의 코드 위치에 따라 실행여부가 달라질 수 있습니다.

```python
@app.get("/users/me")
async def read_user_me():
    return {"user_id": "the current user"}


@app.get("/users/{user_id}")
async def read_user(user_id: str):
    return {"user_id": user_id}
```



---

## 참고 URL

>   [FastAPI](https://fastapi.tiangolo.com)
>
>   [Uvicorn Deployment](https://www.uvicorn.org/deployment/)