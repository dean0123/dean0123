
安裝Desktop後 做以下個設定
1. `Settings -> General -> use WSL2 based engin `
2. `Settings -> WSL integration -> Debian, Ubuntu ..... ` 
3. WSL Linux 內部裝  `apt-get  install docker.io`


## 1. Docker Desktop 打開==WSL 支援==
-  去 Docker Desktop 設定 
`Settings -> General ->use WSL2  based engin`
-  內外應該都==不用==再設定Proxy
`Settings -> Resources  -> Proxy `
也不用在 Ubuntu 裡面設定 
`$ export HTTP_PROXY=......`

## 2. ==每一個==新安裝的 WSL Ubuntu Debian 都要==開啟整合==

- 去 Docker Desktop 
`Settings -> Resources ->  WSL Integration ->`
==`開啟 Distros Debian, Ubuntu ..... `==

## 3. Linux 要裝 `docker.io`
- WSL Linux 要 apt-get install `docker.io`

