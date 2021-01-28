cmake_minimum_required(VERSION 3.10)
project(watertight LANGUAGES CUDA CXX)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif()

find_package(CUDA REQUIRED)
message(STATUS "Found CUDA ${CUDA_VERSION_STRING} at ${CUDA_TOOLKIT_ROOT_DIR}")

find_package(Eigen3 REQUIRED)
find_package(glm REQUIRED)

set(CMAKE_CUDA_STANDARD 11)
set(CMAKE_CUDA_STANDARD_REQUIRED ON)

enable_language(CUDA)
add_executable(watertight src/main.cpp src/voxelize_project.cpp src/watershed.cu src/sdf.cu)

target_include_directories(watertight PRIVATE src src/base ${CUDA_INCLUDE_DIRS})
target_link_libraries(watertight PRIVATE Eigen3::Eigen glm)

