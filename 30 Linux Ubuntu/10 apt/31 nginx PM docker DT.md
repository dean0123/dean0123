
https://nginxproxymanager.com/guide/

## 1. compose安裝NPM
1. 建立進入工作目錄 例如 npm (或 nginx-proxy-mgmt) 
2. 開檔案 docker-conpose.yml
```
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

3. 安裝及開啟
```
# docker-compose up -d 
或
# docker compose up -d 
```
停止用 docker-compose stop 
移除用 docker-compose rm 

4: 登入web adm
測試 `http://localhost` `http://127.0.0.1` `http://10.18.61.166` 都ok

登入 `http://127.0.0.1:81`
`帳號：admin@example.com` 
`密碼：changeme`
再改 email pass

- 檢查 Container 的 `Logs， Exec， files` 
 - Config 在 Container 裡的 `/etc/nginx` `/data/nginx/proxy_host` 
  - Log 在 Container 裡的 `/data/logs`

## 2. OpenSSL 產生 Key/Crt (localhost)
登入 Docker Exec 指令列， 用 OpenSSL 產生 self-signed Key/crt
 
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /data/custom_ssl/docker.key -out /data/custom_ssl/docker.crt
openssl 
openssl verify -- /data/custom_ssl/docker.crt 
```

-   `-x509`：建立自行簽署的憑證。
-   `-nodes`：不要使用密碼保護，因為這個憑證是 NGINX 伺服器要使用的，如果設定密碼的話，會讓伺服器每次在啟動時書需要輸入密碼。
-   `-newkey rsa:2048`：同時產生新的 RSA 2048 位元的金鑰。

==可以用IP Address 10.18.61.116做CommonName==
也可以用localhost 做CommonName


## 3: 加 SSL 到 config file 
==以下部分，還有待確認，因為安裝太多不同版本，有溷肴到Config，應該Docker 的設定就都在/data 裡面， 怎麼會跟 系統的 /etc 混在一起。  如果是/etc 也應該是 container (debian) 裡面的/etc/nginx/conf.d/... 而不是 WSL ubuntu 裡面的 /etc/nginx/sites-enables/... ==
`/etc/nginx/conf.d/default.conf`

在Docker 內，選File `/etc/nginx/conf.d/default.conf`  -> edit  ==加4行， 不改 Server Name==

```
server {

# ------ 加以下四行，加SSL ------    
    listen 443 ssl ;
    listen [::]:443 ssl;
    ssl_certificate /data/custom_ssl/docker.crt;
    ssl_certificate_key /data/custom_ssl/docker.key;
# -----------------------------    
# ---------- 後面不變 ----------
# -----------------------------    
# 到此 https://127.*，10.*可用，
# 但是 https://localhost 不能用 只能這樣了, 
# ------ 就算 加localhost 也不行 -----
#	server_name localhost-nginx-proxy-manager localhost; (這localhost 還是不能用)    
#或	server_name _ localhost; (這localhost 還是不能用)    
#或	server_name 127.0.0.1 10.18.61.116 localhost ; (這樣更慘) 



}




```
重啟 Docker nginx container
`https://127.0.0.1` `https://10.18.61.116`
都 OK，  (不用設WSL interface proxy) 
但是測試 `https://localhost`  不能用，沒關係，一般也不會這樣用。 

==奇怪，為何NPM@docker可以用IP 連，不需要設WSL proxy，但 nginx@ubuntu@WSL就要無法用IP 連，要設WSL proxy 才行==  

==因為：一個是 Docker， 一個是WSL== 

## 4. 加 Reverse Proxy
登入 NPM:81 加 Source: `localhost` `127.0.0.1` `10.18.61.116` 到 Destination:  `http://10.18.61.116:3001`
(不用再加SSL了)
測試 `https://10.18.61.116` 會轉到 3001

還要加 SSL key 到主頁面， 再加到 proxy 裡面

設定檔案在
`/data/nginx/proxy_host/1.conf `

## Path
1 /data/nginx
2 /app  (AP程式)
3 /etc/nginx/conf.d:
