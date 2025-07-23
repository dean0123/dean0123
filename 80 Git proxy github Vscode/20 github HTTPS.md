ghp_tSJPd2CNZU26wQGux53g2amZiN80fakefake

(2025-7-23 產生新的) 也可用在OAuth或API/Basic Auth

ghp_tSJPd2CNZU26wQGux53g2amZiN80f3fakefake

1. 到 github 網站， 
2. 點右上頭像 -> Settings -> 
3. 左下方 Developer Settings -> Perdonal access Tokens -> Tokens (classec 就好)
4. Generate new token (classic) 
5. 選不過期，全部範圍 


# 用GitHub HTTPS : 不能再用 password 必須改用 Personnal Access Token(PAT)
不需要 Fine-grained Personal Access Token (FG PAT)


## HTTPS (這個 PS Ubuntu Docker Host 都可用)


## 1. 建立/進入/清除 工作目錄
```
mkdir test
cd test
rm -r .git/* (清除原有的 git 設定)

git status (看 現在Branch 分支 是啥，可能跟pull 的不同)
git branch -M main  (切換分支 到 Main 跟pull 的一樣， 用config 設定 default 較方便)

git init
git add .
```

## 2. 連線 Remote Origin (HTTPS)
```
# 1 用 HTTPS 的 URL 
git remote add origin https://github.com/dean0123/fastapi.git
git remote -v
```
> 2.1 git remote add origin https:// (加remote Origin 的URL)
>
> 2.2 git remote set-url https://    (改現有 remote Origin 的URL)
>
> 2.3 git remote remove origin       (移除 舊的 remote origin)


## 3. 拉檔案 -> 編輯檔案
```
git pull origin main  (或 master)
dir  
# pull 會有  rebase false|true，ff， merge衝突解決方式
# 或是用 clone 複製整個 repo, 並建立一個 repo 目錄
# git clone https://github.com/dean0123/fastapi.git
```


## 4. Commit Push 回 Remote Origin

### Windows 有 credential-manager 比較簡單
```
git add .
git commit -m '1'
git push -u origin main 
```

### Docker Linux 要輸入 token 比較麻煩。可將 token 加入 URL 中，就不必打 token了
```
git remote set-url origin https://<ghp_xxooToken>@github.com/dean0123/fastapi.git
```

## 5. git log 看 commit history




如果要移除舊的 Remote Origin
```
git remote remove origin
git remote add origin https://github.com/dean0123/fastapi.git
```
