

## 1 image -> save tar 
## 2 load tar -> image
```
docker save dean04 > dean04_save.tar
docker rmi dean04 
docker load < dean04_save.tar
docker history dean04
```

## 3 container -> export tar
```
docker export dean04 > dean04_export.tar
docker stop dean04
docker rm dean04
# 將 tar import 為 image
docker import dean04_export.tar dean04  
```
## 4 import tar -> ==image==