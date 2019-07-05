---
layout: post
title:  "Jetson Nano Cookbook"
date:   2019-06-06 00:01:00 -0500
categories: [Jetson-Nano]
published: true
---

### Connecting to wifi
1. This comes from instruction on device. Forget location.
```
sudo nmcli device wifi connect CAPRICA24 password 'password goes here'
```

### [Setting up Swap File](https://www.jetsonhacks.com/2019/04/14/jetson-nano-use-more-memory/)
1. Clone JetsonHacks Repor installSwapFile
```
https://github.com/JetsonHacksNano/installSwapfile 
```
1. run with defaults
```
cd installSwapFile
./installSwapFile
```

### Switching Power Modes
1. Switch to low power, can power from micro usb
```
jetson@littlefoot:~$ sudo nvpmodel -m1
```
1. Query power mode
```
jetson@littlefoot:~$ sudo nvpmodel -q 
NV Power Mode: 5W
1
```
1. Switch to high power, use barrel-jack
```
jetson@littlefoot:~$ sudo nvpmodel -m0
```
1. Query power mode
```
jetson@littlefoot:~$ sudo nvpmodel -q
NV Power Mode: MAXN
0
```

### [Two Day Demo](https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo.md)

1. Get cmake for Jetson
```
sudo apt-get install git cmake
```

1. Clone jetson-inference project
```
git clone https://github.com/dusty-nv/jetson-inference
cd jetson-inference
git submodule update --init
```

1. Find the camera connected over USB
```
sudo apt-get install v4l-utils
v4l2-ctl --info --list-devices
```

1. Shows our camera is **video0**
```
HD Webcam C615 (usb-70090000.xusb-2.4):
	/dev/video0
```

1. Find 'camera' files to change the camera to be used (from Raspberry Pi module to USB camera.
```
find jetson-inference/ -name *-camera.cpp
```
* jetson-inference/homography-camera/homography-camera.cpp
* jetson-inference/imagenet-camera/imagenet-camera.cpp
* jetson-inference/detectnet-camera/detectnet-camera.cpp
* jetson-inference/segnet-camera/segnet-camera.cpp
* jetson-inference/utils/camera/gst-camera/gst-camera.cpp

1. For each files above, change the following line to match.
```
#define DEFAULT_CAMERA 0
```

1. Configure the project with cmake.
```
cd jetson-inference
mkdir build
cmake ../
```

1. Compile the project. From build directory.
```
make
sudo make install
```

### [Install Jekyll](https://jekyllrb.com/docs/installation/)
1. Install Pre requisites
```
sudo apt-get install ruby-full build-essential zlib1g-dev
```
1. Revise bashrc
```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```
1. Install Jekyll
```
gem install jekyll bundler
```

### [Install Anaconda](https://devtalk.nvidia.com/default/topic/1051415/jetson-nano/anaconda-for-jetson-nano/)

1. Download Anaconda for ARM
Go to ['Anaconda-ARM'](https://github.com/Archiconda/build-tools/releases/tag/0.2.3).
Click on [Archiconda3-0.2.3-Linux-aarch64.sh](https://github.com/Archiconda/build-tools/releases/download/0.2.3/Archiconda3-0.2.3-Linux-aarch64.sh) to download.

1. Go to downloaded location and run script
```
bash Archiconda3-0.2.3-Linux-aarch64.sh
```
1. Creating default conda environment
```
conda create -n default
```
1. Activating 'default' env
```
conda activate default
```
1. Deactivating 'default' env
```
conda deactivate
```
### Setup SSH

1. Install ssh server
```
sudo apt update
sudo apt install openssh-server
```
1. Start SSH Server
```
sudo systemctl status ssh
```
