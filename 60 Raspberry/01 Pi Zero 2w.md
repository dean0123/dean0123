
> lsusb
> dpkg --configure -a

raspi-config # 改啓動 CMD 或 GUI
sudo su -  #切換 root


> 
> rpicam-hello
> libcamera-hello


> rpicam-vid -t 0 -n --codec libav --libav-format mpegts -o - | cvlc stream:///dev/stdin --sout '#rtp{sdp=rtsp://:8554/stream1}'





## -- Service --
add /etc/systemd/system/rtsp.service
```
[Unit]
Desc 
After=multi-user.target
Requires=network.target


[Service]
Environment=DISPLAY=:0
Type=simple
ExecStart=/home/pi/rtsp
Restart=on-failure
User=pi
Grouop=pi



[Install]
WantedBy=multi-user.target
```


systemctl enable rtsp.service
service rtsp status
service rtsp start



# 藍牙


# 登入


# ssh rtsp bluetooth wifi

