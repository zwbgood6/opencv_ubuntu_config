# OpenCV Ubuntu Configuration (VS Code)

## step 0: method 1, follow the guidelines in https://learnopencv.com/install-opencv-4-on-ubuntu-18-04/

## step 1: update the ubuntu system package

```
sudo apt-get update && sudo apt-get upgrade
```

## step 2: Install Required tools and packages

if you cannot install some packages below, you may delete them in the command line and install again.

```
sudo apt-get install build-essential cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install python3.5-dev python3-numpy libtbb2 libtbb-dev
sudo apt-get install libjpeg-dev libpng-dev libtiff5-dev libjasper-dev libdc1394-22-dev libeigen3-dev libtheora-dev libvorbis-dev libxvidcore-dev libx264-dev sphinx-common libtbb-dev yasm libfaac-dev libopencore-amrnb-dev libopencore-amrwb-dev libopenexr-dev libgstreamer-plugins-base1.0-dev libavutil-dev libavfilter-dev libavresample-dev
```

## step 3: download opencv sources using git

```
sudo -s
cd /opt
git clone https://github.com/Itseez/opencv.git
git clone https://github.com/Itseez/opencv_contrib.git
```

## step 4: build & install opencv

```
cd opencv
mkdir release
cd release
cmake -D BUILD_TIFF=ON -D WITH_CUDA=OFF -D ENABLE_AVX=OFF -D WITH_OPENGL=OFF -D WITH_OPENCL=OFF -D WITH_IPP=OFF -D WITH_TBB=ON -D BUILD_TBB=ON -D WITH_EIGEN=OFF -D WITH_V4L=OFF -D WITH_VTK=OFF -D BUILD_TESTS=OFF -D BUILD_PERF_TESTS=OFF -D OPENCV_GENERATE_PKGCONFIG=ON -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D OPENCV_EXTRA_MODULES_PATH=/opt/opencv_contrib/modules /opt/opencv/
make -j4
make install
ldconfig
exit
cd ~
```

## step 5: check opencv version installed

```
pkg-config --modversion opencv
```

## step 6: compile and run a test program

```
mkdir opencv_test
cd opencv_test
gedit test.cpp 
```

## step 7: copy and paste the code posted in step 6 

`test.cpp` and `opencv_testimage.png` are in this repo. 

```
g++ test.cpp -o testoutput -std=c++11 `pkg-config --cflags --libs opencv`
./testoutput
```

# trouble shooting

## error 1: cannot find <opencv/opencv.hpp>

If you install opencv on Ubuntu 20.04, go to `/usr/local/lib/pkgconfig/` and you can find `opencv4.pc`. Then you apply

```
sudo cp opencv4.pc opencv.pc
```
