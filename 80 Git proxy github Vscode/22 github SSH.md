- https://docs.github.com/en/authentication/connecting-to-github-with-ssh
- https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux



# 基本與 HTTPS 一樣， 但是要改爲 SSH URL, 並先產生 一對 SSH Key 


# 1. 產生 25519 Key  (Windows Linux 同)
```
ssh-keygen -t ed25519 -C "your_email@example.com" 
```
或 `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"` 

`> ls ~/.ssh` 看產出的 id key 檔案


# 2. 啓動 ssh-agent
## 2.1 Windows 啓動 ssg-agent
```
> Get-Service -Name ssh-agent
> Set-Service -Name ssh-agent -StartupType Manual
> Start-Service ssh-agent
> ssh-add c:/Users/deanliu/.ssh/id_ed25519
> ssd-add -l (查看是否加入 Pub key)
```

## 2.2 Linux 啓動 ssh-agent
```
$ eval "$(ssh-agent -s)" (用這個指令啓動，會看到PID)
$ ssh-add ~/.ssh/id_ed25519 
$ ssh-add -l  (查看是否加入 Pub Key)
```


## 3. 加 公鑰 id_ed25519.pub 到 github 中
github 右上頭像-> settings -> 左邊 ssh -> add ....
測試 
```
git -T git@github.com  (如果出現 key yes/no 就對了)
```
## 但是如果 有 Proxy 就麻煩了，用手機熱點ok。 不然要安裝 corkscrew , netcat, nmap 等工具，然後設定 ~/.ssh/config 做SSH Proxy 
* linux ncat 試過 不行  <<<失敗>>> 過不了proxy
* linux corkscrew 試過也不行 <<<失敗>>> 過不了 proxy
 
## 4 git remote 
 ```
 git remote set-url origin git@github.com:dean0123/fastapi.git
 git pull/clone/add/commit/push Window Linux 都可以用 很快 手機wifi熱點 試的。
```







