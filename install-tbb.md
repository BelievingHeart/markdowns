[//]: # (#install tbb)

## Linux from source
1. clone the cmake adaptor repo
```
git clone --depth=1 https://github.com/wjakob/tbb.git tbb-cmake 
```
2. add as sub-directory in project in CMakeLists.txt
```cmake
set(TBB_ROOT /home/afterburner/clones/tbb-cmake)
# The following SHARED targets will be defined:
# tbb tbbmalloc tbbmalloc_proxy 
# The following INCLUDE_DIR will be defined:
# TBB_INSTALL_INCLUDE_DIR 
add_subdirectory(${TBB_ROOT} ${TBB_ROOT}/build-release)
```