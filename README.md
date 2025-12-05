# GLSL 1.50 Material Scripts for RViz2

Material script files that enable GLSL 1.50 geometry shaders in RViz2 for Isaac ROS NVBlox visualization.

## Problem

RViz2 crashes with error:
```
ItemIdentityException: Unable to locate geometry program called rviz/glsl150/box.geom
```

## Solution

These material files work together with the GLSL 1.50 shader files from [GLSL150_shader_for_nvblox](https://github.com/sjhwang1236-beep/GLSL150_shader_for_nvblox).

## Installation

1. First, install the shader files from the companion repository:
```bash
git clone https://github.com/sjhwang1236-beep/GLSL150_shader_for_nvblox.git /tmp/GLSL150_shader_for_nvblox
sudo mkdir -p /opt/ros/humble/share/rviz_rendering/ogre_media/materials/glsl150
sudo cp /tmp/GLSL150_shader_for_nvblox/*.geom /opt/ros/humble/share/rviz_rendering/ogre_media/materials/glsl150/
sudo cp /tmp/GLSL150_shader_for_nvblox/*.vert /opt/ros/humble/share/rviz_rendering/ogre_media/materials/glsl150/
sudo cp /tmp/GLSL150_shader_for_nvblox/*.program /opt/ros/humble/share/rviz_rendering/ogre_media/materials/glsl150/
```

2. Then, install these material scripts:
```bash
git clone https://github.com/sjhwang1236-beep/GLSL_150_scripts.git /tmp/GLSL_150_scripts
sudo mkdir -p /opt/ros/humble/share/rviz_rendering/ogre_media/materials/scripts150
sudo cp /tmp/GLSL_150_scripts/*.material /opt/ros/humble/share/rviz_rendering/ogre_media/materials/scripts150/
```

## Files

- `point_cloud_box.material` - Material using geometry shaders for PointCloud2 box rendering
- `point_cloud_square.material` - Material using geometry shaders for PointCloud2 billboard/square rendering

## Test

```bash
ros2 launch nvblox_examples_bringup isaac_sim_example.launch.py \
    rosbag:=/workspaces/isaac_ros-dev/isaac_ros_assets/isaac_ros_nvblox/quickstart \
    navigation:=False \
    rosbag_args:="--loop"
```

RViz2 should now run without geometry shader errors.
