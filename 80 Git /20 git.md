  
## 1. 初始化 工作 目錄 (init / branch / remote)

```sh
git init
git checkout -b main （或是 git branch -M main)
git remote add origin https://XXXXXXXXX@github.com/dean0123/YYYYYYYYYY.git
```

- 如果 Remote URL 已經存在，就不用 remote add 改用 set-url

```sh
git remote add origin https://XXXXXXXXX@github.com/dean0123/YYYYYYYYYY.git
```

## 2. 從 Remote Git Server 拉檔案 (reset / pull)

```sh
git pull origin main
```

- pull = fetch + merge
- 若要 放棄Local的修改， 全部重拉 Git 最新檔案一次

```sh
git reset --hard origin/main
git pull origin main
```


## 3. 放檔案回 Remote Git Server (add / commit / push)

```sh 
git add .
git commit -m "修改版本訊息"
git push -u origin main
```

> 用 `.gitignore` 檔案，避免 git 同步的檔案 或目錄，如設定檔， 備份暫存， package 等。 

# 檢查功能
1. 看 config `git config -l` (--list)
2. 看 remote URL `git remote -v`
2. 看 status HEAD `git status`
2. 看 commit history `git log` (--oneline)


# 檢查Branch 分支 功能

1. 看 Branch 所有分支與提交紀錄  
`git show-branch -a` 
   - 如果只看 local 分支用 `git show-branch` 
   - 如果只看 remote 分支用 `git show-branch -r` 

1. 看 Branch 所有分支  
`git branch -a`   (-vva)
   - 如果只看 local 分支用 `git branch` 
   - 如果只看 remote 分支用 `git branch -r` 

    

    






