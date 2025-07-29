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

1. Basic configuration.
```
/
├── build
├── src
│   └── main.cpp
└── CMakeLists.txt
```

* `/CMakeLists.txt`
```
cmake_minimum_required(VERSION 4.0)

project(hello-world VERSION 1.0.0)

add_executable(${PROJECT_NAME} src/main.cpp)
```

2. Library configuration.
```
/
├── build
├── src
│   ├── hello.hpp
│   ├── hello.cpp
│   └── main.cpp
└── CMakeLists.txt
```

* `/CMakeLists.txt`
```
cmake_minimum_required(VERSION 4.0)

project(hello-world VERSION 1.0.0)

add_library(print-hello
    STATIC
    src/hello.hpp
    src/hello.cpp
)

add_executable(${PROJECT_NAME} src/main.cpp)

target_link_library(${PROJECT_NAME} PRIVATE print-hello)
```

3. Subdirectory configuration.
```
/
├── build
├── run-hello
│   ├── main.cpp
│   └── CMakeLists.txt
├── print-hello
│   ├── hello.hpp
│   ├── hello.cpp
│   └── CMakeLists.txt
└── CMakeLists.txt
```

* `/CMakeLists.txt`
```
cmake_minimum_required(VERSION 4.0)

project(hello-world VERSION 1.0.0)

add_subdirectory(print-hello)
add_subdirectory(run-hello)
```

* `/run-hello/CMakeLists.txt`
```
add_executable(run-hello main.cpp)

target_link_library(run-hello PRIVATE print-hello)
```
OR
```
get_filename_component(EXE_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)

add_executable(${EXE_NAME} main.cpp)

target_link_library(${EXE_NAME} PRIVATE print-hello)
```

* `/print-hello/CMakeLists.txt`
```
add_library(print-hello
    STATIC
    hello.hpp
    hello.cpp
)

target_include_directories(print-hello PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
```
OR
```
get_filename_component(LIB_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)

add_library(${LIB_NAME}
    STATIC
    hello.hpp
    hello.cpp
)

target_include_directories(${LIB_NAME} PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
```

## Build

Generate project files from `build` directory.
```
cmake ..
```

Generate project files from `CMakeLists.txt` directory.
```
cmake -S . -B build
```

Build from the `build` directory.
```
cmake --build .
```

Build from the `CMakeLists.txt` directory.
```
cmake --build build
```

Build a specific configuration.
```
cmake --build <dir> --config <cfg>
cmake --build <dir> --config Debug
cmake --build <dir> --config Release
```

Build a specific target.
```
cmake --build <dir> --target <tgt>
```
