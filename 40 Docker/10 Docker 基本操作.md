
```
# 0 檢查 image 與 Container / 狀態
docker image ls
docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Status}}" -a
# PS1 裡面用 function xxx {} 做 alias
# function dockerps {docker ps  --format "table {{.Names}}\t{{.Image}}\t{{.Status}}\t{{.Ports}}" $args}


# 1 拉 Image
docker pull ubuntu (拉Image或 ubuntu:20.04) 

# 2 用 Image Create & Run new Container + Name(dean01)
docker run -it -d --name dean01 ubuntu /bin/bash 
# 把 Docker 的 5000 mapping 到 host 的 80
docker run -it -d -p 5000:80 --name dean02 ubuntu /bin/bash  
# 全部Port 與 Host 相同
docker run -it -d --network host --name dean03 ubuntu /bin/bash  

 

# 3 執行 /bin/bash 進入容器 dean01
docker exec -it dean01 /bin/bash

# 4 啟動/停止/刪除 容器dean01
docker start/stop/rm dean01 
```

##  換 Port
```
docker stop dean01
docker commit dean01 dean02 (用現在container dean01  建立一個新的 image(不是container) dean02)
docker run -it -d -p 5000:80 --name dean02 dean02 /bin/bash
```


## 尋找  docker search 

## compose
如果要用 Compose 就建立一個目錄，進入，取得 compose.yaml 然後
### 1. 建 Container 同時 也啟動 
 `docker compose up`
 
### 2 停止Container 
 `docker compose stop`
 或 `docker-compose stop`
重啟用， `restart` 

### 3. 下 container   
`docker compose down`
 或 `docker-compose down`
 改完 env 或 docker-compose.yaml 可能需要重 down up