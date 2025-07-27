# CMake

<p align="center"><img align="center" width="30%" height="30%" src="assets/cmake.svg"></p>

[CMake](https://cmake.org/) is an open source, cross-platform family of tools designed to build, test, and package software. It gives you control of the software compilation process using simple independent configuration files. Unlike many cross-platform systems, it is designed to be used in conjunction with the native build environment.

## Index

* [Project Structure](#project-structure)
* [Configuration](#configuration)
* [Build](#build)

## Project Structure

```
/
├── build
├── external
├── src
│   └── main.cpp
└── CMakeLists.txt
```

## Configuration

`CMakeLists.txt` is a build configuration file that contains commands to describe how the project should be built.

Basic file.
```
cmake_minimum_required(VERSION 4.0)

project(my-project VERSION 1.0.0)

add_executable(${PROJECT_NAME} src/main.cpp)
```

## Build

Generate project files.
```
cd build
cmake ..
```

Build.
```
cd build
cmake --build .
```
