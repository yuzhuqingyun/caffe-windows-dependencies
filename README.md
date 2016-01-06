### Deprecated
Use https://github.com/willyd/caffe-builder instead.

# caffe-windows-dependencies
This project sets up a super build of most of the [Caffe](https://github.com/BVLC/caffe) library dependencies on Windows. The dependencies built by this project are:
* gflags
* glog
* leveldb
* lmdb
* protobuf
* snappy
* opencv
* hdf5

It does not build the following dependencies:
* boost


Windows binaries for these dependencies are widely available. Please note that boost is required to build the windows version of leveldb.

The project is setup via git submodules pointing to either the original code repository on github or a fork of the project so that a CMake-based build is available.

When this project is built it will generate binaries and includes (via CMake install) and a cmake cache file that cane be used so configure the CMake based build of Caffe. Here is what an initial setup would look like
##打开“VS2013 x64 兼容工具命令提示”输入命令
    cmd> md caffe
    cmd> cd caffe
    cmd> git clone https://github.com/willyd/caffe.git caffe
    cmd> git checkout windows
    cmd> git clone --recursive https://github.com/willyd/caffe-windows-dependencies.git caffe-windows-dependencies
    cmd> md build-caffe-windows-dependencies
    cmd> cd build-caffe-windows-dependencies
    cmd> cmake -G "<your generator>" ..\caffe-windows-dependencies
    # configure your environment, set path to boost, set path to opencv, etc...
    cmd> cmake --build . --config Debug
    cmd> cmake --build . --config Release
    cmd> cd ..
    cmd> md build-caffe
    cmd> cd build-caffe
    cmd> cmake  -G "Visual Studio 12 Win64" -C ..\build-caffe-windows-dependencies\install\caffe-cache-init.cmake ..\caffe
    cmd> cmake --build . --config Debug
    cmd> cmake --build . --config Release
    
This was only test with Visual Studio 2013 64 bit build and CMake 3.2.
