[//]: # (#install opencv)
## opencv modules
```python
["aruco", "bgsegm", "bioinspired", "calib3d", "ccalib", "core", "cudaarithm", "cudabgsegm", "cudacodec", "cudafeatures2d", "cudafilters", "cudaimgproc", "cudalegacy", "cudaobjdetect", "cudaoptflow", "cudastereo", "cudawarping", "cudev", "cvv", "datasets", "dnn", "dnn_objdetect", "dpm", "face", "features2d", "flann", "freetype", "fuzzy", "gapi", "hfs", "highgui", "img_hash", "imgcodecs", "imgproc", "java_bindings_generator", "line_descriptor", "ml", "objdetect", "optflow", "phase_unwrapping", "photo", "plot", "python_bindings_generator", "reg", "rgbd", "saliency", "shape", "stereo", "stitching", "structured_light", "superres", "surface_matching", "text", "tracking", "ts", "video", "videoio", "videostab", "xfeatures2d", "ximgproc", "xobjdetect", "xphoto"]
```

## Cmake inputs
```
cmake -D CMAKE_BUILD_TYPE=Debug \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
    -D PYTHON3_EXECUTABLE=/usr/local/bin/python3 \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_opencv_python3=ON \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D INSTALL_C_EXAMPLES=OFF \
    -D OPENCV_ENABLE_NONFREE=ON \
    -D WITH_QT=ON \
    -D BUILD_EXAMPLES=OFF \
    -D WITH_CUDA=ON \
    -D BUILD_opencv_cudacodec=OFF \
    -D WITH_OPENCL=ON ..
```

## Trouble shooting
1. WITH_CUDA -- Ubuntu 18.04 [reference](https://nicolas-bettenburg.com/2018-08-18-ubuntu-18-04-deep-learning-box)
- Install Latest Long Lived [NVIDIA drivers](https://www.nvidia.com/object/unix.html)
- sudo sh ${NVIDIA drivers}

- Install [CUDA toolkits](https://developer.nvidia.com/cuda-downloads)
- sudo sh ${CUDA toolkits}
- follow CUDA toolkits instructions after installation complete

2. WITH_QT -- MacOSX
- brew install qt
- export PATH="/usr/local/opt/qt/bin:$PATH"

3. download time out when configuring cmake:
- open CMakeDownloadLog.txt under build directory, search for the failed package, e.g.ippicv_2019_mac_intel64_general_20180723.tgz

