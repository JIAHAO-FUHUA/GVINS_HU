cmake_minimum_required(VERSION 2.8.3)
project(gvins_feature_tracker)

set(CMAKE_BUILD_TYPE "Release")
set(CMAKE_CXX_FLAGS "-std=c++14")
set(CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -g")

find_package(catkin REQUIRED COMPONENTS
    roscpp
    std_msgs
    sensor_msgs
    cv_bridge
    gvins_camera_model
    )

find_package(OpenCV 4 REQUIRED)

catkin_package()

include_directories(
    ${catkin_INCLUDE_DIRS}
    )

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)
find_package(Eigen3)
include_directories(
  ${catkin_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIR}
)

add_executable(gvins_feature_tracker
    src/feature_tracker_node.cpp
    src/parameters.cpp
    src/feature_tracker.cpp
    )

target_link_libraries(gvins_feature_tracker ${catkin_LIBRARIES} ${OpenCV_LIBS})
