# CMake

<p align="center"><img align="center" width="30%" height="30%" src="assets/cmake.svg"></p>

[CMake](https://cmake.org/) is an open source, cross-platform family of tools designed to build, test, and package software. It gives you control of the software compilation process using simple independent configuration files. Unlike many cross-platform systems, it is designed to be used in conjunction with the native build environment.

## Index

* [Project Structure](#project-structure)
* [Configuration](#configuration)
  * [CMakeLists.txt](#cmakeliststxt)
* [Build](#build)

## Project Structure

```
/
├── build
│   └── <platform:linux,macos,windows,etc.>
│       └── <architecture:x86,x86_64,amd64,arm64,aarch64,riscv32,riscv64,etc.>
│           └── <configuration:debug,release,distribution,etc.>
│               ├── bin
│               └── lib
├── external
├── tests
├── src
│   └── main.cpp
└── CMakeLists.txt
```

## Configuration

### CMakeLists.txt

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

4. Cross-platform configuration.
```
/
├── build
│   └── <platform>
│       └── <architecture>
│           └── <configuration>
│               ├── bin
│               └── lib
├── src
│   └── main.cpp
└── CMakeLists.txt
```

* `/CMakeLists.txt`
```
cmake_minimum_required(VERSION 4.0)

project(hello-world VERSION 1.0.0)

# Platform
if(UNIX)
    set(PLATFORM "linux")
elseif(APPLE)
    set(PLATFORM "macos")
elseif(WIN32)
    set(PLATFORM "windows")
else()
    message(FATAL_ERROR "Unknown platform")
endif()
message(STATUS "Platform: ${PLATFORM}")

# Architecture
string(TOLOWER "${CMAKE_SYSTEM_PROCESSOR}" ARCHITECTURE_LOWER)
if(ARCHITECTURE_LOWER MATCHES "^(x86_64|amd64)$")
    set(ARCHITECTURE "x86_64")
elseif(ARCHITECTURE_LOWER MATCHES "^(arm64|aarch64)$")
    set(ARCHITECTURE "arm64")
else()
    set(ARCHITECTURE "${CMAKE_SYSTEM_PROCESSOR}")
endif()
message(STATUS "Architecture: ${ARCHITECTURE}")

# Configuration
if(CMAKE_CONFIGURATION_TYPES)  # Multi-config (Visual Studio/Xcode)
    message(WARNING "Using multiple configuration")
    set(CONFIGURATION $<CONFIG>)
else()  # Single-config (Makefile/Ninja)
    message(WARNING "Using single configuration")
    string(TOLOWER "${CMAKE_BUILD_TYPE}" CONFIGURATION)
endif()
message(STATUS "Configuration: ${CONFIGURATION}")

# Construct the output directory path
set(OUTPUT_DIR "${CMAKE_SOURCE_DIR}/build/${PLATFORM}/${ARCHITECTURE}/${CONFIGURATION}")

# Apply to runtime, library, and archive outputs
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${OUTPUT_DIR}/lib)

# Multi-config output mapping
if(CMAKE_CONFIGURATION_TYPES)
    foreach(CONFIG ${CMAKE_CONFIGURATION_TYPES})
        string(TOUPPER "${CONFIG}" CONFIG_UPPER)
        string(TOLOWER "${CONFIG}" CONFIG_LOWER)
        set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/build/${PLATFORM}/${ARCHITECTURE}/${CONFIG_LOWER}/bin)
        set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/build/${PLATFORM}/${ARCHITECTURE}/${CONFIG_LOWER}/lib)
        set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${CONFIG_UPPER} ${CMAKE_SOURCE_DIR}/build/${PLATFORM}/${ARCHITECTURE}/${CONFIG_LOWER}/lib)
    endforeach()
endif()

add_executable(${PROJECT_NAME} src/main.cpp)
```

## Build

Generate build files from `build` directory.
```
cmake ..
```

Generate build files from `CMakeLists.txt` directory.
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
