# ROS Interface for the UWB Tracking Demos of Decawave's DWM1001 and EVK1000 Kits

This repo extends the ROS interfaces for the Ultra-Wideband (UWB) Real Time Locatin System (RTLS) [demo](https://www.decawave.com/wp-content/uploads/2018/08/mdek1001_quick_start_guide.pdf) of Decawave's MDEK1001 Dev-boards provided by [TIERs](https://github.com/TIERS/ros-dwm1001-uwb-localization.git) and [20chix (Mub)](https://github.com/20chix/dwm1001_ros.git) for the purpose of tracking and visualizing multiple tags in ROS environment. Additionally, we also provide the ROS interface for the UWB tracking [demo](https://www.decawave.com/wp-content/uploads/2018/09/trek1000_user_manual.pdf) based on TREK1000/EVK1000 Dev-boards. The code has been tested under Ubuntu 20.04 with ROS Noetic Ninjemys distribution. 

This project has been originated as a supplementary sub-project for [CITrack](https://cit-ec.de/en/ks/projects/citrack) in Cognitronics and Sensor Systems Research Group, [CITEC](https://www.cit-ec.de/en), Bielefeld University.


## Requirements and Setups
### DWM1001/MDEK1001 Setup
- clone this repo into your catkin workspace (see installation section)
- Plug the USB cable of the tag acting as either a listener node or gateway node into your machine
- Check the name of the USB in your machine (typically it is /dev/ttyACM0 in Ubuntu if no other USB is connected into it)
- Give read-write permission to your USB (i.e., sudo chmod 0777 /dev/<your_USB_port> or add it into the user group dialout)
- Make sure that RTLS is working on the app from the grid view according to the instruction in 'Get Started' section 


## Installation

Clone this repo into your catkin workspace and install the dependencies if required 
```
rosdep install --from-paths src --ignore-src -r -y
pip install pyserial
```

Build the workspace:
```
cd ~/<your_catkin_workspace>
catkin_make --build <your_ros_package>
```
Then, run the respetive launch file.
```
roslaunch <your_ros_package>/ <your_launch_file>
```

For instance, run the following launch file for the DWM1001 multiple tags tracking scenario:
```
roslaunch uwb_tracking_ros uwb_tracking_dwm1001.launch
```


## Getting Started
### For DWM1001/MDEK1001 
Follow the steps in [Decawave's DRTLS Guide](https://www.decawave.com/wp-content/uploads/2018/08/mdek1001_quick_start_guide.pdf) to setup a Real Time Location System (RTLS) system with at least 3 anchors and 1 active node using DWM1001-dev board ( in our case, we use MDEK1001 hardware setup). An android phone or a tablet is required to set-up the RTLS using DRTLS andriod app. 

The UWB node can be set-up as an anchor, tag, and listener modes. This repo requires the listener node to be attached into the PC or remote machine where ROS is running. The task of the listener node is echoing the positioning data of tags that it has heard. Only position data (x, y, z) of the tags in 3D are able to process via listener node (i.e., the ranging data are not available). To set-up the node as a listener, simply switch the dedicated UWB node to a 'passive' mode in the Decawave's RTLS app. 

The update rate of the tag's position can be adjusted within the Decawave's app. However, we recommend setting the update rate to 10 Hz in stationary mode.

The following is a sample visualization screenshot of two tags on rviz in 3D
![rviz_uwb_sample](https://user-images.githubusercontent.com/18302290/144410317-1d5b5a1f-3058-487b-b583-408133118df7.JPG)

