# gRPC Demo for CS6210 Project 4

If you are running on advos, you can skip to [Building the Demo](#building-the-demo). Otherwise, you may need to install these dependencies:

## Dependencies

Install cmake:
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