https://kheresy.wordpress.com/2021/10/15/run-windows-container-without-docker-desktop/


WSL2 好像不需要 Nyper-V

可能要的 
```
#Optionally enable required Windows features if needed
PS> Enable-WindowsOptionalFeature -Online -FeatureName containers –All
PS> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V –All
```
