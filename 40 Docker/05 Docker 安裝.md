# 1. Windows



# 2. Mac



# 3. Linux Ubuntu (22.04.5) 

## 1. 安裝基本 `docker.io` (Ubuntu 22.04.5 LTS)
```
docker.                     #測試是否有安裝docker
sudo apt update
sudo api install docker.io  #安裝基本
sudo docker ps              #用root 測試docker
docker ps                   #一般user 測試docker,應該不行
```

## 2. 加入 User 使用
```

sudo usermod -aG docker $USER      #加入要用docker 的user 到docker 群組, user 重新登
sudo systemctl restart docker.service. #重啟 Docker Servife
docker ps                   #檢查是否可執行 
docker search hello-world.  #檢查是否Proxy可連 dockerhub 拉image

```

## 3. 安裝 `docker-compose-v2`
```
docker compose              #檢查 docker compose 應該沒安裝
sudo apt install docker-compose-v2
docker compose              #檢查 docker compose 應該可以用了
```



## 4. Linux Docker + Porxy (公司內網) 
Docker Pull image是透過 docker deamon去啦資料, 單純由command line 設PROXY 是無法讓Daemon 使用, 必須在 deamon 啟動時參考設定檔才行
1. 設定 Docker Daemon 環境變數檔案, 通常位於 /etc/systemd/system/docker.service.d/ 目錄下, 沒有的話, 自己建立, 則systemctl 啟動時, 會參考這個位置
```
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo vi /etc/systemd/system/docker.service.d/http-proxy.conf
```
2. 加入以下Proxy 設定
```
[Service]
Environment="HTTP_PROXY=http://10.1.229.229:15629/"
Environment="HTTPS_PROXY=http://10.1.229.229:15629/"
```
3. 重新載入 systemd 設定, 重啟 docker service
```
sudo systemctl daemon-reload
sudo systemctl restart docker.service
docker search hello-world.  #測試dockerhub 連線
```