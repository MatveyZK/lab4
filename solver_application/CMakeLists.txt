cmake_minimum_required(VERSION 3.11)
project(equation)

add_executable(equation equation.cpp)
target_link_libraries(equation solver formatter_ex)

