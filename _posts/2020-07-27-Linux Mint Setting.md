---
title: "Linux Mint Setting"
date: 2020-07-27 15:59:00 -0400
categories: linux
---

#### Linux Mint 한글 설정
```
$ sudo apt-get install nabi
$ im-config
hangul 선택
```

#### zsh 적용
```
$ sudo apt-get install zsh
$ chsh -s /usr/bin/zsh
$ sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# 폰트 다운
$ sudo apt install fonts-powerline

# ~/.zshrc를 열어서 DEFAULT_USER추가
# DEFAULT_USER
DEFAULT_USER="cwsfa"

$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
$ echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc

# 테마
https://velog.io/@yujo/Ubuntu-20.04%EC%9A%B0%EB%B6%84%ED%88%AC-Terminal-%EC%84%B8%ED%8C%85

```

