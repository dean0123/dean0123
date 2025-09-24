## 1. 下載 mediaMTX
```

# 下載 CPU 的 Bin 執行檔案 ARM64 X86 arm7
$ curl -LO https://github.com/bluenviron/mediamtx/releases/download/v1.15.0/mediamtx_v1.15.0_linux_arm64.tar.gz 
$ gunzip xxx.gz
$ tar -xvf xxx.tar

$ vi mediamtx.yml  # 改設定檔 Stream 名稱 路徑
     paths:
        mystream:
           source: rpiCamera
$ ./mediamtx       # 啟動mediamtx 執行檔
```
