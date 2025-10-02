## 1. 下載 mediaMTX
```sh

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

## 2. 設定 轉90度
在 mediamtx.yml 下面,找到 paths 加入下面幾行
```yml
paths:
  rotate:                       # 這個是 stream 的路徑一
  mystream:                     # 這個是 stream 的路徑二, 可繼續增加
    source: rpiCamera           # 來源是 rpi 鏡頭
    runOnReady: >               # 這裡做轉換90 度, 如果不用轉換, 整段可不用. 
      ffmpeg -i rtsp://localhost:8554/mystream
        -vf "transpose=2"
        -pix_fmt yuv420p -c:v libx264 -preset ultrafast -b:v 600k
        -max_muxing_queue_size 1024 -f rtsp rtsp://localhost:8554/rotate
    runOnReadyRestart: yes


```
## 3. 設定Service
vi /etc/systemd/system/mediamtx.service
```sh
[Unit]
Description=MediaMTX Server
After=multi-user.target
Requires=network.target


[Service]
EnvironmentFile=-/home/pi/mtx_arm64
ExecStart=/home/pi/mtx_arm64/mediamtx /home/pi/mtx_arm64/mediamtx.yml
Environment=DISPLAY=:0
Type=simple
Restart=on-failure
StandardOutput=file:/home/pi/mtx_arm64/mtx.log
StandardError=inherit
User=pi
Group=pi

[Install]
WantedBy=multi-user.target
```

```
systemctl daemon-reload
systemctl enable mediamtx
systemctl start  mediamtx
```

WebRTC Chrome 開啟 WebRTC 8889
- http://10.18.61.229:8889/mystream
- http://10.18.61.229:8889/rotate

HLS Chrome & Safari HLS 8888
- http://10.18.61.229:8888/mystream
- http://10.18.61.229:8889/rotate


RTSP: 用 CCTV/VLC 開啟 RTSP 8554
- rtsp://10.18.61.229:8554/mystream
- rtsp://10.18.61.229:8554/rotate
