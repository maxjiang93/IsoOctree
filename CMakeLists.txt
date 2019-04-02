cmake_minimum_required(VERSION 2.6)
project(IsoOctree)
set(CMAKE_BUILD_TYPE Release)

set(CMAKE_CXX_FLAGS "-Wall -Wextra")
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")

include_directories("${PROJECT_SOURCE_DIR}/SRC")
file(GLOB SOURCES "SRC/*.cpp")
add_executable(IsoOctree ${SOURCES})