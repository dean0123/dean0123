# PROXY

cat > /etc/apt/apt.conf
```
Acquire::http::Proxy "http://10.1.229.229:15629/";
```
or
```
Acquire::http::Proxy "http://10.1.220.44:8080";
Acquire::https::Proxy "http://10.1.220.44:8080";

```



環境變數 (wget git docker pip )
```
export http_proxy="http://10.1.220.44:8080/"
export https_proxy="http://10.1.220.44:8080/"
no_proxy="localhost,127.0.0.1"
```

# SSH
apt update
apt install ssh (openssh-server 一樣， 要選 5 Asia，72 Taipei 看是否可以自動 或固定)

service --status-all 
service ssh start 

hostname -I (看 IP Address)
useradd dean
passwd dean  (dean)
passwd root  (admin)
ssh dean@localhost  (or IP address)


# IP Address





