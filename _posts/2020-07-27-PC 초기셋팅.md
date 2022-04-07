---
title: "Linux 초기 PC 셋팅"
date: 2020-07-27 15:56:28 -0400
categories: linux
---

#### 터미네이터 설치 방법

1. 다운로드

    ```bash
    sudo apt install terminator
    ```

2. $ vi ~/.config/terminator/config에 입력

    ```text
    [global_config]
        focus = system
        suppress_multiple_term_dialog = True
        tab_position = bottom
        title_transmit_bg_color = "#d30102"
        window_state = maximise
    [keybindings]
    [layouts]
        [[default]]
        [[[child1]]]
            parent = window0
            type = Terminal
        [[[window0]]]
            parent = ""
            type = Window
    [plugins]
    [profiles]
        [[default]]
        background_color = "#002b36"
        background_darkness = 0.85
        background_image = None
        background_type = transparent
        cursor_color = "#eee8d5"
        font = Monospace 11
        foreground_color = "#e6e0da"
        icon_bell = False
        palette = "#073642:#dc322f:#859900:#b58900:#268bd2:#d33682:#2aa198:#eee8d5:#586e75:#cb4b16:#586e75:#657b83:#839496:#6c71c4:#93a1a1:#fdf6e3"
        split_to_group = True

    ```

3. 최종 설정

    ```bash
    gsettings set org.gnome.desktop.default-applications.terminal exec '/usr/bin/terminator'
    ```

#### Telegram 설치 방법

```bash
sudo apt install snapd
sudo snap install telegram-desktop
```

한글 입력 방법

```bash
sudo apt install fcitx-hangul
sudo apt install fcitx-config-gtk
'언어지원' 들어가서 기본적인 설치 완료
키보드 입력방법을 fcitx로 변경 후 재부팅
```

#### 메뉴바 런쳐 사라졌을 때

```bash
rm -rf ~/.config/compiz-1/compizconfig/*
```

#### esp8266 설치 및 적용

```bash
1. 환경설정에서 추가
http://arduino.esp8266.com/stable/package_esp8266com_index.json
2. 보드매니저에서 esp관련파일 설치
3. 추가 세팅
Flash Size : "4M (3M SPIFFS)"
Upload Speed: "921600"
```

#### CubeMX linux install

```bash
# 1. .linux 파일용 라이브러리 설치
sudo apt install lib32z1

# 2. 설치 파일이 있는 폴더
chmod 777 SetupSTM32CubeMX-5.4.0.linux
./SetupSTM32CubeMX-5.4.0.linux
```

#### Chrome

```bash
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
sudo apt update
sudo apt install google-chrome-stable
```

#### VSCODE

```bash
sudo apt install curl
sudo sh -c 'curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /etc/apt/trusted.gpg.d/microsoft.gpg'
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install code
```

#### VSCODE (ARM 계열)

```bash
sudo apt install git libx11-dev libxkbfile-dev libsecret-1-dev fakeroot rpm libnss3 apt-transport-https
sudo apt install curl
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt install -y nodejs
nodejs -v
sudo apt install gcc g++ make
curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update
sudo apt install yarn # check if yarn installation is ok using the command
yarn --version
git clone https://github.com/microsoft/vscode
------------------------
cd vscode
yarn
yarn run watch
----------vscode 폴더로 이동 ------------
./scripts/code.sh
```
