---
title: "Linux Mint Setting"
date: 2020-07-27 15:59:00 -0400
categories: linux
---

####  Linux Mint 한글 설정
```
$ sudo apt-get install nabi
$ im-config
hangul 선택
```

#### zsh 적용
````
$ sudo apt-get install zsh
$ chsh -s /usr/bin/zsh
$ sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# ~/.zshrc를 열어서 theme를 agnoster로 변경

# 폰트 다운
$ sudo apt intsll fonts-powerline

# ~/.zshrc를 열어서 DEFAULT_USER추가
# DEFAULT_USER
DEFAULT_USER="cwsfa"

$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
$ echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```
