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
## 2. install nvm , nvm use 22 set node version  to 22

## 2. install Gemini - CLI https://github.com/google-gemini/gemini-cli

```
$ brew install gemini-cli
$ gemini --version
0.7.0

$ brew update
$ brew upgrade gemini-cli
$ gemini --version
```


## 3. 登入 使用
到 https://aistudio.google.com/ 建立/取得 API Key ：
API Key ： AIzaSyCyTqltPf9nn3rvXd_aXBaLs_KhJ-AgUJw
Name ： Z00 Compeq Ai Coding Key
Project Name ： projects/716648977913
Project Number ： 716648977913

```


```



----

# LINUX install Node/npm/gemini-cli

```
sudo apt update 
sudo apt install nodejs npm
node --version
npm --version
npm config set proxy       http://10.1.229.229:15629                       
npm config set https-proxy http://10.1.229.229:15629 

sudo npm search gemino-cli
sudo npm --proxy http://10.1.229.229:15629 install -g @google/gemini-cli


```