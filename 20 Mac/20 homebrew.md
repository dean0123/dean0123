



```
export HTTP_PROXY="http://10.1.229.229:15629/";export HTTPS_PROXY=$HTTP_PROXY; export ALL_PROXY=$HTTP_PROXY

# 安裝 Homebrew（官方指令）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"


```


```
# 使用 
brew info
brew list
brew search 
brew install
brew uninstall

# pkg 檔案都在 /opt/homebrew/share 下面
```


```
 $ brew list          
==> Formulae
ca-certificates		libidn2			tree
eza			libssh2			wget
gettext			libunistring		zsh-autocomplete
grep			openssl@3		zsh-autosuggestions
libgit2			pcre2			zsh-syntax-highlighting
==> Casks
font-meslo-lg-nerd-font	iterm2



deanliu Dean-Mac-Air ~/github/dean0123(main)$ brew list                                                    (main)
==> Formulae
ca-certificates			libssh2				sqlite
certifi				libunistring			tree
eza				libyaml				wget
fastapi				mpdecimal			xz
gettext				openssl@3			zsh-autocomplete
grep				pcre2				zsh-autosuggestions
libgit2				python@3.13			zsh-history-substring-search
libidn2				readline			zsh-syntax-highlighting

==> Casks
font-meslo-lg-nerd-font	font-sf-mono		iterm2



```



```
# 安裝 GNU 工具與實用工具
brew install coreutils findutils gnu-sed grep gawk
```