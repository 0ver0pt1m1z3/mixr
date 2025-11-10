
cmake_minimum_required(VERSION 3.16)

project(mixr)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(src/base)
add_subdirectory(src/dafif)
add_subdirectory(src/graphics)
add_subdirectory(src/ighost)