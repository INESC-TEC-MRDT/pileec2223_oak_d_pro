# OAK-D Pro

Model:
https://docs.luxonis.com/projects/hardware/en/latest/pages/DM9098pro.html.

ROS: https://github.com/luxonis/depthai-ros/tree/noetic.

## ROS

### Configuration

1. Install dependencies
   ```sh
   sudo apt install libopencv-dev
   sudo wget -qO- https://raw.githubusercontent.com/luxonis/depthai-ros/main/install_dependencies.sh | sudo bash
   ```
2. Setting up Depth AI ROS workspace
   ```sh
   mkdir -p dai_ws/src
   cd dai_ws/src
   git clone https://github.com/luxonis/depthai-ros.git
   cd depthai-ros
   git checkout noetic
   cd ../..
   rosdep install --from-paths src --ignore-src -r -y
   sudo apt update
   sudo apt dist-upgrade
   source /opt/ros/noetic/setup.bash
   catkin_make_isolated -l1 -j1
   source devel_isolated/setup.bash
   ```

**Note:** do not put `source ~/dai_ws/devel_isolated/setup.bash` in the
`~/.bashrc` file. This avoids to have conflicts with your own catkin workspace
when you are not using Depth AI ROS drivers.
However, note that you must source always when using those drivers!

**Test:** Asus ROG G501VW (personal PC of Ricardo Sousa).

- Intel Core i7 6th Gen 6700HQ Quad-Core 2.60 GHz (up to 3.50 GHz)
- RAM 8G DDR4
- Nvidia GeForce GTX 960M 4GB DDR5
- 3 x USB 3.0, 1 x USB 3.1 Gen 2 (Type C)

### Examples

Source: https://github.com/luxonis/depthai-ros#executing-an-example.

**stereo_inertial_node**

```sh
roslaunch depthai_examples stereo_inertial_node.launch
```

If appears an error relative to the rviz plugin for the Inertial Measurement
Unit (IMU), execute the following commands:

```sh
sudo apt update
sudo apt install ros-noetic-rviz-imu-plugin
```
