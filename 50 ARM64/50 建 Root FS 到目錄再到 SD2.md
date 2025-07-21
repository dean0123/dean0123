

# 50 Root File System 到目錄 --> 再到 SD2卡

## 1. 建立 Root FS  (debootstrap 1, 2) 
```bash
# cd ~/virtualarm
# debootstrap \
--arch=armhf \
--keyring=/usr/share/keyrings/debian-archive-keyring.gpg \
--verbose \
--foreign buster ./rootfs

# cp /usr/bin/qemu-arm-static /mnt/sdcard2/usr/bin

# chroot ./rootfs /bin/bash 

time /debootstrap/debootstrap --second-stage
```
最後出現 I: Base system installed successfully.




## 2. 改造 Root FS  (rootfs)

帳號密碼 Hostname
```bash
echo root:admin |chpasswd
useradd dean
echo dean:dean | chpasswd
echo arm_dean > /etc/hostname
```



加網路卡 dhcp 或固定
vi /etc/network/interfaces
```bash
# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
allow-hotplug enp2s0
iface enp2s0 inet dhcp
```

安裝 Apache
```bash
apt-get install apache2
systemctl isenabled apache2
systemctl is-enabled apache2
```

清除
```bash
apt-get clean
rm -rf /usr/share/doc/*
rm -rf /usr/share/locale/*
rm -rf /usr/share/man/*
rm -rf /var/log/*
```



## 3 最後同步到 Sd-Card2 (rsync)

```bash
/virtualarm# rsync -av ./rootfs/ /mnt/sdcard2
```
檢查 /etc/hostname   /etc/network/interfaces 設定