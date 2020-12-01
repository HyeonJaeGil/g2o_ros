cmake_minimum_required(VERSION 3.0.2)
project(g2o_ros)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/thirdparty/g2o/cmake_modules)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
)


find_package(SuiteSparse)
include_directories(${SUITESPARSE_INCLUDE_DIRS})
find_package(Boost REQUIRED COMPONENTS system)
find_package(Eigen3 REQUIRED)
find_package(g2o REQUIRED)

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if your package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES g2o_ros
#  CATKIN_DEPENDS roscpp rospy
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
  ${EIGEN3_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
  ${CSPARSE_INCLUDE_DIRS}
  # ${G2O_INCLUDE_DIRS}
  )

set(G2O_LIBS
	g2o_core 
	g2o_types_sba 
	g2o_types_slam3d
	g2o_solver_csparse 
	g2o_stuff 
	g2o_csparse_extension
	)

add_executable(g2o_example src/g2o_example.cpp)

target_link_libraries(g2o_example
  ${catkin_LIBRARIES}
  ${EIGEN3_LIBS}
  ${G2O_LIBS}
  )

