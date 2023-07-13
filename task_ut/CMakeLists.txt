cmake_minimum_required(VERSION 3.26)

project(task_ut)

include_directories(../task)

set(UT_SOURCES ut.cpp)

add_executable(task_ut ${UT_SOURCES})

target_link_libraries(task_ut task)