---
title: "ROS1 Noetic & ROS2 Foxy Installation"
date: 2021-12-23 14:13:00 -0400
categories: ros2
---

Linux Mint 20.2 Uma 기준 설치 방법 입니다.

## ROS1 Noetic

- Debian package 설치

    ```bash
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu focal main" > /etc/apt/sources.list.d/ros-latest.list'
    sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
    sudo apt update
    sudo apt install ros-noetic-desktop-full
    ```

- 의존성 설정

    ```bash
    sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
    sudo apt install python3-rosdep
    sudo rosdep init
    rosdep update
    sudo apt install python3-osrf-pycommon
    sudo apt install python3-catkin-tools
    ```

- 작업 폴더 생성

    ```bash
    mkdir -p ~/catkin_ws/src
    cd catkin_ws
    catkin_init
    catkin build
    ```

## ROS2 Foxy

- Debian package 설치

    ```bash
    sudo apt update && sudo apt install locales
    sudo locale-gen en_US en_US.UTF-8
    sudo update-locale LC_ALL=en_US.UTF-8 hLANG=en_US.UTF-8
    export LANG=en_US.UTF-8

    sudo apt update && sudo apt install curl gnupg2 lsb-release
    sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

    sudo apt update
    sudo apt install ros-foxy-desktop
    sudo apt install -y python3-argcomplete
    ```

- 필수 패키지 설치

    ```bash
    sudo apt install ros-foxy-rmw-fastrtps-cpp
    sudo apt install ros-foxy-rmw-cyclonedds-cpp

    sudo apt update && sudo apt install -y build-essential cmake git libbullet-dev python3-colcon-common-extensions python3-flake8 python3-pip python3-pytest-cov python3-rosdep python3-setuptools python3-vcstool wget
    python3 -m pip install -U flake8-blind-except flake8-builtins flake8-class-newline flake8-comprehensions flake8-deprecated flake8-docstrings flake8-import-order flake8-quotes pytest-repeat pytest-rerunfailures pytest
    sudo apt install --no-install-recommends -y libasio-dev libtinyxml2-dev libcunit1-dev
    ```

## Noetic, Foxy 환경 설정 쉘 (zsh 사용 시, ~/.zshrc에 추가)

```bash
vim ~/.zshrc
```

```bash
# ROS1 & ROS2 Setup Function
noetic(){
    source /opt/ros/noetic/setup.zsh
    source ~/catkin_ws/devel/setup.zsh

    alias cw='cd ~/catkin_ws'
    alias cs='cd ~/catkin_ws/src'
    alias cb='cd ~/catkin_ws && catkin build'

    echo "ROS1 Noetic is Activated!"

    if [ $# -eq 1 ]
    then
        if [ $1 = "-n" ]
        then
            export ROS_MASTER_URI=http://192.168.0.16:11311
            export ROS_IP=192.168.0.3
        else
            echo "Invalid option."
        fi
    fi
}

foxy(){
    source /opt/ros/foxy/setup.zsh
    source ~/robot_ws/install/local_setup.zsh
    source ~/uros_ws/install/local_setup.zsh

    source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash
    source /usr/share/vcstool-completion/vcs.bash
    source /usr/share/colcon_cd/function/colcon_cd.sh
    export _colcon_cd_root=~/robot_ws

    export ROS_DOMAIN_ID=7
    # export ROS_NAMESPACE=robot1

    export RMW_IMPLEMENTATION=rmw_fastrtps_cpp
    # export RMW_IMPLEMENTATION=rmw_connext_cpp
    # export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
    # export RMW_IMPLEMENTATION=rmw_gurumdds_cpp

    # export RCUTILS_CONSOLE_OUTPUT_FORMAT='[{severity} {time}] [{name}]: {message} ({function_name}() at {file_name}:{line_number})'
    export RCUTILS_CONSOLE_OUTPUT_FORMAT='[{severity}]: {message}'
    export RCUTILS_COLORIZED_OUTPUT=1
    export RCUTILS_LOGGING_USE_STDOUT=0
    export RCUTILS_LOGGING_BUFFERED_STREAM=1

    alias cw='cd ~/robot_ws'
    alias cs='cd ~/robot_ws/src'
    alias ccd='colcon_cd'

    alias cb='cd ~/robot_ws && colcon build --symlink-install'
    alias cbs='colcon build --symlink-install'
    alias cbp='colcon build --symlink-install --packages-select'
    alias cbu='colcon build --symlink-install --packages-up-to'
    alias ct='colcon test'
    alias ctp='colcon test --packages-select'
    alias ctr='colcon test-result'

    alias tl='ros2 topic list'
    alias te='ros2 topic echo'
    alias nl='ros2 node list'

    alias killgazebo='killall -9 gazebo & killall -9 gzserver  & killall -9 gzclient'

    alias af='ament_flake8'
    alias ac='ament_cpplint'

    alias testpub='ros2 run demo_nodes_cpp talker'
    alias testsub='ros2 run demo_nodes_cpp listener'
    alias testpubimg='ros2 run image_tools cam2image'
    alias testsubimg='ros2 run image_tools showimage'

    echo "ROS2 Foxy is Activated!"
}

```

## Micro ROS agent

```bash
# Download & Install
foxy
mkdir uros_ws && cd uros_ws
git clone -b $ROS_DISTRO https://github.com/micro-ROS/micro_ros_setup.git src/micro_ros_setup
rosdep update && rosdep install --from-path src --ignore-src -y
colcon build

# Setup micro-ROS agent
source install/local_setup.zsh
ros2 run micro_ros_setup create_agent_ws.sh
ros2 run micro_ros_setup build_agent.sh
```
