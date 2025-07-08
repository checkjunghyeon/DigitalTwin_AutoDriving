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

✅ **(1) **

```
```
