cmake_minimum_required(VERSION 3.5)

project(efficientnet)

add_definitions(-std=c++11)

option(CUDA_USE_STATIC_CUDA_RUNTIME OFF)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Debug)

cmake_policy(SET CMP0146 OLD)
set(CUDA_TOOLKIT_ROOT_DIR "C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v12.2/lib/x64")
find_package(CUDA REQUIRED)

include_directories(${PROJECT_SOURCE_DIR}/include)
# include and link dirs of cuda and tensorrt, you need adapt them if yours are different
# cuda
include_directories(/usr/local/cuda/include)
link_directories(/usr/local/cuda/lib64)
# tensorrt
include_directories(/usr/include/x86_64-linux-gnu/)
link_directories(/usr/lib/x86_64-linux-gnu/)

add_executable(efficientnet  ${PROJECT_SOURCE_DIR}/efficientnet.cpp)
target_link_libraries(efficientnet nvinfer)
target_link_libraries(efficientnet cudart)

add_definitions(-O2 -pthread)

