---
title: "ROS1 systemd"
date: 2020-09-11 14:30:00 -0400
categories: ros1
---

#### ROS1 Systemd

- Create a systemd unit file in /etc/systemd/system
```
cd /etc/systemd/system
sudo vim <service_name>.service
```  

## 1. roscore systemd 등록

- Create a systemd unit file for roscore
```
$ cd /etc/systemd/system
$ sudo vim roscore.service
```

- Create .sh unit file for roscore
```
$ cd /usr/local/bin/system
$ sudo vim roscore.sh
$ sudo chmod 755 roscore.sh
```

## 2. 명령어

- Unit 파일 생성/수정 후 systemd 변경사항을 시스템에 적용
```
$ sudo systemctl daemon-reload
```  

- Service를 수동으로 시작/중지
```
$ sudo systemctl start <service_name>.service
$ sudo systemctl stop <service_name>.service
```

- systemd unit이 부팅시 자동 시작되도록 설정/해제
```
$ sudo systemctl enable <service_name>.service
$ sudo systemctl disable <service_name>.service
```

- 서비스 로그 확인 (-b: 부팅 이후의 로그 / -e: 엔터를 통해 스크롤하지 않음(전체출력))
```
$ sudo systemctl status <service_name>.service
$ journalctl -u <service_name>.service -b -e
```
