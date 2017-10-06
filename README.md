## ROS release package for http://pjreddie.com/darknet/

## Setup

1. Install CUDA from https://developer.nvidia.com/cuda-downloads

  Please ensure cuda is available:

  ```bash
  $ nvidia-smi
  Fri Oct  6 18:55:36 2017
  +-----------------------------------------------------------------------------+
  | NVIDIA-SMI 375.26                 Driver Version: 375.26                    |
  |-------------------------------+----------------------+----------------------+
  | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
  | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
  |===============================+======================+======================|
  |   0  GeForce GTX TIT...  Off  | 0000:02:00.0      On |                  N/A |
  | 22%   34C    P8    19W / 250W |    589MiB / 12203MiB |      9%      Default |
  +-------------------------------+----------------------+----------------------+
  
  +-----------------------------------------------------------------------------+
  | Processes:                                                       GPU Memory |
  |  GPU       PID  Type  Process name                               Usage      |
  |=============================================================================|
  |    0    117042    G   /usr/bin/X                                     369MiB |
  |    0    118023    G   compiz                                         216MiB |
  +-----------------------------------------------------------------------------+
  ```

2. Install ROS from http://wiki.ros.org/indigo/Installation/Ubuntu
3. Install this package

  ```bash
  $ sudo apt-get install ros-indigo-darknet
  ```

## Example

```
roscd darknet
darknet detect cfg/yolo.cfg weights/yolo.weights data/dog.jpg
```

![predictions](https://cloud.githubusercontent.com/assets/493276/22402982/4560e38c-e64d-11e6-9dc6-83ffa679783d.png)
