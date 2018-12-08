apriltags_ros
===
apriltags ros package for tag detection based on https://github.com/swatbotics/apriltags-cpp

ubuntu16.04 ROS kinetic 

Installation
===

PreInstall

**for ubuntu16.04**
sudo apt-get --yes install libcgal-qt5-dev libcgal-dev  # for pr apriltags

**for ubuntu14.04**
sudo apt-get --yes install libcgal-dev  # for pr apriltags


**1.apriltags-cpp** 
Building
========

git clone 


To compile the code, 
```
    cd apriltags_ros/software/apriltags-cpp
    mkdir build
    cd build
    cmake .. -DCMAKE_BUILD_TYPE=Release
    make
    sudo make install
```
How to Fly
========

**2.apriltags ROS packages**
```
    cd ~/apriltags_ros/apriltags_ws
    source environment.sh
    catkin_make 
    source environment.sh
```

Usage
========
Print out tag36h11.pdf  in apriltags_ros/software/  with your desire size.

edit tag deteails in the launch file

For example The tag ID 1 inner width is 82mm  set 0.082m
```
   <rosparam param="tag_data">
      "1": 
        size: 0.082
        name:tag1
      "2":
        size: 0.048
        name:tag2
    </rosparam>
 ```

also remap right  topic for your camera device
the default using usb_cam.
ex:
    <remap from="~image" to="/usb_cam/image_raw"/>
    <remap from="~camera_info" to="/usb_cam/camera_info"/>

Open 4 terminal shows like this, you can utilize byobu tool.

**Terminal1:**
`roslaunch usb_cam usb_cam-test.launch`

**Terminal2:**
`roslaunch apriltags usb_cam_apriltags.launch`

**Terminal3:**
`rostopic echo /apriltags/detections`

**Terminal4:**
`rosrun image_view image_view image:=/usb_cam/image_raw`
