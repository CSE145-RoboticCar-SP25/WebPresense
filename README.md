# Autonomous Obstacle-Avoiding Robotic Car
### CSE 145 Spring 2025 | Fast Robotics Team

<div align="center">
  <img src="resources/mbot1.png" width="350" height="400"  style="object-fit: cover; border-radius: 8px;">
  <p><em>Our autonomous robotic car integrating RB5 and mBot Mega platforms</em></p>
</div>

[![ROS2](https://img.shields.io/badge/ROS-Foxy-blue)](https://docs.ros.org/en/foxy/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-orange)](https://ubuntu.com/)
[![Python](https://img.shields.io/badge/Python-3.8+-green)](https://python.org)

## 🚀 Quick Start

```bash
# Clone the robotic car repository into ROS2 workspace
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
git clone https://github.com/SamvathnaEm/CSE145_RoboticCar.git
cd ~/ros2_ws

# Source ROS2 environment
source /opt/ros/foxy/setup.bash

# Build all ROS2 packages
colcon build --symlink-install
source install/setup.bash

# Terminal 1: Launch camera and vision system
ros2 launch rb5_ros2_vision rb_camera_main_ocv_launch.py

# Terminal 2: Launch web interface
ros2 run rb5_ros2_control combined_flask_server.py

# Terminal 3: Launch robot control node
ros2 run rb5_keyjoy_control_node.py

# Access web interface at http://<RB5_IP>:8004
```

## 📋 Table of Contents

- [Autonomous Obstacle-Avoiding Robotic Car](#autonomous-obstacle-avoiding-robotic-car)
    - [CSE 145 Spring 2025 | Fast Robotics Team](#cse-145-spring-2025--fast-robotics-team)
  - [🚀 Quick Start](#-quick-start)
  - [📋 Table of Contents](#-table-of-contents)
  - [🎯 About The Project](#-about-the-project)
    - [Abstract](#abstract)
    - [Technical Specifications](#technical-specifications)
  - [🏗️ System Architecture](#️-system-architecture)
  - [🔧 Hardware Requirements](#-hardware-requirements)
    - [Essential Components](#essential-components)
    - [Optional Components](#optional-components)
  - [💻 Software Setup](#-software-setup)
    - [Installation Steps](#installation-steps)
  - [📁 Repository Structure](#-repository-structure)
  - [🎮 Usage Guide](#-usage-guide)
    - [Basic Operation](#basic-operation)
  - [🌐 Web Interface](#-web-interface)
    - [Features](#features)
    - [Technical Implementation](#technical-implementation)
  - [🎥 Demo Videos](#-demo-videos)
  - [🚀 Future Enhancements](#-future-enhancements)
    - [Planned Features](#planned-features)
    - [Research Opportunities](#research-opportunities)
  - [🙏 Acknowledgments](#-acknowledgments)

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
### Installation Steps

1. **Clone the Main Code Repository**
   ```bash
   # Create ROS2 workspace structure
   mkdir -p ~/ros2_ws/src
   cd ~/ros2_ws/src
   git clone https://github.com/SamvathnaEm/CSE145_RoboticCar.git
   cd ~/ros2_ws
   ```
   
   > **Note**: This project builds upon the [UCSD CSE 276A RB5 ROS2 starter code](https://github.com/AutonomousVehicleLaboratory/rb5_ros2/tree/fa24_cse276a) with additional web interface and autonomous navigation features developed by our team.

2. **Setup ROS2 Environment**
   ```bash
   source /opt/ros/foxy/setup.bash
   colcon build --symlink-install
   source install/setup.bash
   ```

3. **Launch System Components**
   ```bash
   # Terminal 1: Camera and Vision
   ros2 launch rb5_ros2_vision rb_camera_main_ocv_launch.py
   
   # Terminal 2: Web Control Interface
   ros2 run rb5_ros2_control combined_flask_server.py
   
   # Terminal 3: Robot Control
   ros2 run rb5_keyjoy_control_node.py
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

1. **Start the System Components**
   ```bash
   # Terminal 1: Launch camera and vision
   ros2 launch rb5_ros2_vision rb_camera_main_ocv_launch.py
   
   # Terminal 2: Launch web server
   ros2 run rb5_ros2_control combined_flask_server.py
   
   # Terminal 3: Launch robot control
   ros2 run rb5_keyjoy_control_node.py
   ```

2. **Access Web Interface**
   - Open browser to `http://<RB5_IP>:8004`
   - Use on-screen controls for manual operation
   - Monitor live camera feed

3. **Autonomous Mode**
   - Click "AUTO" button in web interface
   - Robot will navigate and avoid AprilTag obstacles
   - Monitor system status in terminal

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

## 🎥 Demo Videos
| Milestone | Description | Video Link |
|-----------|-------------|------------|
| **Milestone 1** | Basic motion control | [![Demo](https://img.shields.io/badge/▶️-Watch-red)](https://youtube.com/shorts/3WjsdgmxzQk?si=Hlpb7G_hmRHQ9anV) |
| **Milestone 2** | Open loop control | [![Demo](https://img.shields.io/badge/▶️-Watch-red)](https://youtube.com/shorts/IcfyvWsRw90) |
| **Milestone 3** | Closed loop AprilTag | [![Demo](https://img.shields.io/badge/▶️-Watch-red)](https://www.youtube.com/watch?v=pJJRyhtKATg) |

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

## 🙏 Acknowledgments

- **UC San Diego CSE 145** - Course support and guidance
- **UC San Diego CSE 276A** - [RB5 ROS2 starter code](https://github.com/AutonomousVehicleLaboratory/rb5_ros2/tree/fa24_cse276a) from Autonomous Vehicle Laboratory
- **Qualcomm** - RB5 development board documentation
- **ROS2 Community** - Framework and package ecosystem
- **AprilTag Library** - Computer vision detection system
- **Thank you, Rohan Patil - Computer Science PhD Student at UC San Diego,** for your continuous support, guidance, and helpful advice throughout our project.
- **Thank you, Julian Raheems - Computer Science and Engineering PhD Candidate at UC San Diego,** for your time, effort, and valuable insights that helped us stay on track and successfully complete this project.

<div align="center">
  <p><strong>Built with ❤️ by Fast Robotics Team</strong></p>
  <p><em>Autonomous robotics for the future</em></p>
</div>
