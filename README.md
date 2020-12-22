# ASL
These files were tested on Jackal1

## GMapping
**GMapping with ZED only:** `lidar_gmapping_noodom.launch`

Required packages: 
- laser_scan_matcher
- slam_gmapping
                   
**GMapping with ZED only and path:** `lidar_gmapping_noodom.launch`

Required packages: 
- pointcloud_to_laserscan (not necessary, can be commented out)
- laser_scan_matcher
- slam_gmapping
- hectory_trajectory_server
- hector_geotiff

Copy the `robot_localization.yaml` file from the params folder and place it in the `/opt/ros/kinetic/share/robot_localization/params` folder. This file contains the covariance matrix values for optimal mapping.

**GMapping with ZED and odometry and path:** `lidar_gmapping_covB.launch`

Required packages: 
- pointcloud_to_laserscan (not necessary, can be commented out)
- robot_localization
- slam_gmapping
- hector_trajectory_server
- hector_geotiff

#### Offline Mapping
To perform offline mapping, a series of topics must be recorded.

First, the LIDAR must be enabled with VLP16-points.launch from the velodyne package.
Then, gmapping and RViz must be launched.

From here, record the following topics using `rosbag record`:
- /initialpose
- /scan
- /jackal_velocity_controller/odom
- /tf
- /tf_static
Once offline, launch roscore, gmapping, and RViz. Then enter `rosbag play` and playback the recorded rosbag from earlier.

If time errors occur, do the following.

Before launching anything, enter 
```sh
set rosparam use_sim_time true
```
When playing back data, enter `rosbag play --clock`

## RTAB-Map
**RTAB-Map with ZED only:** `zed_rtabmap_stereob.launch`
