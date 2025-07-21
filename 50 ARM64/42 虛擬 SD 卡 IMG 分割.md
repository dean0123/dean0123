# 虛擬  SDCard Img分割
>1. 建立 虛擬 SD Card 檔案 **dd**  image file
>3. 分割 fdisk Image 檔案
>4. 模擬 loop Device **losetup**
>5. 格式化 mkfs Device
>6. 掛載 mount Device

```
# cd ~/virtualarm
# dd if=/dev/zero of=sdcard.img bs=1G count=1 
# fdisk -lu sdcard
# fdisk     sdcard 
# fdisk -lu sdcard 

```
可用 file 或 hexdump 看這個檔案形態及內容
此時無法 mkdosfs 也不行 mkfs，要連結為一個假的 Device
losetup  設定 Loop device 設定 file 檔案模擬成為 Block Device 可以Mount 跟 Format

```
# losetup -a
# losetup /dev/loop0 sdcard.img
# losetup -a
# losetup -o `expr 2048   \* 512` /dev/loop1 /dev/loop0
# losetup -o `expr 165888 \* 512` /dev/loop2 /dev/loop0
# losetup -a
# blkid /dev/loop1 (檢查 都沒有) 
```



