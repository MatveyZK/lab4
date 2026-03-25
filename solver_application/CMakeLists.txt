cmake_minimum_required(VERSION 3.11)
project(solver)

add_library(formatter STATIC ../formatter_lib/formatter.cpp)
target_include_directories(formatter PUBLIC ../formatter_lib)
add_library(formatter_ex STATIC ../formatter_ex_lib/formatter_ex.cpp)
target_include_directories(formatter_ex PUBLIC ../formatter_ex_lib)
target_link_libraries(formatter_ex formatter)
add_library(solver STATIC ../solver_lib/solver.cpp)
target_include_directories(solver PUBLIC ../solver_lib)
add_executable(equation equation.cpp)
target_include_directories(equation PUBLIC ../solver_lib)
target_link_libraries(equation solver formatter_ex)

