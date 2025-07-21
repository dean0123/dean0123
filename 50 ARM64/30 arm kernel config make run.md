# ARM Kernel 
### 0.  get Kernel (wget)
### 1.  config Kernel (vexpress_defconfig ) 
### 2.  make Kernel (make CROSS_COMPILE)
### 3.  run Kernel (qemu-system-arm -M)


# 0. Get kernel

取得 Linux Kernel
```bash
# cd /usr/src
# wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.15.178.tar.xz
```
Run as **USER account** 用一般User在arm下建立 linux 目錄
```bash
$ cd ~
$ cd virtualarm/kernel
$ tar xvf /usr/src/linux-5.15.178.tar.xz
$ cd linux-5.15.178
```


# 1. Config kernel (user) 
```bash
$ cd ~/virtualarm/kernel/linux-5.15.178
$ alias make_arm='make -j4 ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-'
$ make_arm vexpress_defconfig
$ make_arm menuconfig
# --> System Type --> [] Enable L2x0 outer cache controller 不要
# --> Save/exit 產生 .config 再用 menuconfig 手動改

```

# 2. Build kernel


```bash
$ alias make_arm='make -j4 ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf-'

$ time make_arm uImage LOADADDR=0x60000000 
$ make_arm dtbs
$ make_arm modules
# make_arm modules_install    (用 root 執行，會產生 /lib/modules/5.15.178/modules....
```
**modules_install** (可能要su  root後執行，之後檢查 直接build 到/lib/modules 目錄 v.rr.sss )

或

$ time make_arm  INSTALL_MOD_PATH=…/modules/ modules_install  (可能su  root後執行，之後到  ../modules 目錄，tar cvf  ../modules-v.rr.sss.tar.

xz lib/ 再cp 到  /lib)

# 3. Run Kernel test
```bash
$ cd arch/arm/boot
$ qemu-system-arm -M vexpress-a9 \
-m 256 -nographic \
-kernel zImage  
# -----> 然後當機 。。。。 
```