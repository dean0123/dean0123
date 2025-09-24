# ubuntu 22.04.5

```sh   (Put into ~/.zshrc)
# ======= Dean Added .zshrc ========

# -------- 1: Color  ---------
export LS_COLORS=${LS_COLORS}'di=01;36';
alias ls='ls --color=auto'
alias ll='ls -alrt'

#
# -------- 2: Prompt Git ---------
autoload -Uz vcs_info
precmd() { vcs_info }
zstyle ':vcs_info:git:*' formats '(%b)%f'
setopt PROMPT_SUBST
PROMPT='%F{green}%n %B%F{green}%m%f%b%f %F{39}%~%f${vcs_info_msg_0_}%(!.#.$) '
PROMPT='%F{184}%n%f %K{blue}%B%F{2}%m%f%b%k %F{39}%~%f%F{181}${vcs_info_msg_0_}%f%(!.#.$) '
# %B--%b 是粗體, %K--%k 是設定底色 %F--%f是字型顏色# --> 右邊也顯示 GIT Branch R-PROMPT
RPROMPT=\$vcs_info_msg_0_

# -------- 3: Hisroty ----------
setopt histignorealldups sharehistory
HISTSIZE=10000
SAVEHIST=10000
HISTFILE=~/.zsh_history

# -------- 4: Syntax, Suggestion, Substring  -------
source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh-history-substring-search/zsh-history-substring-search.zsh
bindkey "$terminfo[kcuu1]" history-substring-search-up
bindkey "$terminfo[kcud1]" history-substring-search-down

# -------- 5: Complete  -----------
autoload -Uz compinit
compinit
setopt AUTO_CD AUTO_LIST AUTO_PARAM_KEYS

```






## 1. zsh 換 目錄顏色
將以下放入 .zshrc 後面
```
export LS_COLORS=${LS_COLORS}'di=01;36';
alias ls='ls --color=auto'
alias ll='ls -alrt'
```

## 2. zsh 手動設定 Prompt
``` 
# 放入 ~/.zshrc
autoload -Uz vcs_info; 
precmd() { vcs_info }
zstyle ':vcs_info:git:*' formats  '(%b)%f'
setopt PROMPT_SUBST
PROMPT='%F{184}%n%f %F{2}%m%f %F{39}%~%f%F{181}${vcs_info_msg_0_}%f%(!.#.$) '  
# --> 右邊也顯示 GIT Branch R-PROMPT
RPROMPT=\$vcs_info_msg_0_

```




## 2-1. zsh 預設 Prompt Theme adm1
 
```
# 放入 ~/.zshrc
autoload -Uz promptinit  #載入
promptinit               #啟動
prompt -p                #列出所有 prompt theme
prompt adam1             #設為 adam1 theme
```

- 若要 修改 預設 theme 內容
  1. `vi /usr/share/zsh/functions/Prompts/prompt_adam1_setup`. 

  1. 去掉 $prompt_newline 可以不換行
  2. PS1 後面 %#  --> 改成 $
  3. 重新登入 設定 prompt thmem  








# zsh 四大天王

```
zsh-users/zsh-completions       #按TAB 自動完成
zsh-users/zsh-autosuggestions   #自動最後指令 灰色
zsh-users/zsh-history-substring-search      #上下尋找
zdharma-continuum/fast-syntax-highlighting  #語法顏色
```

## 1. 建議灰色 suggestion 語法彩色syntax
```sh
apt install zsh zsh-syntax-highlighting zsh-autosuggestions

cat <<'ZRC' >> ~/.zshrc
# 輸入時的灰色建議, 語法顏色
source /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
ZRC
```


## 2. 尋找 history substring search
- 一般history 設定
```
setopt histignorealldups sharehistory
HISTSIZE=10000
SAVEHIST=10000
HISTFILE=~/.zsh_history
```

- 尋找history 設定
git pull https://github.com/zsh-users/zsh-history-substring-search.git

放到 /usr/share/zsh-history-substring-search 下
source /usr/share/zsh-history-substring-search/
```
$ zsh-history-substring-search.zsh
$ bindkey "$terminfo[kcuu1]" history-substring-search-up
$ bindkey "$terminfo[kcud1]" history-substring-search-down
```

## 3 Complete 完成
算了 不用了, 用基本就好
```
autoload -Uz compinit
compinit
setopt AUTO_CD AUTO_LIST AUTO_PARAM_KEYS
```