# Autonomous Obstacle-Avoiding Robotic Car
### CSE 145 Spring 2025 | Fast Robotics Team

<div align="center">
  <img src="resources/mbot1.png" width="500" height="400">
  <p><em>Our autonomous robotic car integrating RB5 and mBot Mega platforms</em></p>
</div>

[![ROS2](https://img.shields.io/badge/ROS-Foxy-blue)](https://docs.ros.org/en/foxy/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-orange)](https://ubuntu.com/)
[![Python](https://img.shields.io/badge/Python-3.8+-green)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)

## 🚀 Quick Start

```bash
# Clone the robotic car repository directly
git clone https://github.com/SamvathnaEm/CSE145_RoboticCar.git
cd CSE145_RoboticCar

# Source ROS2 environment
source /opt/ros/foxy/setup.bash

# Build all ROS2 packages
colcon build --symlink-install
source install/setup.bash

# Launch the camera and vision system
ros2 launch rb5_ros2_vision rb_camera_main_ocv_launch.py

# In a new terminal, launch the web interface
ros2 run rb5_ros2_control combined_flask_server.py

# Access web interface at http://<RB5_IP>:8004
```

## 📋 Table of Contents

- [About The Project](#about-the-project)
- [Team Members](#team-members)
- [System Architecture](#system-architecture)
- [Hardware Requirements](#hardware-requirements)
- [Software Setup](#software-setup)
- [Repository Structure](#repository-structure)
- [Usage Guide](#usage-guide)
- [Web Interface](#web-interface)
- [Documentation](#documentation)
- [Demo Videos](#demo-videos)
- [Future Enhancements](#future-enhancements)

## 🎯 About The Project

### Abstract

This project presents an autonomous robotic car capable of real-time obstacle detection and avoidance using camera-based vision. Built on the Qualcomm RB5 development board and mBot Mega platform, the system runs Ubuntu 22.04 with ROS 2 Foxy framework. Our robot achieves autonomous navigation in a 2m × 2m test space, detecting obstacles within 30cm and responding within 0.5s using AprilTag detection and visual processing.

**Key Features:**
- 🎯 Vision-based obstacle detection using AprilTags
- 🕹️ Real-time web-based control interface
- 🤖 ROS 2 Foxy integration for modular architecture
- 📷 Camera-based navigation without traditional sensors
- ⚡ Sub-500ms response time for obstacle avoidance
- 🌐 Flask web server for remote monitoring and control

### Technical Specifications

| Component | Specification |
|-----------|---------------|
| **Processing Unit** | Qualcomm RB5 Development Board |
| **Platform** | mBot Mega |
| **Operating System** | Ubuntu 22.04 LTS |
| **Framework** | ROS 2 Foxy |
| **Vision** | RB5 Onboard Camera + AprilTag Detection |
| **Control Interface** | Web-based (Flask + HTML/CSS/JS) |
| **Response Time** | < 500ms |
| **Navigation Area** | 2m × 2m indoor space |

## 👥 Team Members

| Name | Role | Contributions |
|------|------|---------------|
| **Eugenie** | Project Lead & AI Integration | Machine learning integration, system architecture, technical documentation |
| **Momina** | Embedded Systems Engineer | Hardware integration, sensor calibration, ROS2 node development |
| **Emma** | Robotics Software Developer | Navigation algorithms, obstacle avoidance logic, robot control systems |
| **Sam** | Web Developer & DevOps | Web interface, Flask server, repository management, CI/CD |

## 🏗️ System Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Web Interface │────│   Flask Server   │────│   ROS2 Bridge   │
│   (HTML/CSS/JS) │    │   (Python)       │    │   (Publisher)   │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                         │
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│  Camera Stream  │────│  AprilTag Node   │────│  Control Node   │
│   (rb5_vision)  │    │  (Detection)     │    │  (Navigation)   │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                         │
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Motor Control │────│   mBot Bridge    │────│   Joy Messages  │
│     (mBot)      │    │   (Serial)       │    │  (ROS2 Topic)   │
└─────────────────┘    └──────────────────┘    └─────────────────┘
```

## 🔧 Hardware Requirements

### Essential Components
- **Qualcomm RB5 Development Board** - Main processing unit
- **mBot Mega Platform** - Motor control and chassis
- **USB Camera** (if not using RB5 onboard camera)
- **Power Supply** - For RB5 and mBot
- **AprilTag Markers** - For obstacle detection testing

### Optional Components
- External monitor for debugging
- Wireless keyboard/mouse for setup
- Additional sensors (for future enhancements)

## 💻 Software Setup

### Prerequisites
```bash
# Ubuntu 22.04 LTS with ROS2 Foxy
sudo apt update && sudo apt upgrade -y

# Install ROS2 Foxy
sudo apt install ros-foxy-desktop python3-rosdep python3-colcon-common-extensions

# Install Python dependencies
pip3 install flask opencv-python numpy apriltag
```

### Installation Steps

1. **Clone Repository**
   ```bash
   git clone https://github.com/SamvathnaEm/CSE145_RoboticCar.git
   ```
   
   > **Note**: This project builds upon the [UCSD CSE 276A RB5 ROS2 starter code](https://github.com/AutonomousVehicleLaboratory/rb5_ros2/tree/fa24_cse276a) with additional web interface and autonomous navigation features.

2. **Setup ROS2 Environment**
   ```bash
   source /opt/ros/foxy/setup.bash
   cd CSE145_RoboticCar
   colcon build --symlink-install
   source install/setup.bash
   ```

3. **Configure Camera Parameters**
   ```bash
   # Edit camera configuration
   nano rb5_ros2_vision/config/camera_params.yaml
   ```

4. **Launch System**
   ```bash
   # Terminal 1: Camera and Vision
   ros2 launch rb5_ros2_vision rb_camera_main_ocv_launch.py
   
   # Terminal 2: Control Interface
   ros2 run rb5_ros2_control combined_flask_server.py
   
   # Terminal 3: AprilTag Detection
   ros2 run ros2_april_detection april_detection_node
   ```

## 📁 Repository Structure

```
WebPresense/
├── README.md                          # This file
├── .gitmodules                        # Git submodule configuration
├── resources/                         # Documentation assets
│   ├── mbot1.png
│   ├── mbot2.PNG
│   └── system_diagram.png
└── Robotic_Car/                       # Main robotic car submodule
    ├── README.md                      # Robotic car specific documentation
    ├── index.html                     # Project overview page
    ├── camera_viewer/                 # Camera streaming package
    │   ├── package.xml
    │   ├── setup.py
    │   └── camera_viewer/
    ├── key_joy/                       # Keyboard control package
    │   ├── CMakeLists.txt
    │   ├── package.xml
    │   └── key_joy/
    ├── my_rtabmap_odom/              # SLAM odometry package
    │   ├── CMakeLists.txt
    │   ├── package.xml
    │   ├── launch/
    │   └── my_rtabmap_odom/
    │       └── camera_info_publisher.py
    ├── rb5_ros2_control/             # Main control package
    │   ├── CMakeLists.txt
    │   ├── package.xml
    │   ├── setup.py
    │   └── rb5_ros2_control/
    │       ├── combined_flask_server.py    # Web server + ROS2 bridge
    │       ├── web_joy_server.py           # Basic web interface
    │       ├── templates/                  # HTML templates
    │       │   ├── index.html             # Main control interface
    │       │   └── control.html           # Simple control page
    │       └── static/                     # Web assets
    │           ├── css/
    │           │   ├── webflow.css
    │           │   └── robot-joy-controller.webflow.css
    │           ├── js/
    │           └── images/
    ├── rb5_ros2_vision/              # Vision processing package
    │   ├── CMakeLists.txt
    │   ├── package.xml
    │   ├── config/
    │   ├── include/
    │   ├── launch/
    │   └── src/
    └── ros2_april_detection/         # AprilTag detection package
        ├── CMakeLists.txt
        ├── package.xml
        ├── include/
        ├── launch/
        └── src/
```

## 🎮 Usage Guide

### Basic Operation

1. **Start the System**
   ```bash
   # Launch all nodes
   ros2 launch rb5_ros2_control robot_launch.py
   ```

2. **Access Web Interface**
   - Open browser to `http://<RB5_IP>:8004`
   - Use on-screen controls for manual operation
   - Monitor live camera feed

3. **Autonomous Mode**
   - Click "AUTO" button in web interface
   - Robot will navigate and avoid AprilTag obstacles
   - Monitor system status in terminal

### Control Options

- **Web Interface**: Full-featured control with camera feed
- **Keyboard Control**: Use `key_joy` package for direct control
- **ROS2 Topics**: Publish directly to `/joy` topic

### Monitoring

```bash
# View active topics
ros2 topic list

# Monitor joy commands
ros2 topic echo /joy

# Check camera feed
ros2 run rqt_image_view rqt_image_view
```

## 🌐 Web Interface

The web interface provides comprehensive control and monitoring capabilities:

### Features
- **Live Camera Feed**: Real-time video stream from robot camera
- **Directional Controls**: Forward, backward, left, right movement
- **Rotation Controls**: Clockwise and counter-clockwise rotation
- **Autonomous Mode**: Toggle for automatic obstacle avoidance
- **Status Monitoring**: Real-time system status and feedback

### Technical Implementation
- **Backend**: Flask server with ROS2 integration
- **Frontend**: Responsive HTML5/CSS3/JavaScript interface
- **Styling**: Custom Webflow-based design
- **Communication**: AJAX for real-time command sending

Access the interface at: `http://<robot-ip>:8004`

## 📚 Documentation

### Project Documentation
- [**Technical Report**](docs/technical_report.pdf) - Detailed system analysis
- [**User Manual**](docs/user_manual.md) - Complete setup and operation guide
- [**API Reference**](docs/api_reference.md) - ROS2 topics and services
- [**Hardware Guide**](docs/hardware_setup.md) - Assembly and wiring instructions

### ROS2 Package Documentation
- [**rb5_ros2_vision**](Robotic_Car/rb5_ros2_vision/README.md) - Camera and vision processing
- [**rb5_ros2_control**](Robotic_Car/rb5_ros2_control/README.md) - Control and web interface
- [**ros2_april_detection**](Robotic_Car/ros2_april_detection/README.md) - AprilTag detection
- [**my_rtabmap_odom**](Robotic_Car/my_rtabmap_odom/README.md) - SLAM odometry

## 🎥 Demo Videos

### Project Showcase
- [**Final Demonstration**](videos/final_demo.mp4) - Complete system operation
- [**Web Interface Tour**](videos/web_interface_demo.mp4) - Control interface walkthrough
- [**Autonomous Navigation**](videos/autonomous_demo.mp4) - Obstacle avoidance in action

### Development Progress
- [**Milestone 1**](videos/milestone1_demo.mp4) - Basic motion control
- [**Milestone 2**](videos/milestone2_demo.mp4) - Camera integration
- [**Milestone 3**](videos/milestone3_demo.mp4) - AprilTag detection

## 🚀 Future Enhancements

### Planned Features
- [ ] **Full SLAM Integration** - Complete mapping and localization
- [ ] **Nav2 Framework** - Advanced path planning and navigation
- [ ] **Multiple Obstacle Types** - Beyond AprilTag detection
- [ ] **Machine Learning** - Neural network-based obstacle classification
- [ ] **Mobile App** - Native iOS/Android control interface
- [ ] **Multi-Robot Coordination** - Swarm behavior implementation

### Research Opportunities
- Advanced computer vision algorithms
- Reinforcement learning for navigation
- Real-time mapping optimization
- Human-robot interaction interfaces

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **UC San Diego CSE 145** - Course support and guidance
- **UC San Diego CSE 276A** - [RB5 ROS2 starter code](https://github.com/AutonomousVehicleLaboratory/rb5_ros2/tree/fa24_cse276a) from Autonomous Vehicle Laboratory
- **Qualcomm** - RB5 development board documentation
- **ROS2 Community** - Framework and package ecosystem
- **AprilTag Library** - Computer vision detection system

## 📞 Contact

**Fast Robotics Team** - CSE 145 Spring 2025

- **Project Repository**: [https://github.com/YourUsername/WebPresense](https://github.com/YourUsername/WebPresense)
- **Documentation Wiki**: [Project Wiki](https://github.com/YourUsername/WebPresense/wiki)

---

<div align="center">
  <p><strong>Built with ❤️ by Fast Robotics Team</strong></p>
  <p><em>Autonomous robotics for the future</em></p>
</div>