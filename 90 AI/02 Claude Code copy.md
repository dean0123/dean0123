## install setup (export PROXY)
## 1. install node@22 https://nodejs.org/

```
brew install node@22
```

If you need to have node@22 first in your PATH, run:
```
$ echo 'export PATH="/opt/homebrew/opt/node@22/bin:$PATH"' >> ~/.zshrc
```
For compilers to find node@22 you may need to set:
```
$ export LDFLAGS="-L/opt/homebrew/opt/node@22/lib"
$ export CPPFLAGS="-I/opt/homebrew/opt/node@22/include"
```
驗證 node npm 
```
$ node --version
v22.20.0
$ npm --version 
10.9.3
$ npx --version 
10.9.3

```
## 2. install Claude Code on Mac  https://docs.claude.com/zh-TW/docs/claude-code/setup

```
$ brew install --cask claude-code 
$ claude --version
2.0.5 (Claude Code)


$ brew update
$ brew upgrade --cask claude-code 
$ claude --version
2.0.14 (Claude Code)
```


## 3. 登入 使用
到 https://aistudio.google.com/ 建立/取得 API Key ：
API Key ： AIzaSyCyTqltPf9nn3rvXd_aXBaLs_KhJ-AgUJw
Name ： Z00 Compeq Ai Coding Key
Project Name ： projects/716648977913
Project Number ： 716648977913

```


```

