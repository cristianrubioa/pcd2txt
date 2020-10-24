#//////////////////////////////////////////////////////////////////////#
#                       CMAKE CONFIGURATION                            #
#//////////////////////////////////////////////////////////////////////#

# CMake version check
cmake_minimum_required(VERSION 3.5.1)

# create project "pcd2txt"
project(pcd2txt VERSION 1.0.0)

# set build type = Debug mode
set(CMAKE_BUILD_TYPE Release)

message("\n" "====================================")
message("Project: ${PROJECT_NAME} ")
message("====================================")

# set the include directive in the same project folder
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# set corresponding package directories
set(PCL_DIR /opt/pcl-1.8.1/build)

# include dependencies of pcl 1.8.1 in the project directory
set(CMAKE_MODULE_PATH ${PCL_DIR}/../cmake/Modules)

# set cmake for use std c++11 and output executable folder to bin
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

# packages 
message("Finding PCL package...")
message("=====================")
message("PCL PACKAGE")
message("=====================")

find_package(PCL 1.9 PATHS ${PCL_DIR} QUIET)
if(PCL_FOUND)
    message(STATUS "PCL status:")
    message(STATUS "    version: ${PCL_VERSION}")
    message(STATUS "    directorie: ${PCL_DIR}")
else()
    message(WARNING "   PCL 1.9 not found, attempting 1.8...")
    find_package(PCL 1.8 QUIET)
    if(PCL_FOUND)
        message(STATUS "PCL status:")
        message(STATUS "    version: ${PCL_VERSION}")
        message(STATUS "    directorie: ${PCL_DIR}")
    else()
    	message(FATAL_ERROR "    ERROR: PCL minimum required version 1.8. Not found")    
    endif()
endif()

# headers
include_directories(${PCL_INCLUDE_DIRS})
include(CheckFunctionExists)
add_definitions(${PCL_DEFINITIONS})

# libraries path
link_directories(${PCL_LIBRARY_DIRS})

# source code
set(MAIN_SOURCE "pcd2txt.cpp")

# executables 
add_executable(${PROJECT_NAME} ${MAIN_SOURCE})

# target libraries
target_link_libraries(${PROJECT_NAME} ${PCL_LIBRARIES})

message("============================================")
message("Project: ${PROJECT_NAME} COMPILED WITH CMAKE " ${CMAKE_VERSION})
message("============================================")