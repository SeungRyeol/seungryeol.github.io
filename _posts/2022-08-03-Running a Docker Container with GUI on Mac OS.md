---
title: "Running a Docker Container with GUI on Mac OS"
date: 2022-08-03 13:37:00 -0400
categories: mac
use_math: true
---

1. Install XQuartz

    ```bash
    brew install xquartz
    ```

2. Run XQuartz

    ```bash
    open -a XQuartz
    ```

3. Allow Network Connections (XQuartz/Preferences)

    - [x] Authenticate connections
    - [x] Allow connections from network clients

4. Get the Host IP

    ```bash
    IP=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}')
    ```

5. SET DISPLAY Environment Variable

    ```bash
    export DISPLAY=$IP:0
    ```

6. Add Path to "xhost" to my zsh-Profile; added this line to .zshrc:

    ```bash
    export PATH=/usr/X11/bin/xhost:$PATH
    ```

7. Added the IP with xhost

    ```bash
    xhost + $IP
    ```

8. Run ROS Noetic from Docker Container (test)

    ```bash
    docker pull osrf/ros:noetic-desktop-full
    docker run -dit --platform linux/amd64 -e DISPLAY=$IP:0 -v /tmp/.X11-unix:/tmp --name ros osrf/ros:noetic-desktop-full
    ```
