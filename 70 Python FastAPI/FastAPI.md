- https://ithelp.ithome.com.tw/m/users/20162280/ironman/6767
- https://minglunwu.com/notes/2021/fast_api_note_1.html/
 


apt search fastapi, ivucorn
install python3-fastapi python3-uvicorn uvicorn
vi main.py
```
from fastapi import FastAPI
app=FastAPI()
@app.get("/")
async def root():
    return {"Message":"Hello FastAPI world"}
```
啟動 Server (default 8000)  docker 要設mapping
```
uvicorn main:app --host 0.0.0.0 --port 5000 --reload
```

