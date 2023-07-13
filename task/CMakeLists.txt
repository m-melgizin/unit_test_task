cmake_minimum_required(VERSION 3.26)

project(task_lib)

set(LIB_SOURCES task.cpp)

add_library(task STATIC ${LIB_SOURCES})