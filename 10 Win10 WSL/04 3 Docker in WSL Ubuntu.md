https://lippertmarkus.com/2021/09/04/containers-without-docker-desktop/

https://github.com/twtrubiks/docker-tutorial?tab=readme-ov-file

==參考上面這個連結==
# ==Ubuntu 設定簡單，由WSL使用==


這個 從

==可行 且快速==
但是就等於 又多包一層，docker 指令 可在 WSL ubuntu 裏面下， 
也可從 Windows PowerShell 下。

 最後還是，
 ==不要執着== 直接用desktop  
 或許==轉到 Mac OS 開發== 
 畢竟==主要是開發的結果 而不是平台==
 ## 1 安裝 
```
apt install docker
```

## 2 設 docker.service 重啓
```
sudo cp /lib/systemd/system/docker.service /etc/systemd/system/
sudo sed -i 's/\ -H\ fd:\/\//\ -H\ fd:\/\/\ -H\ tcp:\/\/127.0.0.1:2375/g' /etc/systemd/system/docker.service
sudo systemctl daemon-reload
sudo systemctl restart docker.service

# Automatically start on startup 好像不用這個
sudo systemctl enable docker.service
```
## 3 如果要 Proxy 的話，[Service] 下加兩行
```
vi /etc/systemd/system/docker.service
[Service]
export http_proxy="http://10.1.220.44:8080"
export https_proxy="http://10.1.220.44:8080"
```
測試 docker search ubuntu

## 4 如果要讓外部 (PS1) 下指令 docker 的話, 改這樣，重啓 docker.service
```
sudo sed -i 's/\ -H\ fd:\/\//\ -H\ fd:\/\/\ -H\ tcp:\/\/127.0.0.1:2375/g' /etc/systemd/system/docker.service
# 改成這樣：ExecStart=/usr/bin/dockerd -H fd:// -H tcp://127.0.0.1:2375 --containerd=/run/containerd/containerd.sock
```
## 5. 外部 PS1上設Context 
==context create use==
```
PS> docker context create lin --docker host=tcp://127.0.0.1:2375
PS> docker -c lin ps
PS> docker -c lin image ls
PS> docker dontext use lin
PS> docker ps 
```
` docker context ls` 列出可用的 context


### 啓動 Container
```
docker run -it -d \
-h dean03 \
-v /mnt/c:/mnt/c \
-p 8000:8000 \
--name dean03 \
--network host \
dean03 /bin/bash 
```

### 進入 Container
```
docker exec -it dean03 /bin/bash 
```
