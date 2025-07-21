https://learn.microsoft.com/zh-tw/troubleshoot/developer/webapps/aspnetcore/practice-troubleshoot-linux/2-2-install-nginx-configure-it-reverse-proxy

https://hackmd.io/@warrenpig/create-self-signed-https-nginx-app


## 1. apt install nginx 

1. 我是在 Ubuntu @ WSL2 上安裝nginx
2. 也可以在VM hyper-v 的Ubuntu/Debian上安裝 nginx
3. 也可以直接在 Docker 上安裝nginx。 
4. 也可以在Docker 上裝 nginx-proxy-mangemer

測試 check `curl http://localhost`  

## 2. 加OpenSSL Key/Crt


apt install openssl

mkdir /etc/nginx/ssl (放憑證的地方)
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/local.key -out /etc/nginx/ssl/local.crt

openssl verify -- local.crt (測試) 
```
## 3. 加SSL 及 Reverse Proxy 到 config file 
- /etc/nginx/sites-enabled/default 

Port 3001 是 RocketChat@docker 測試Port
```
server {
# ------------- Basic Server Setup -----------------
  server_name _;
  # server_name 10.18.61.116 127.0.0.1 localhost;

  listen 80;
  listen [::]:80;

  listen 443 ssl;
  listen [::]:443 ssl;
  ssl_certificate /etc/nginx/ssl/local.crt;
  ssl_certificate_key /etc/nginx/ssl/local.key;

  access_log /tmp/access.log;
  error_log  /tmp/error.log   warn;
#               index index.html;
#               root /var/www/html;

# ------------- Reverse Proxy Setup ----------------
    location / {
        proxy_pass         http://localhost:3001;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;

    }

}
```
測試 check `https://localhost`  


## 4. 連 Localhost 可以，IP不行 (@WSL)
測試 只通 `http://localhost` 跟 `http://127.0.0.1` 
但 `http://10.18.61.116` 不通，
到 ==WSL PS Admin==執行
```
PS> netsh interface portproxy add v4tov4 listenport=80 listenaddress=10.18.61.116 connectport=80 connectaddress=127.0.0.1
PS> netsh interface portproxy add v4tov4 listenport=443 listenaddress=10.18.61.116 connectport=443 connectaddress=127.0.0.1
PS> netsh interface portproxy show all

# PS> netsh interface portproxy add v4tov4 listenport=80 listenaddress=0.0.0.0 connectport=80 connectaddress=172.29.251.104
# PS> netsh interface portproxy delete v4tov4 listenport=443 listenaddress=10.18.61.116 

# 開啟外連內防火牆
PS> New-NetFirewallRule -DisplayName "WSL2 Port Bridge" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 80,443,8008

```
再測試IP  `http://10.18.61.116` 及 `httpx://10.18.61.116` 
OK

==奇怪，為何NPM@docker可以用IP 連，不需要設WSL proxy，但 nginx@ubuntu@WSL就要無法用IP 連，要設WSL proxy 才行==  

==因為：一個是Docker， 一個是WSL==


## 5 Log /var/log/nginx
