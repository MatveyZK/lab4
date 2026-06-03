cmake_minimum_required(VERSION 3.11)
project(formatter)

add_library(formatter STATIC formatter.cpp)
target_include_directories(formatter PUBLIC .)
