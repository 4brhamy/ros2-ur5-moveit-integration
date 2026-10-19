# UR5 Motion Planning with ROS 2 Humble and MoveIt 2

A lightweight simulation environment for the **Universal Robots UR5** industrial arm. It plans and executes
collision-free motions in RViz with **MoveIt 2**, using **ros2_control mock hardware**, so it needs no Gazebo
and no physical robot.

<img width="1375" alt="UR5 planning a motion in RViz with MoveIt 2" src="https://github.com/user-attachments/assets/62c99d1d-27d7-4576-b1e2-8d21231c64d9" />

## Features

- **Custom robot description.** A UR5 xacro built on the official `ur_macro.xacro`, set up for the UR5's own
  joint limits, kinematics and physical parameters.
- **Mock hardware.** `mock_components/GenericSystem` stands in for the robot driver. Commanded joint positions are
  echoed back as state, so trajectories execute instantly in simulation.
- **MoveIt 2 configuration.** SRDF, kinematics, joint limits, controllers and Pilz Cartesian limits, generated with
  the MoveIt Setup Assistant and then customised.
- **Motion planning.** OMPL planning pipeline (RRTConnect by default) for collision-free paths, executed through
  `ros2_control` joint trajectory controllers.
- **Driver conflicts resolved.** The default UR hardware interface is replaced with the mock system, which fixes the
  `ros2_control_node` crashes you get when launching the stock description without a real robot.

## Packages

| Package | Contents |
|---|---|
| `moveit_ur5` | UR5 description (xacro), meshes for the robot cell, and an RViz launch with joint sliders |
| `ur_moveit_config` | MoveIt 2 configuration: SRDF, controllers, kinematics, limits and launch files |

## Prerequisites

- Ubuntu 22.04 with **ROS 2 Humble**
- MoveIt 2, ros2_control, ros2_controllers, and the UR description package:

```bash
sudo apt install ros-humble-moveit ros-humble-ros2-control ros-humble-ros2-controllers ros-humble-ur-description
```

## Build

```bash
mkdir -p ~/ur5_ws/src && cd ~/ur5_ws/src
git clone https://github.com/4brhamy/ros2-ur5-moveit-integration.git .
cd ~/ur5_ws
rosdep install --from-paths src --ignore-src -r -y
colcon build
source install/setup.bash
```

## Run

**Plan and execute motions with MoveIt:**

```bash
ros2 launch ur_moveit_config demo.launch.py
```

In RViz, drag the interactive marker at the end effector to a target pose, then click **Plan & Execute** in the
MotionPlanning panel. MoveIt plans a collision-free path and the arm follows it.

**View the robot model with joint sliders (no MoveIt):**

```bash
ros2 launch moveit_ur5 rviz.launch.py
```

## Troubleshooting

If `ros2_control_node` crashes on startup, make sure the mock components are installed:

```bash
sudo apt install ros-humble-ros2-control ros-humble-ros2-controllers
```

**Stack:** ROS 2 Humble · MoveIt 2 · OMPL · ros2_control · RViz 2 · xacro

---
Abrham Yilma
