# openpose_ros

Example ROS catkin package that utilizes the OpenPose library from https://github.com/CMU-Perceptual-Computing-Lab/openpose.

## System
Tested on:
* Ubuntu 16.04
* ROS Kinetic
* CUDA 8.0
* cuDNN 6
* OpenCV 3.2.0

## Installation Steps

1. Install openpose (not in catkin_workspace).
   ```bash
   git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose.git
   ```
2. Clone the gflags repository into your catkin_workspace/src directory.
   ```bash
   git clone https://github.com/davetcoleman/gflags.git
   ```
3. Clone this repository into your catkin_workspace/src directory.
   ```bash
   git clone https://github.com/firephinx/openpose_ros.git
   ```
4. Modify the following lines in the CMakeLists.txt to the proper directories of where you installed caffe and openpose:
   ```bash
   set(CAFFE_DIR /path/to/caffe)
   set(OPENPOSE_DIR /path/to/openpose)
   ```
5. Modify the model_folder line in src/gflags_options.cpp to where openpose is installed.
   ```bash
   DEFINE_string(model_folder,             "/path/to/openpose/models/",      "Folder path (absolute or relative) where the models (pose, face, ...) are located.");
   ```
6. Modify the image_topic line in src/gflags_options.cpp to the image_topic you want to process.
   ```bash
   DEFINE_string(camera_topic,             "/camera/image_raw",      "Image topic that OpenPose will process.");
   ```
7. Modify the other parameters in src/gflags_options.cpp to your liking such as enabling face and hands detection.
8. Run catkin_make from your catkin_workspace directory.

### Potential Installation Issues
1. If cv_bridge is causing you errors and/or you decide to use OpenCV 3.2+, copy the cv_bridge folder from https://github.com/ros-perception/vision_opencv into your catkin_workspace/src directory. 
2. If you have problems with CUDA during catkin_make, uncomment this line in CMakeLists.txt # find_package(CUDA REQUIRED)

## Running
```bash
source catkin_workspace/devel/setup.bash
rosrun openpose_ros openpose_ros_node
```


### Using with the ZED camera.

Modify the image_topic line in src/gflags_options.cpp to the image_topic you want to process.
```bash
DEFINE_string(camera_topic,   "/camera/rgb/image_rect_color",   "Image topic that OpenPose will process.");
```
   
   Other options [here](http://wiki.ros.org/zed-ros-wrapper)
