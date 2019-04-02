cmake_minimum_required(VERSION 3.2)
project(IsoOctree)
set(CMAKE_BUILD_TYPE Release)

set(CMAKE_CXX_FLAGS "-Wall -Wextra")
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")
set(CMAKE_CXX_STANDARD 14)

# include OpenMP for OSX
if(APPLE)
	include_directories("/usr/local/lib/")
endif()

include_directories("${PROJECT_SOURCE_DIR}/SRC")
file(GLOB SOURCES "SRC/*.cpp")
add_executable(IsoOctree ${SOURCES})
