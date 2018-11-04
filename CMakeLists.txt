cmake_minimum_required(VERSION 3.0)
project(strtk CXX)

add_library(strtk INTERFACE)
target_include_directories(strtk INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>) 
