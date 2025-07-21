# 實體 SDCard vhd分割
>1. 加入實體 SD Card dmesg Device
>2. 分割 fdisk Device
>3. 格式化 mkfs Device
>4. 掛載 mount Device
>5. 儲存 Device 成為 Image 檔案



## 磁碟機 或 CD Card 插入，檢查，分割
> - 插入 sdcard (然後用dmesg 查看 **/dev/sdb**) 
> - 用 VM (hyperv) 建立 VHD，加入 Linux VM，(可能需要重開機)
> - 使用工具如下 確認 **/dev/sdb**

    # dmesg   (| grep sd 插上隨身碟， 再dmesg檢查 /dev/sdb
    ，sdax，sdbx...)
    # lsblk   (列出 Block Device 及 分割Partitions)
    # /usr/sbin/blkid  (檢查 Block UUID 及Block Size Type)
    # /usr/sbin/fdisk  /dev/sdb  (確認新插入的 SD Card 是 sdbx 後，進行分割)  (後面版本 ext4 要用 fdisk.ext4 來分割)

分割sdcard
1. 分割一 vfat 100M (type b, W95 FAT32 vfat)    
```
# fdisk /dev/sdb
```

> - **n** ->  **p**  -> **1** -> **2048** -> **+100M** -> **p**
> 一個 HD 只能建4個 primary
> 0-2047 MBR (DOS) 保留給 partition table
> - **t** -> **1** -> **b** ->**p**： 改 Type 從 Linux 改為 FAT32
> - **w** 最後 Write 儲存 分割內容。 

3. 分割二 Linux 剩下全部 (type 83 Linux)
4. 格式化 mkfs format 檢查新Disk 的Partitions 並掛載
```
# mkdosfs   /dev/sdb1 (再用 #blkid 檢查 type變vfat)
# mkfs.ext4 /dev/sdb2 (再用 #blkid 檢查 type變ext4) 
```
```
# mount /dev/sdb1 /sdcard1
# mount /dev/sdb2 /sdcard2  (用 #du -h 或 #lsblk 看 mount point) 
```
4. 製作 image 檔案 (然後用 file, fdisk 看這個 sdb.img 檔案的 partition list) 

```
# dd if=/dev/sdb of=sdb.img
```
