
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

