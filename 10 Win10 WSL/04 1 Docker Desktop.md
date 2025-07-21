

# ==Desktop 就比較多東西，有時候比較慢，但通通幫你弄好，是PS下 可切換 WIndows 容器 跟 Linux 容器==
## ==用WSL的話，會開一個 Docker Desktop==

Docker 會用 hyper-V 或 WSL2，如果有 WSL2 的話， 
Docker 安裝時 會建議用WSL2 效率比較好
所以 最好還是裝 WSL2 再裝 Docker

## 1 上篇安裝 WSL2
可能要的 
```
#Optionally enable required Windows features if needed
PS> Enable-WindowsOptionalFeature -Online -FeatureName containers –All
PS> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V –All
```

## 2 指令 winget 安裝 desktop
```
PS1> winget search --id wsl
PS1> ==winget search --id dockerdesktop==
```


## 設定 為 WSL2
安裝Docker Desktop後 做以下個設定
1. `Settings -> General -> use WSL2 based engin `
2. `Settings -> WSL integration -> Debian, Ubuntu ..... ` 
3. WSL Linux 內部裝  `apt-get  install docker.io`



這個不確定要不要，沒有也可以運行
`Settings -> General -> tcp://localhost:2375 without TLS`
`$ export DOCKER_HOST=tcp://127.0.0.1:2375`



https://learn.microsoft.com/zh-tw/windows/wsl/tutorials/wsl-containers

