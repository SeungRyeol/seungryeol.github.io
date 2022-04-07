---
title: "Linux Mint Setting"
date: 2020-07-27 15:59:00 -0400
categories: linux
---

#### Linux Mint 한글 설정

```bash
sudo apt-get install nabi
im-config
# hangul 선택 진행
```

#### Terminator 셋팅 ([테마설정](https://github.com/EliverLara/terminator-themes))

```bash
sudo apt install terminator
```

#### zsh 적용

```bash
sudo apt-get install zsh
chsh -s /usr/bin/zsh
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# 폰트 다운
sudo apt install fonts-powerline

# ~/.zshrc를 열어서 DEFAULT_USER추가
# DEFAULT_USER
DEFAULT_USER="cwsfa"

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc

# 테마
https://velog.io/@yujo/Ubuntu-20.04%EC%9A%B0%EB%B6%84%ED%88%AC-Terminal-%EC%84%B8%ED%8C%85

```

#### fusuma (touchpad gesture)

```bash
sudo apt-get install libinput-tools
sudo apt-get install ruby
sudo gem install fusuma
sudo apt-get install xdotool
```

config 파일 생성

```bash
mkdir -p ~/.config/fusuma
vim ~/.config/fusuma/config.yml
```

config.yml

```yaml
swipe:
  4:
    up:
      command: 'xdotool key ctrl+alt+Up'  # Show all workspaces
    down:
      command: 'xdotool key ctrl+alt+Down'  # Show all windows
    right:
      command: 'xdotool key ctrl+alt+Left'  # Workspace left
    left:
      command: 'xdotool key ctrl+alt+Right'  # Workspace right
  3:
    up:
      command: 'xdotool key alt+space'  # Albert
    down:
      command: 'xdotool key alt+space'  # Albert
    right:
      command: 'xdotool key alt+Right'  # History forward
    left:
      command: 'xdotool key alt+Left'  # History back

threshold:
  swipe: 1
  pinch: 1

interval:
  swipe: 1
  pinch: 1
```

#### 기타 설치

```bash
sudo apt install terminator
sudo apt install peek # gif capture
```
