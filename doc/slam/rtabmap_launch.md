# Changes to the rtabmap Release File

Due to an update of rtabmap, changes have occurred in the names of some nodes and pkg. 
This change has not yet been implemented in oak-d pro.

To make this change, you need to modify the **rtabmap.launch** file located in 
`~/dai_ws/src/depthai-ros/depthai_ros_driver/launch` 
and replace it with the following:

```
<?xml version="1.0"?>
<launch>
    <arg name="name" default="oak" />
    <arg name="params_file" default="$(find depthai_ros_driver)/config/rgbd.yaml" />



    <include file="$(find depthai_ros_driver)/launch/camera.launch">
        <arg name="name" value="$(arg name)"/>
        <arg name="params_file" value="$(arg params_file)"/>
    </include>
    <node type="rgbd_odometry" name="rgbd_odometry" pkg="rtabmap_odom">
        <remap from="rgb/image" to="$(arg name)/rgb/image_raw"/>
        <remap from="rgb/camera_info" to="$(arg name)/rgb/camera_info"/>
        <remap from="depth/image" to="$(arg name)/stereo/image_raw"/>
        <param name="frame_id" type="string" value="$(arg name)"/>

        <rosparam param="subscribe_depth">True</rosparam>
        <rosparam param="approx_sync">True</rosparam>
        <rosparam param="approx_sync_max_interval">0.01</rosparam>
        
    </node>
    <node type="rtabmap" name="rtabmap" pkg="rtabmap_slam" respawn="true">
        <remap from="rgb/image" to="$(arg name)/rgb/image_raw"/>
        <remap from="rgb/camera_info" to="$(arg name)/rgb/camera_info"/>
        <remap from="depth/image" to="$(arg name)/stereo/image_raw"/>
        <rosparam param="Rtabmap/DetectionRate">3.5</rosparam>
        <param name="frame_id" type="string" value="$(arg name)"/>

    </node>
    <node type="rtabmap_viz" name="rtabmap_viz" pkg="rtabmap_viz">
        <remap from="rgb/image" to="$(arg name)/rgb/image_raw"/>
        <remap from="rgb/camera_info" to="$(arg name)/rgb/camera_info"/>
        <remap from="depth/image" to="$(arg name)/stereo/image_raw"/>
    </node>

</launch>
```
