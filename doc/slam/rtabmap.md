# RTAB-Map

GitHub: https://github.com/introlab/rtabmap.

ROS Package: https://wiki.ros.org/rtabmap.

## ROS

### Installation

Source: https://github.com/introlab/rtabmap/wiki/Installation

```sh
# Update OS
sudo apt update
sudo apt dist-upgrade

#  Install ROS package
sudo apt install ros-noetic-rtabmap-ros ros-noetic-robot-localization ros-noetic-imu-filter-madgwick ros-noetic-octomap-rviz-plugins
```

## SLAM

Source: https://github.com/luxonis/depthai-ros#readme

### Launch

```sh
roslaunch depthai_ros_driver rtabmap.launch
```

**Note:** in order to delete past sessions data, execute the following command:

```sh
cd ~/.ros/
rm -rf rtabmap.db
```
