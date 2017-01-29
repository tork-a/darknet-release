## ROS release package for http://pjreddie.com/darknet/

## Setup
Install CUDA from https://developer.nvidia.com/cuda-downloads

## Example
```
roscd darknet
darknet detect cfg/yolo.cfg weights/yolo.weights data/dog.jpg
```

![predictions](https://cloud.githubusercontent.com/assets/493276/22402982/4560e38c-e64d-11e6-9dc6-83ffa679783d.png)
