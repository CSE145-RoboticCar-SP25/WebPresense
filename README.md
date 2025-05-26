# Robotic Car (Autonomos Obstacle-Avoiding Robot Car (with RB5 + mBot) project

<img src="mbot1.png" width="500" height="500">

  
## About The Project
### Motivation - Why are you committing to this project?
**1. Eugenie**

Inspired by the robotic systems we encounter in everyday life such as autonomous vacuum cleaners, self-driving cars, and warehouse robots, we're excited to explore how these technologies are built from the ground up. This project gives us the opportunity to bridge theory with practice by integrating concepts from both our machine learning and web application development courses. We're not only interested in developing an obstacle-avoiding robot but also in enhancing it with intelligent behavior, real-time data processing, or a web-based interface for remote control. By working on this project, we aim to deepen our technical skills, understand the challenges of building smart systems, and push the boundaries of what we can create as a team.

**2. Momina**

I am excited to build something hands-on that combines embedded systems and robotics. I became especially interested in this topic after attending a workshop at my college where we built a basic robotic car with simple sensors. It was a great experience that introduced me to the foundations of robot design, but we didn’t have the chance to explore the AI side of things. This project gives me the opportunity to take that experience further by not only creating an obstacle-avoiding robot but also learning how to integrate smarter features like AI and intelligent navigation. I’ve always wanted to understand how autonomous systems work in the real world, and this project is a perfect way to explore how Arduino, RB5 sensors, motors, and AI can work together in real time.

**3. Emma**

I have always dreamed of building a robot, and this project gives me the great opportunity to bring that dream to life. By making a robotic car, I can apply my understanding and knowledge on hardware, software and AI, machine learning into a hands-on, meaningful experience. I am also lucky to have teammates that share the same passion and interest in creating a robotic car. We want to combine what we have learned to build an obstacle-avoiding robot car using AI and machine learning.

**4. Sam**

I am genuinely committed to this project because building a robot has been a personal goal of mine since transferring here. I also want to take what I’ve already learned from machine learning and web development to parallel computing and apply those skills to embedded hardware using the RB5 and mBot. I am excited to try adding something creative and original to the robotic car as well.

_________________________________________________________

### Abstract

This project presents the design and development of an autonomous robotic car capable of detecting and avoiding obstacles in real time using camera-based vision. The system integrates the Qualcomm RB5 development board with the mBot Mega platform and runs on Ubuntu 22.04, using Robot Operating System (ROS 2 - Foxy) framework. Our Minimum Viable Product (MVP) was defined as navigating a 1.5 m × 1.5 m test space, detecting obstacles within 30 cm, and responding within 500 milliseconds. The robot uses its onboard camera and AprilTag detection to identify obstacles and adjust its movement accordingly. By eliminating infrared and ultrasonic sensors and relying entirely on visual input and an IMU sensor, the robot achieves closed-loop behavior with real-time responsiveness. Built with accessible components and modular ROS 2 software, the system provides a strong foundation for future enhancements such as full SLAM integration, dynamic path planning with Nav2, and real-time mapping using ORB-SLAM3.

________________________________________________________

### Introduction

Autonomous robotic systems play a critical role in modern applications, from delivery services to home automation and industrial operations. These systems rely on real-time navigation and obstacle avoidance to perform tasks safely and effectively without human intervention. Inspired by technologies like robot vacuum cleaners and delivery robots, our project focuses on building a low-cost autonomous robotic car that can navigate a small indoor space and avoid obstacles using vision-based perception.

Our robot is built on the mBot Mega platform for motor control and uses the Qualcomm RB5 development board for onboard processing and camera-based sensing. The system runs Ubuntu 22.04 and uses Robot Operating System 2 (ROS 2) as its main software framework. The robot detects its environment using the RB5’s onboard camera and identifies obstacles through AprilTag detection. It reacts by adjusting its motion in real time when a tag (representing an obstacle) is detected within a 30 cm range, responding in under 500 milliseconds.
This project served as an educational opportunity for our team to apply skills in robotics, computer vision, embedded systems, and collaborative software development. We structured the work into clear milestones: beginning with open-loop motion control, then establishing camera integration and AprilTag detection, and finally preparing for path planning using SLAM-based odometry and the Nav2 framework.

