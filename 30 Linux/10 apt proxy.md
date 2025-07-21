/etc/apt/apr.conf
```
Acquire::http::Proxy "http://10.1.220.44:8080";
Acquire::https::Proxy "http://10.1.220.44:8080";

```



環境變數 (git docker pip )
```
export http_proxy="http://10.1.220.44:8080/"
export https_proxy="http://10.1.220.44:8080/"
no_proxy="localhost,127.0.0.1"
```