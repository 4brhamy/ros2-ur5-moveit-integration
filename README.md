# ROS 2 Humble UR5 MoveIt Integration

![UR5 Simulation]<img width="1375" height="794" alt="image" src="https://github.com/user-attachments/assets/62c99d1d-27d7-4576-b1e2-8d21231c64d9" />)


## 🤖 Project Overview
This repository contains a complete simulation environment for the **Universal Robots UR5** industrial arm, built with **ROS 2 Humble** and **MoveIt 2**.

Unlike standard configuration packages, this project features a manually implemented **Mock Hardware Interface**, allowing the robot to be simulated and controlled without needing Gazebo or a physical robot. This serves as a lightweight testbed for motion planning algorithms and trajectory execution.

## ✨ Key Features
* **Custom URDF Configuration:** Integrated `mock_components/GenericSystem` for hardware abstraction.
* **MoveIt 2 Setup:** Generated and customized SRDF, kinematics, and controller configurations.
* **Motion Planning:** Configured with OMPL (RRTConnect) for collision-free path planning.
* **Hardware Interface Debugging:** Resolves common `ros2_control` conflicts by overriding default hardware drivers with simulated feedback loops.

## 🛠️ Prerequisites
* **OS:** Ubuntu 22.04 LTS (Jammy Jellyfish)
* **ROS Version:** ROS 2 Humble Hawksbill
* **Dependencies:** MoveIt 2, ros2_control, ros2_controllers

## 🚀 Installation & Build

1.  **Create a workspace:**
    ```bash
    mkdir -p ~/ur5_ws/src
    cd ~/ur5_ws/src
    ```

2.  **Clone the repository:**
    ```bash
    git clone [https://github.com/4brhamy/ros2-ur5-moveit-integration.git](https://github.com/4brhamy/ros2-ur5-moveit-integration.git) .
    ```

3.  **Install dependencies:**
    ```bash
    cd ~/ur5_ws
    rosdep install --from-paths src --ignore-src -r -y
    ```

4.  **Build the workspace:**
    ```bash
    colcon build
    source install/setup.bash
    ```

## 🎮 Usage

Launch the visualization and motion planning interface:
Controls:
The RViz window will open with the UR5 arm loaded.

Use the MotionPlanning plugin to drag the interactive marker (blue ball) to a desired pose.

Click Plan & Execute to visualize the path planning and see the robot move.

📂 Project Structure
moveit_ur5/: Contains the UR5 robot description (URDF/Xacro) and mesh files.

ur_moveit_config/: Contains the semantic robot description (SRDF), launch files, and controller parameters.

🔧 Troubleshooting
If you encounter ros2_control_node crashes, ensure you have the mock components installed:

   sudo apt install ros-humble-ros2-control ros-humble-ros2-controllers



```bash
ros2 launch ur_moveit_config demo.launch.py
