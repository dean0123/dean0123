# Dean 的工作日記 4
## 主要分內容為
1. Win10 WSL
2. Mac 
3. Linux
4. Docker
5. ARM64
6. Raspberry 
7. Python
8. git  


Markdown

ubuntu:jammy
debian:bookworm-slim


Home work python:3.10-slim-bookworm 
1. Install Docker Desktop and Run hello-world
   去 hub.docker.com 看要的 official images ex:python (找要的版本 tag)
2. 下載 Iamge vs 建立 Container (容器) 
```
----- 可去 hub.docker.com 找要用的 image ----
----- 也可指令尋找 image                 ----
   > docker search python    
   > docker pull python:3.10-slim-bookworm  # 下載 image
   > docker images -a ; docker ps -a        # 檢查image 與 容器
----- 用 image 執行 建立 容器 web_cntr -----
----- 並 執行 容器 命令 (/bin/bash)    -----
   > docker run -it --name web_ctnr python:3.10-slim-bookworm /bin/bash  
   # python --version   # 已經進入 web_ctnr 容器,檢查一下
   # cat /etc/os*a      # 查看 ctnr 的 OS 版本
   # curl               # 測試指令 curl 不能用
   # exit               # 跳出 ctnr shell 
   > docker images -a ; docker ps -a
----- 啟動 並 執行 容器 指令 -----
   > docker start web_ctnr 
   > docker images -a ; docker ps -a
   > docker exec -it web_ctnr /bin/bash
   # python --version   # 測試容器指令
   # exit               # 跳出 ctnr shell 
   > docker images -a ; docker ps -a
   > docker stop  web_cntr   # 停止容器 web_cntr
   > docker rm    web_cntr   # 刪除容器
   > docker rmi   python:3.10-slim-bookworm  #刪除 iamge
-----> 然後從頭再做一次

   ``` 

3. 進入 容器 web_cntr 開始 limux 測試
3. 進入 容器 web_cntr 開始 python 測試

