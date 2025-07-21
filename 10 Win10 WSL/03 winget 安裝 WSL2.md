
- https://learn.microsoft.com/zh-tw/windows/wsl/install
- https://learn.microsoft.com/zh-tw/windows/wsl/install-manual
- 


或  WINGET
```
PS1> winget search --id wsl
PS1> winget install --id wsl
PS1> winget list --id wsl
PS1> winget uninstall --id wsl
```

開啓 WSL2

```
wsl --install
wsl --set-default-version 2
```

舊版 或 手動安裝 DISM
```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```




# 基本指令

```
wsl
wsl -l -o (列出 online 有的 image Distribution)
wsl -l -v (列出已經安裝的 image)
wsl --install Ubuntu-30.04 
wsl -d Ubuntu-20.04  (連到 開啓 Ubuntu Image)
wsl --shutdown Ubuntu
wsl --set-default Ubuntu (設為預設 image)
wsl --terminal Ubuntu (終止 移除 Image)
```


username: dean dean dean  (安裝ubundu 加user dean)

