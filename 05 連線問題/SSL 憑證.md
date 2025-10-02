## 1. 安裝 ca-certificates
```sh
apt install ca-certificates
ls -l /etc/ssl/certs/ca-cert*
```
會包含大部分的CA 並產生一個 ca-sertificates.crt 
也 可以用 `update-ca-certificates` 重新建出來一樣的

## 2. 匯入 購買的 CA 憑證, 放到 CA 根目錄
``` 
    # 通常是 /usr/local/share/ca-certificates/
$ cp my.crt /usr/local/share/ca-certificates/
$ update-ca-certificates  # 把 my.crt 加入 CA-Certificates.crt 
$ ls /etc/ssl/certs/my*   # 會 產生一個 my.pem 連結 
$ ls /etc/ssl/certs/ca-*  # 會變大, 因為加入新的 my.crt
```
## 3. 驗證 my.crt
```
$ openssl verify /usr/local/share/ca-certificates/my.crt
傳回----> /etc/ssl/certs/ca-certificates.crt: OK
```

## 4. 產生 自簽 憑證 openssl
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout my.key -out my.crt
```


