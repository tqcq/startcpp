cmake_minimum_required(VERSION 3.18)
project(startcpp LANGUAGES C CXX VERSION 0.1.0)

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/third_party/rxcpp/Rx/v2/src")

add_executable(startcpp "")
target_sources(startcpp
    PRIVATE
        src/main.cpp
)