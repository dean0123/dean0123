
curl http://google.com 不行
curl http://google.com --proxy 10.1.220.44:8080 可以

再 Powershell 中設

```
$env:HTTP_PROXY = "http://10.1.220.44:8080"
$env:HTTPS_PROXY = "http://10.1.220.44:8080"
$env:NO_PROXY = "localhost,127.0.0.1" # Optional: Exclude certain hosts
```

```
