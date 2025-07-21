

## Windows Server 2019 只能裝 WSL1.  (2022 才能裝 WSL2)
太麻煩了， 不要用
 

https://learn.microsoft.com/en-us/windows/wsl/install-on-server


沒 winget
沒 docker desktop
沒 wsl2 只有 wsl1
太麻煩了， 至少要2022 不建議使用， 
改用 win10 wsl2 就好
或是直接 用 VMWare
Proxmax, MacOS



WSL 2 僅適用於 Windows 11 或 Windows 10 版本 1903、組建 18362 或更新版本。 要確認您的 Windows 版本，輸入 **winver** 檢查
x64 系統：**版本 1903**  或更新版本，**組建 18362.1049**  或更新版本。
Windows Server 2019 只能用WSL1 ， 






==很麻煩 不要了， 用 Docker 比較方便 又快速==
## 1: 開啟 feature
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux, VirtualMachinePlatform
```
## 2: 更新 WSL Kernel Update 以便執行 WSL2 的 image
```
Invoke-WebRequest -Uri "https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi" -OutFile ".\wsl_update_x64.msi"
Start-Process "msiexec.exe" -ArgumentList "/i .\wsl_update_x64.msi /quiet" -NoNewWindow -Wait
```

## 3: 手動 下載 安裝 啟動 WSL2 的image  ubuntu-2004.appx
https://learn.microsoft.com/en-us/windows/wsl/install-manual#downloading-distributions
```
curl.exe -L -o ubuntu-2004.appx https://aka.ms/wslubuntu2004
Add-AppxPackage .\ubuntu-2004.appx
```


