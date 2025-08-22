- GIT 基本 https://ithelp.ithome.com.tw/users/20139195/ironman/4770
- GIT 分支 使用指令 https://github.com/twtrubiks/Git-Tutorials


## 01 Git 基本設定 
```
git config --list
git config --list --show-origin
git config --global init.defaultbranch main
#   設定預設 branch 為 main 先定為一樣， 配合 github
#   因為 github 預設是main  
#   但是 git    預設是master
git config --global http.proxy "http://10.1.229.229:15629/"
git config --global user.name dean0123
git config --global user.email dean0000@gmail.com 

git config --edit (修改 刪除 config)
git config --global --edit 

```


## 02 基本操作如下，細節如個別檔案
1. git init 設定 工作目錄 
2. git remote add origin URL 設定連線remote origin
3. git pull origin main 從remote拉檔案分支。或clone
4. git add/commit/push -u origin main 存回檔案分支

## pull 會有  rebase false|true，ff， merge衝突解決方式
## Windows 有 credential-manager Auth 比較簡單，不用Token
