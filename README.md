# FastAPI tutorial

## Install FastAPI

```bash
pip install fastapi uvicorn
```

## Hello World

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```

### FastAPI 실행 명령어

```bash
uvicorn --host 0.0.0.0 --reload main:app
```

