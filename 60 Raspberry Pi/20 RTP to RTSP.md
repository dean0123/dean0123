## 1. 做一個 rtsp 執行檔案

```
#!/bin/bash
rpicam-vid -t 0 --codec libav --libav-format mpegts -o -| cvlc stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/stream2}'
```


## 2. 設定 Servive
```
pi@raspberrypi-10.18.61.229:~ $ cat > /etc/systemd/system/rtsp.service
[Unit]
Description=RTSP Server
After=multi-user.target
Requires=network.target


[Service]
ExecStart=/home/pi/rtsp
Environment=DISPLAY=:0
Type=simple
Restart=on-failure
StandardOutput=file:/home/pi/rtsp.log
StandardError=inherit
User=pi
Group=pi


[Install]
WantedBy=multi-user.target
```

```
systemctl daemon-reload
systemctl enable rtsp.servie
systemctl start rtsp.service
```

vlc 開啟 http://10.18.61.229:8554/stream2