

## 1. 基本顏色設定

### 不要裝 Oh-My-Zsh 很難設定
最近設定， 只設定 會的
```sh 
source /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /opt/homebrew/share/zsh-history-substring-search/zsh-history-substring-search.zsh
bindkey '^[[A' history-substring-search-up
bindkey '^[[B' history-substring-search-down


alias ls='ls -GF's
alias ll='ls -lhGrt'
alias la='ls -lahG'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'


# LSCOLORS: 近似 Ubuntu 的目錄/檔案色彩
# export LSCOLORS=GxFxCxDxBxegedabagaced


# ---- Ubuntu 風格 Prompt：user@host:cwd (git) $ ----
autoload -Uz vcs_info
precmd_vcs_info() { vcs_info }
precmd_functions+=( precmd_vcs_info )
setopt prompt_subst
RPROMPT=\$vcs_info_msg_0_
# PROMPT=\$vcs_info_msg_0_'%# '
zstyle ':vcs_info:git:*' formats '(%b)'

# 綠色 user@host，藍色目前目錄，括號顯示 git 分支，最後 $（root 變 #）
PROMPT='%F{green}%n@%m%f:%F{cyan}%~%f${vcs_info_msg_0_}%(!.#.$) '

```



```sh
cat <<'ZRC' >> ~/.zshrc

##### --- Ubuntu 風格：顏色與提示字串（zsh）--- #####

# ls/grep/less 基本顏色（BSD 工具）
export CLICOLOR=1
# LSCOLORS: 近似 Ubuntu 的目錄/檔案色彩
export LSCOLORS=GxFxCxDxBxegedabagaced

# ls 常用別名（會自動偵測 gnu ls / bsd ls）
if command -v gls >/dev/null 2>&1; then
  alias ls='gls --color=auto -F'
  alias ll='gls --color=auto -lh'
  alias la='gls --color=auto -lah'
else
  alias ls='ls -GF'
  alias ll='ls -lhG'
  alias la='ls -lahG'
fi

alias ls='ls -GF's
alias ll='ls -lhGrt'
alias la='ls -lahG'
alias grep='grep --color=auto'


# grep 顏色（若有 ggrep 就用它，否則用內建 grep）
if command -v ggrep >/dev/null 2>&1; then
  alias grep='ggrep --color=auto'
  alias egrep='gegrep --color=auto'
  alias fgrep='gfgrep --color=auto'
fi

# less 顯示 ANSI 顏色
export LESS='-R'

# ---- Ubuntu 風格 Prompt：user@host:cwd (git) $ ----
autoload -Uz vcs_info
precmd_vcs_info() { vcs_info }
precmd_functions+=( precmd_vcs_info )
setopt prompt_subst
RPROMPT=\$vcs_info_msg_0_
# PROMPT=\$vcs_info_msg_0_'%# '
zstyle ':vcs_info:git:*' formats '(%b)'


# 綠色 user@host，藍色目前目錄，括號顯示 git 分支，最後 $（root 變 #）
PROMPT='%F{green}%n@%m%f:%F{blue}%~%f${vcs_info_msg_0_}%(!.#.$) '

# 便利性：自動完成與列出
autoload -Uz compinit; compinit
setopt AUTO_CD AUTO_LIST AUTO_PARAM_KEYS

# 歷史記錄
HISTFILE=~/.zsh_history
HISTSIZE=10000
SAVEHIST=10000
setopt HIST_IGNORE_ALL_DUPS SHARE_HISTORY

ZRC

# 套用設定
source ~/.zshrc


```


brew install zsh-substring-search

```
# -------- 4: Syntax, Suggestion, Substring  -------
source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh-history-substring-search/zsh-history-substring-search.zsh
bindkey '^[[A'             history-substring-search-up
bindkey '^[[B'             history-substring-search-down
# 如果上面兩行不行, 就執行下面兩行
bindkey "$terminfo[kcuu1]" history-substring-search-up
bindkey "$terminfo[kcud1]" history-substring-search-down
```


## 2. 指令建議 語法 亮度
```sh
brew install zsh-autosuggestions zsh-syntax-highlighting
cat <<'ZRC' >> ~/.zshrc

# 輸入時的灰色建議
if command -v brew >/dev/null 2>&1; then
  ZSH_SHARE="$(brew --prefix)/share"
  [ -r "$ZSH_SHARE/zsh-autosuggestions/zsh-autosuggestions.zsh" ] && \
    source "$ZSH_SHARE/zsh-autosuggestions/zsh-autosuggestions.zsh"
  # 注意：syntax-highlighting 建議放在檔案最後載入
  [ -r "$ZSH_SHARE/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" ] && \
    source "$ZSH_SHARE/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh"
fi




bindkey '^[[A' history-substring-search-up
bindkey '^[[B' history-substring-search-down

ZRC

source ~/.zshrcsu
```


## 3. 外掛 Terminal (iTerm2) 與 Font (Nerd)
```sh
# 安裝 iTerm2
brew install --cask iterm2

# 安裝 Nerd Font（讓 eza/提示字元圖示顯示正常）
brew tap homebrew/cask-fonts
brew install --cask font-meslo-lg-nerd-font
brew install --cask font-sf-moni. (這個字型比較好看,Apple原來的)

# 選LGS Small 的 比較好
```
- 打開 iTerm2 > Settings > Profiles > Text，字型選：MesloLGS NF（或其他 Nerd Font）。
- 顏色可選內建暗色系；若想更像 Ubuntu，可挑溫暖/橘紫系配色。



## 4. vi 顏色 ～/。vimrc
```sh
syntax on
filetype plugin indent on
set term=builtin_ansi
```
