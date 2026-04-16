cmake_minimum_required(VERSION 3.10)
project(tests)

add_executable(tests ${CMAKE_CURRENT_SOURCE_DIR}/test.cpp)

target_link_directories(tests gtest gtest-main banking)

