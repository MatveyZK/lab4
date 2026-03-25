cmake_minimum_required(VERSION 3.11)
project(formatter_ex)

add_library(formatter STATIC ../formatter_lib/formatter.cpp)
target_include_directories(formatter PUBLIC ../formatter_lib)
add_library(formatter_ex STATIC formatter_ex.cpp)
target_link_libraries(formatter_ex PUBLIC formatter)
