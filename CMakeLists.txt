cmake_minimum_required(VERSION 3.21)
project(autopilot LANGUAGES C CXX CUDA)

set(CMAKE_CXX_STANDARD 20)

include_directories(include)
include_directories(/usr/local/cuda/include)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CUDA_STANDARD 17)

set(CMAKE_C_FLAGS "-O3 -fopenmp")
set(CMAKE_CXX_FLAGS "-O3 -fopenmp")
set(CMAKE_CUDA_FLAGS "")

find_package(PNG REQUIRED)
include_directories(${PNG_INCLUDE_DIR})

add_executable(autopilot
    ./src/main.cpp
    ./src/stereobm.cpp
    ./src/kernels.cu
)

link_directories(/usr/local/cuda/lib64)
link_libraries(autopilot cudart)

target_link_libraries(autopilot ${PNG_LIBRARY})
