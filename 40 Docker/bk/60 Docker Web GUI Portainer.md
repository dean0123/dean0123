



# 簡易WEB UI docker portainer
- https://kawsing.gitbook.io/opensystem/docker-cong-an-zhuang-dao-ying-yong-ru-men-pian/webui-portainer#jian-yi-web-ui-docker-portainer


```
docker run -d --privileged --name portainer -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock --restart=always -v /docker/portainer/data:/data portainer/portainer
```
**--privileged**

**當操作者執行docker run --privileged時，Docker將擁有訪問主機所有設備的權限，同時Docker也會在apparmor或者selinux做一些設置，使容器可以容易的訪問那些運行在容器外部的設備**

### 

**-p 9000:9000**

**容器中可以執行一些網路應用，要讓外部也可以存取這些應用，可以通過 -P 或 -p 參數來指定連接埠映射**

**使用 -P 參數時，Docker 會隨機映射一個 49000~49900 的連接埠到內部容器開放的網路連接埠**

**-p（小寫的）則可以指定要映射的連接埠。支援的格式有 ip:hostPort:containerPort | ip::containerPort | hostPort:containerPort**

### 

**-v /portainer/data:/data**

**掛載一個HOST主機目錄作為資料卷 使用 -v 可以指定掛載一個HOST主機的目錄到容器中去**
window docker desktop 是在WSL 的desktop WSL 裡面的路徑 `/mnt//docker/volume/` 裡面， 也可以用 `docker volume create --name portainer` 自定 volume

**這個參數的目的很==重要==，那就是將portainer第一次啟動，初始話的過程設定紀錄到嚮應的HOST的目錄中，保存HOST機的設定，==container 被刪掉時那個資料夾資料仍被保留==
只要使用相同的指令，便能重新取回之前的==設定，管理者帳號的密碼==等**

**然後，由瀏覽器輸入 HOST 機的ip:9000（透過連接埠映射）**

**建立管理員密碼**