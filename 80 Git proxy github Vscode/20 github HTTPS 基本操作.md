
## TOKEN 不能寫在 開放的檔案，這樣大家都拿得到。 
要寫在私人檔案內




# 用GitHub HTTPS : 指令列 不能再用 password 必須改用 Personnal Access Token(PAT)
- 不需要 Fine-grained Personal Access Token (FG PAT)
- HTTPS (這個 PS Ubuntu Docker Host 都可用)


## 1. 工作目錄 workdir/repo (建立/進入/清除)
```
--> 1. 用 CLONE 建立 repo 
$ mkdir workdir (工作目錄)
$ cd workdir
$ git clone https://github.com/dean0123/fastapi.git (會建立 fastapi repo 目錄) (PAT TOKEN 可以在這裡加 也可之後要 PUSH 再改)
$ cd fastapi （repo 目錄，git remote 連線自動設好）

--> 2. 用 PULL 拉檔案 (自己建立 工作目錄 跟 Repo 目錄)
$ mkdir -p workdir/fastapi01  （可以建與原來 repo 名稱不同的目錄）
$ cd workdir/fastapi01
$ git init (初始化 repo 目錄, 建立 .git/*)
$ git pull https://github.com/dean0123/fastapi.git (不會建立repo目錄，直接放在目前 pwd 下，也不會設好 git remote )
 
--> 3. 清除 git 設定 或 git repo 目錄
rm -rf .git/* (只清除原有的 git 設定)
rm -rf repo (清除全服 repo 目錄，重拉一遍)

```

## 2. 遠端連線 Remote Origin (HTTPS+PAT)
```
--> 1 建立 連線  
$ git remote add     origin https://<ghp_xxooTOKEN>@github.com/dean0123/fastapi.git
--> 2 改 連線 （或加/改 PAT TOKEN）
$ git remote set-url origin https://<ghp_xxooTOKEN>@github.com/dean0123/fastapi.git
--> 3 看 連線
$ git remote -v
--> 4 移除 連線
$ git remote remove origin
```


## 3 基本檢查
```
$ git remote -v  （看remote 連結 Token 等）
$ git status     （看 那一個 branch 是 main master 或其他）
$ git config -l   (看config)
$ git log         (看 commit 等 歷史紀錄)

$ git branch -M main  (切換分支 到 Main 跟pull 的一樣， 用config 設定 default 較方便)
```

## 4. 寫回GIT ADD COMMIT PUSH 
```
git add .
git commit -m '1'
git push -u origin main （或master 其他branch）
```

# ===== 基本操作 結束 =====

