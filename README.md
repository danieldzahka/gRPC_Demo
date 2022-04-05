# gRPC Demo for CS6210 Project 4

The globally installed version of cmake on advos is too old for this to work, so if you want to do this on advos, [install cmake locally](#install-cmake-locally-without-sudo), then skip to [Building the Demo](#building-the-demo). If you are running on your own machine, make sure all of the dependencies are installed. After the project 3 deadline, we plan to upgrade the cmake on advos to eliminate the first step.

## Dependencies
### Install cmake locally without sudo
Install cmake locally (you can do this on advos without sudo):
```shell
wget https://github.com/Kitware/CMake/releases/download/v3.23.0/cmake-3.23.0-linux-x86_64.sh
mkdir -p $HOME/localcmake 
sh cmake-3.23.0-linux-x86_64.sh --prefix=$HOME/localcmake --skip-license 
export PATH=$HOME/localcmake/bin:$PATH #You need to do this every time you login, otherwise put in $HOME/.profile 
which cmake # /home/<gtid>/localcmake/bin/cmake
cmake --version # cmake version 3.23.0
```

### Installing Dependencies with sudo

Install cmake with sudo:
```shell
sudo apt-get install cmake
cmake --version # output should be >= 3.15
```

Dependencies to build gRPC:
```shell
sudo apt-get install build-essential autoconf libtool pkg-config
```

ninja-build is an optional dependency that can speed up the gRPC build.
```shell
sudo apt-get install ninja-build # optional dependency
ninja --version #Check install
```

## Building the Demo
```shell
git clone https://github.com/danieldzahka/gRPC_Demo.git
cd gRPC_Demo
cmake -S . -B ./build #-G Ninja (optional: add this if you installed ninja-build)
cmake --build ./build --target client server
```

## Running Server & Client
If you are on advos, make sure you are [using unique port](#a-note-about-ports)

In one terminal:
```shell
cd build
./src/server
```

In a different terminal:
```shell
cd build
./src/client
```

## A Note about ports
If you are running on a shared machine (like advos) you will need to run your server/client on a port that doesn't conflict with other students on the same machine.
