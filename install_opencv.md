[//]: # (#install opencv)
## opencv modules
1.
```python
["aruco", "bgsegm", "bioinspired", "calib3d", "ccalib", "core", "cudaarithm", "cudabgsegm", "cudafeatures2d", "cudafilters", "cudaimgproc", "cudalegacy", "cudaobjdetect", "cudaoptflow", "cudastereo", "cudawarping", "cudev", "cvv", "datasets", "dnn", "dnn_objdetect", "dpm", "face", "features2d", "flann", "freetype", "fuzzy", "gapi", "hfs", "highgui", "img_hash", "imgcodecs", "imgproc", "java_bindings_generator", "line_descriptor", "ml", "objdetect", "optflow", "phase_unwrapping", "photo", "plot", "python_bindings_generator", "reg", "rgbd", "saliency", "sfm", "shape", "stereo", "stitching", "structured_light", "superres", "surface_matching", "text", "tracking", "ts", "video", "videoio", "videostab", "xfeatures2d", "ximgproc", "xobjdetect", "xphoto"]
```
2. how to replace `needed_cv_libs.py`: `\b(\w+)\b -> "$1",`

## Cmake inputs
```
cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX=/usr/local -DOPENCV_EXTRA_MODULES_PATH=/home/afterburner/clones/opencv_contrib/modules -DPYTHON3_EXECUTABLE=/usr/local/bin/python3 -DBUILD_opencv_python2=OFF -DBUILD_opencv_python3=ON -DINSTALL_PYTHON_EXAMPLES=OFF -DINSTALL_C_EXAMPLES=OFF -DOPENCV_ENABLE_NONFREE=ON -DWITH_QT=ON -DBUILD_EXAMPLES=OFF -DWITH_CUDA=ON -DBUILD_opencv_cudacodec=OFF -DWITH_OPENCL=ON ..
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

4. [sfm moudule install](https://github.com/opencv/opencv_contrib/tree/master/modules/sfm)
5. viz module: `sudo apt-get install libvtk6-dev`
