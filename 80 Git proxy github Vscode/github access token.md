ghp_tSJPd2CNZU26wQGux53g2amZifakefake
(2025-7-23 產生新的) 


# 1 用Github commnad line HTTPS : 不能再用 password 必須改用 Personnal Access Token(PAT)， 或 Fine-grained Personal Access Token (FG PAT)


## 幾種 git remote 的方法 

1. https (https://github.com/dean0123/fastapi.git)

    1.1 windows 可用 git credential-manager 就不用，每次輸入token

    1.2 lunix 用credentail-manager 要安裝 .NET 不佳。 直接每次輸入token 麻煩。

2. ssh (git@github.com:dean0123/fastapi.git)


3. GitHub CLI






## SSH git@ 。。。。
``` 
git remote add origin git@github.com:dean0123/fastapi.git
```
```
git remote -v
origin  git@github.com:dean0123/fastapi.git (fetch)
origin  git@github.com:dean0123/fastapi.git (push)
```
