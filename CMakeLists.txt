# moon buggy
cmake_minimum_required(VERSION 3.0)

project(moon-buggy)

find_package(Curses REQUIRED)
set(LIBRARIES ${CURSES_LIBRARIES})
include_directories(${CURSES_INCLUDE_DIRS})

add_subdirectory(src bin)
