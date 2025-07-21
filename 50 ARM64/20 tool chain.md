

# 0. vi /etc/apt/apt.conf  加 
```
Acquire::http::Proxy "http://10.1.229.229:15629/";
或 
Acquire::http::Proxy "http://10.1.220.44:8080/";
```

# 1. Architecture Tool chain
##  1. ArmHF tool chain (Float Point)
 
```bash
apt-get install crossbuild-essential-armhf \
libc6-armhf-cross \
gcc-arm-linux-gnueabihf \
cpp-arm-linux-gnueabihf \
g++-arm-linux-gnueabihf

dpkg --add-architecture armhf
dpkg --print-foreign-architectures
```
## 2. ArmEL tool chain
```bash
apt-get install crossbuild-essential-armel \
libc6-armel-cross \
gcc-arm-linux-gnueabi \
cpp-arm-linux-gnueabi \
g++-arm-linux-gnueabi

dpkg --add-architecture armel
```
## 3. Arm64  tool chain (arm 64 bit)
```bash
apt-get install crossbuild-essential-arm64 \
libc6-arm64-cross \
gcc-aarch64-linux-gnu \
cpp-aarch64-linux-gnu \
g++-aarch64-linux-gnu 

dpkg --add-architecture arm64

```


# 2. Common Tool Chains


```bash
apt-get install fakeroot \
build-essential libncurses-dev \
xz-utils libssl-dev bc \
flex libelf-dev bison
# ncurses --> libncurses-dev  

apt-get install python3  dwarves \
u-boot-tools debootstrap

apt-get install qemu-system-arm \
qemu-user-static binfmt-support

apt-get install dosfstools file wget

# ---- for hexdump (mey not need) ----
apt-get install bsdextrautils

# ---- make u-boot this -----
apt-get install libgnutls28-dev

# --- rsync ----- 同步 root fs -----
apt-get install rsync
```

2: Cross build tool chain