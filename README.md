# DigitalTwin_AutoDriving

### ROKEY 3기 디지털 트윈 기반 서비스 로봇 운영 시스템 구성
- 프로젝트 기간: 2025.06.23 ~ 2025.07.04 (12일)
- 참여인원: 4명

<br>

## 🎥 프로젝트 소개
[![Video Label](http://img.youtube.com/vi/pKlhblwV81o/0.jpg)](https://youtu.be/pKlhblwV81o)
  ➡ 영상 클릭 시, youtube 재생
  
**vF1**은 **도로 환경 요소 인식**과 물리적 **장애물 제거**를 수행하는 **디지털 트윈 기반 자율주행 시스템**입니다.
- **TurtleBot3 Burger (Jetson Orin)**, **OpenMANIPULATOR-X**, **Logitech C270 웹캠**,
**OpenCV**, **PyQt5 기반 GUI 제어**, **ROS2 Humble**
- 신호등/차단바/표지판 인식 → 경로/속도/정지 제어까지 실시간 주행 제어 수행
- GUI 기반 사용자 제어와 디지털 트윈 환경에서 반복 실험 가능

<br>

## 🔧 주요 기능
- 🚦 신호등 인식: 빨간불 대기, 초록불 시 주행 시작
- 🛑 차단바 인식: 수평/수직 상태에 따라 정지 및 이동 결정
- 🪧 교차로 표지판 인식: 좌/우 방향 지시에 따른 경로 변경
- ⚙️ 속도 제어: 감속/가속 표지판에 따라 실시간 속도 조절
- 🖥️ PyQt5 GUI 제어: 긴급 정지 및 주행 재개, 로봇 상태 모니터링 등 UI 제공
- 🧪 디지털 트윈 실험 환경: 조명, 거리, 각도 변화에 대한 반복 테스트 및 알고리즘 튜닝 가능

<br>

## 🚀 전체 실행 순서

📦 파일 다운로드
```
mkdir ~/DigitalTwin_AutoDriving/
cd ~/DigitalTwin_AutoDriving/
git clone https://github.com/checkjunghyeon/DigitalTwin_AutoDriving.git

colcon build --symlink-install
```

<br>

## ✅ (1) 시뮬레이션 버전(Gazebo)
#### 🔹Install Dependent ROS 2 Packages
```
$ sudo apt install ros-humble-gazebo-*
$ sudo apt install ros-humble-cartographer
$ sudo apt install ros-humble-cartographer-ros
$ sudo apt install ros-humble-navigation2
$ sudo apt install ros-humble-nav2-bringup
```

#### 🔹Install TurtleBot3 Packages
```
$ source /opt/ros/humble/setup.bash
$ mkdir -p ~/turtlebot3_ws/src
$ cd ~/turtlebot3_ws/src/
$ git clone -b humble https://github.com/ROBOTIS-GIT/DynamixelSDK.git
$ git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
$ git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3.git
$ sudo apt install python3-colcon-common-extensions
$ cd ~/turtlebot3_ws
$ colcon build --symlink-install
$ echo 'source ~/turtlebot3_ws/install/setup.bash' >> ~/.bashrc
$ source ~/.bashrc
```

#### 🔹Environment Configuration
```
$ echo 'export ROS_DOMAIN_ID=30 #TURTLEBOT3' >> ~/.bashrc
$ echo 'source /usr/share/gazebo/setup.sh' >> ~/.bashrc
$ echo 'source /opt/ros/humble/setup.bash' >> ~/.bashrc
$ source ~/.bashrc
```

#### 🔹Install Simulation Package
```
$ cd ~/turtlebot3_ws/src/
$ git clone -b humble https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
$ cd ~/turtlebot3_ws && colcon build --symlink-install
```

#### 🔹Basic Setting
```
$ cd ~/turtlebot3_ws/src/
$ git clone https://github.com/ROBOTIS-GIT/turtlebot3_autorace.git
$ cd ~/turtlebot3_ws && colcon build --symlink-install

$ sudo apt install ros-humble-image-transport ros-humble-cv-bridge ros-humble-vision-opencv python3-opencv libopencv-dev ros-humble-image-pipeline
$ echo 'export GAZEBO_PLUGIN_PATH=$HOME/turtlebot3_ws/build/turtlebot3_gazebo:$GAZEBO_PLUGIN_PATH' >> ~/.bashrc
$ echo 'export TURTLEBOT3_MODEL=burger_cam' >> ~/.bashrc
```

#### 🔹Bringup(TurtleBot3 SBC)
```
$ ros2 launch turtlebot3_manipulation_bringup hardware.launch.py
```

#### 🔹Simulation with MoveIt2!
```
$ ros2 launch turtlebot3_manipulation_moveit_config moveit_gazebo.launch.py
```
➡️➡️➡️ Goal State를 lane_tracking3으로 선택 후, Plan & Execute 버튼 클릭

<br>

#### 🔹System Running
```
# Terminal 1
$ ros2 launch turtlebot3_gazebo turtlebot3_autorace_2020.launch.py

# Terminal 2
$ ros2 launch turtlebot3_autorace_camera intrinsic_camera_calibration.launch.py

# Terminal 3
$ ros2 launch turtlebot3_autorace_camera extrinsic_camera_calibration.launch.py

# Terminal 4
$ ros2 launch turtlebot3_autorace_detect detect_lane.launch.py calibration_mode:=True

# Terminal 5
$ ros2 launch turtlebot3_autorace_detect detect_signcombine.launch.py

# Terminal 6
$ ros2 launch turtlebot3_autorace_detect detect_level_crossing.launch.py

# Terminal 7
$ ros2 launch turtlebot3_autorace_mission control_lane.launch.py
```

#### Terminal 8
```
$ cd ~/{your_ws}/src/pyqt5_gui
$ python3 main_window.py
```

<br>

## ✅ (2) 실환경 버전(Gazebo)
