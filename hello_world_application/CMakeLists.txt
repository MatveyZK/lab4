cmake_minimum_required(VERSION 3.11)
project(hello_world)

add_library(formatter STATIC ../formatter_lib/formatter.cpp)
target_include_directories(formatter PUBLIC ../formatter_lib)
add_library(formatter_ex STATIC ../formatter_ex_lib/formatter_ex.cpp)
target_include_directories(formatter_ex PUBLIC ../formatter_ex_lib)
target_link_libraries(formatter_ex formatter)
add_executable(hello_world hello_world.cpp)
target_include_directories(hello_world PUBLIC ../formatter_ex_lib)
target_link_libraries(hello_world formatter_ex)

