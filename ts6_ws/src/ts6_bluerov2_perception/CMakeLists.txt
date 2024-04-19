cmake_minimum_required(VERSION 2.8.3)
project(ts6_bluerov2_perception)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  geometry_msgs
  ##message_generation  # Add this line for message generation
)

## Generate messages in the 'msg' folder
##add_message_files(
##  FILES
##)

## Generate added messages and services with any dependencies listed here
##generate_messages(
##  DEPENDENCIES
##  std_msgs
##  geometry_msgs
##)

## Declare a catkin package
catkin_package(
  CATKIN_DEPENDS roscpp std_msgs geometry_msgs message_runtime  # Add 'message_runtime' for message generation
)

## Build talker and listener
include_directories(
  ${catkin_INCLUDE_DIRS}
)

catkin_install_python(PROGRAMS 
  script/imu_analysis.py
  script/pressure_to_depth.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

find_package(gazebo REQUIRED)
include_directories(${GAZEBO_INCLUDE_DIRS})
link_directories(${GAZEBO_LIBRARY_DIRS})

add_library(model_push SHARED library/model_push.cc)
target_link_libraries(model_push ${GAZEBO_LIBRARIES})
