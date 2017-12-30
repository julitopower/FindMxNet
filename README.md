# FindMxNet

CMake module to find MxNet

# Notes

To develop C/C++ code with MxNet, its source code must be checked out and compiled locally. This module works best if an environment varialbe called __MXNET_ROOT__ is defined, and points to the root of MxNet source code.

# Building MxNet

To build MxNet from source, refer to http://mxnet.incubator.apache.org/install/index.html and select _Build from source_. The following steps generally work:

```bash
$ sudo apt-get update
$ sudo apt-get install -y build-essential git
$ sudo apt-get install -y libopenblas-dev liblapack-dev
$ sudo apt-get install -y libopencv-develop

$ git clone --recursive https://github.com/apache/incubator-mxnet
# export MXNET_ROOT=$(readlink -f ./inclubator-mxnet)

$ cd incubator-mxnet
$ make -j $(nproc) USE_OPENCV=1 USE_BLAS=openblas USE_CPP_PACKAGE=1
```

After taking this steps the FindMxNet module will work as expected.

# Integration in your project

## As git submodule

This is the recommended way. In the root of your project, execute the following commands

```bash
git submodule add https://github.com/julitopower/FindMxNet cmake/Modules
git submodule update --init --recursive
```

## Adding the module to your project

In the root of your project, execute the following commands:

```bash
mkdir -p cmake/Modules
git clone https://github.com/julitopower/FindMxNet /tmp/FindMxNet
cp /tmp/FindMxNet/FindMxNet.cmake cmake/Modules
rm -rf /tmp/FindMxNet
```

# Usage

Now add the following lines to your CMakeLists.txt root file, just below the project statement:

```cmake
set (CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake/Modules/)
find_package(MxNet REQUIRED)
include_directories(${MxNet_INCLUDE_DIRS})
```

To link a target against MxNet shared library, simply add the following to your CMake configuration:

```cmake
target_link_libraries(target_name ${MxNet_LIB})
```