
- https://lippertmarkus.com/2021/09/04/containers-without-docker-desktop/
- https://kheresy.wordpress.com/2021/10/15/run-windows-container-without-docker-desktop/


# ==這個只有 Window的容器，只能執行windows app， 不能跑Linux ubuntu 等==

## ==這個 沒什麼用 ,  但是可以用指令 docker context 看 WSL 的 Dockerd==




也是要enable  VM 跟 WSL2 比較好

##  1 下載 執行檔，再設路徑PATH
https://download.docker.com/win/static/stable/x86_64/
就兩個檔案而已 
或用




## 2 用 Winget 安裝 CLI，自動設PATH

`inget install --id Docker.DockerCLI`

```
> winget search --id docker 
> winget install --id Docker.DockerCLI -e (會自動加PATH 到執行檔 docker 跟 dockerd) 
   Path environment variable modified; restart your shell to use the new value.
   Command line alias added: "docker"
   Command line alias added: "dockerd"

> winget list docker
Name       Id               Version Source
-------------------------------------------
Docker CLI Docker.DockerCLI 28.2.2  winget
> docker -v
Docker version 28.2.2, build e6534b4
```


##  3: 另外可 用 WINGET 下載 
```
>winget download --id Docker.DockerCLI 
```


##  執行 啓動 dockerd (設Proxy)
```
$env:HTTP_PROXY = "http://10.1.229.229:15629"
$env:HTTP_PROXY = "http://10.1.229.229:15629"
dockerd
```

## Pull Image (linux vs windows)
```
## docker login -u deanliu1 -p ?1 (可不用登入)
docker search ubuntu
```

== 沒辦法  最後 還是 失敗， Window Docker CLI 只能起 Windows 的Container， 無法執行 linux 的 image  也不知道如何 改為 Linux 的Engine 還是要 Docker Desktop CLI 才性 ， 所以 下載 改 WSL 裏面的 Ubuntu  裝 Docker ==