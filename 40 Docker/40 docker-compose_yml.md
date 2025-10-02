# docker-compose.yml 用來建立 Container 容器

```
docker compose buile  #依照 Dockerfile 建立 Image, 依照 yml 裡面來命名
docker compose up     #依照 yml 建立容器, 並執行命令, ctrl-c跳出 停止

docker compose up --build     #同時建立Image 與 Contrainer容器
docker compose up --build -d  #背景執行 不跳出
docker logs -f                #看output

docker down                   #停止 容器
```


## 如下 sample 
```yml
# Docker Compose 檔案版本
#version: '3.8'

services:
  # 我們的 FastAPI 應用程式服務 (整合前後端)
  backend:
    # 上面會是 Image 名,前面會自動加一層 DIR 名, 如: mydir-backeng
    # 告訴 Docker Compose 使用當前目錄的 Dockerfile 來建立映像檔
    build: .
    container_name: sql_web
    # 上面是 Container 名
    # 將主機的 8000 埠映射到容器的 8000 埠
    ports:
      - "8000:8000"
    # volumes 用於將主機的目錄掛載到容器內
    # 1. 掛載程式碼目錄：讓您在主機上修改程式碼時，容器內會同步更新, 不需要一直 COPY
    volumes:
      - .:/app
    # 覆寫 Dockerfile 的 CMD，加上 --reload 參數以啟用熱重載
    command: uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```