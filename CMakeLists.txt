cmake_minimum_required(VERSION 3.1)
project(cluster)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(SOURCE_FILES mpich-multi.c.cpp)
add_executable(cluster ${SOURCE_FILES})