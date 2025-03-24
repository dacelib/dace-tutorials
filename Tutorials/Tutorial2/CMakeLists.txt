# DACE Examples
#
# This file shows how to use the DACE in a cmake project
# Simply import the DACE cmake package. It automatically provides the correct
# locations for headers and libraries.
# If the DACE is installed in a non-default location, tell cmake where to look:
#   set(dace_DIR "/my/custom/root/usr/local/lib/cmake/dace")
# It exposes two targets:
#   dace::dace   (the dynamic DACE library)
#   dace::dace_s (the static DACE library)
# Make sure to link your executable with one of those and include the correct
# header (<dace/dace.h> or <dace/dace_s.h>) in the code.
#
# On Windows only, the dace.dll dynamics library is typically expected to be
# located in the same directory as the executable using it. You can use a
# command such as the file(COPY ...) below to automatically copy the dace.dll
# from the DACE package next to your executables.
#
# Alternatively, you can use the FetchContent mechanism to automatically clone
# the DACE repository, and have it added to your builds. For forward compatibility,
# you should still use the dace::dace and dace::dace_s libraries described above.
#

cmake_minimum_required (VERSION 3.10)

project(Examples2 CXX)

# Use this mechanism to find DACE library installed separately in your sytem (and copy to binary dir on Windows)

find_package(dace 2.0.0 REQUIRED)
if(WIN32)
    get_target_property(DACEDLL dace::dace LOCATION)
    file(COPY "${DACEDLL}" DESTINATION "${CMAKE_CURRENT_BINARY_DIR}")
endif(WIN32)

# Use this mechanism to automatically download and build DACE

#include(FetchContent)
#FetchContent_Declare(
#  DACE
#  GIT_REPOSITORY https://github.com/dacelib/dace.git
#)
#FetchContent_MakeAvailable(DACE)
#add_library(dace::dace ALIAS dace)
#add_library(dace::dace_s ALIAS dace_s)


add_executable(1Basics-Ex 1Basics-Ex.cpp)
target_link_libraries(1Basics-Ex PUBLIC dace::dace)

add_executable(2IntDiff-Ex 2IntDiff-Ex.cpp)
target_link_libraries(2IntDiff-Ex PUBLIC dace::dace)

add_executable(3Evaluation-Ex 3Evaluation-Ex.cpp)
target_link_libraries(3Evaluation-Ex PUBLIC dace::dace)

add_executable(4Solver-Ex 4Solver-Ex.cpp)
target_link_libraries(4Solver-Ex PUBLIC dace::dace)

add_executable(5Vectors-Ex 5Vectors-Ex.cpp)
target_link_libraries(5Vectors-Ex PUBLIC dace::dace)

add_executable(6Integrator-Ex 6Integrator-Ex.cpp)
target_link_libraries(6Integrator-Ex PUBLIC dace::dace)

add_executable(7PID-Ex 7PID-Ex.cpp)
target_link_libraries(7PID-Ex PUBLIC dace::dace)
