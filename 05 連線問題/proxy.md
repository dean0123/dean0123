## 1. Linux export 

```
export HTTP_PROXY="http://10.1.229.229:15629";export HTTPS_PROXY=$HTTP_PROXY
```

PC use OS setup
MAC use OS setup

取消用
unset HTTP_PROXY
unset HTTPS_PROXY
unset ALL_PROXY


## 2. apt apt-get (proxy)

```
cat > /etc/apt/apt.conf
Acquire::http::Proxy "http://10.1.229.229:15629/";
```

## 3 curl (用這個比 wget 好一些)
>>> [!CAUTION] curl: (60) SSL certificate problem: self-signed certificate in certificate chain
More details here: https://curl.se/docs/sslcerts.html
---> 安裝 openssl 等試試看


curl -O https://git/.../master.zip  (下載檔案)

## 4 wget
>>>[!CAUTION] wget unable to establish ssl connection.
---> 安裝 openssl 等試試看


## 5 git (Proxy) 
>>> [!CAUTION] git clone https:// gnutls_handshake() failed: The TLS connection was non-properly terminated.
---> 安裝 openssl 等試試看


git config --global http.proxy http://10.1.229.229:15629
git config --global https.proxy http://10.1.229.229:15629
git config --global http.sslVerify false

git config -l

刪除
git config --global --unset http.proxy
git config --global --unset https.proxy
git config --global --unset http.sslVerify


## 6. docker Linux (Porxy 公司內網) 
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



