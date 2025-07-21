
## 更新路徑： 跳過 企業WSUS 直接去 Internet 更新
Proxy 10.1.229.229：15629 可以
```
# 1:regedit 改Registry 或下指令
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" -Name "UseWUServer" -Value 0  
# 2:重新啟動 Update Service
Restart-Service -name wuauserv   
```

## 安裝：放大鏡找 feature > 選用功能 > +新增 > 尋找 openssl > 安裝，或用指令 
```
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```


## 連線 用 AD 帳號 或 Local 帳號
```
ssh domain\username@servername
```