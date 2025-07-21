# u-boot loader

看官網，用git 下載 u-boot source code (用 **github** 比 官網快) 
https://docs.u-boot.org/en/latest/build/source.html


```bash
$ cd ~/virtualarm/bootloader
$ git config --global https.proxy http://10.1.229.229:15629
$ git config --global http.proxy http://10.1.229.229:15629
$ git config --global http.sslVerify false
$ git clone https://source.denx.de/u-boot/u-boot.git v2016.09
$ cd u-boot (or v2016.09) 
$ ls configs
$ alias make_arm='make -j4 ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-'
$ make_arm vexpress_ca9x4_defconfig
$ make_arm menuconfig
# apt-get install libgnutls28-dev
$ make_arm -j4
$ qemu-system-arm -machine vexpress-a9 -m 256 -nographic -kernel u-boot
==> mmcinfo
==> bdinfo
==> mmc info
==> mmc list
==>
==> control-a x (跳出)
```


```bash
$ qemu-system-arm -machine vexpress-a9 -m 256 -nographic -kernel u-boot -drive file=../../sdcard.img,if=sd,format=raw,index=0
==> mmcinfo
==> bdinfo
==> mmc info
==> mmc list
==> mmc part
==> ls mmc 0:1
==> ls mmc 0:2
==> fatinfo mmc 0:1


```