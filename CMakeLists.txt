cmake_minimum_required(VERSION 2.6)
project(jackson)

enable_testing()

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release")
endif()

set(CXX_FLAGS
        -fno-omit-frame-pointer # linux perf
        -Wall
        -Wextra
        -Werror
        -Wconversion
        -Wno-unused-parameter
        -Wold-style-cast
        -Woverloaded-virtual
        -Wpointer-arith
        -Wshadow
        -Wwrite-strings
        -std=c++17
        -march=native
        -rdynamic)
string(REPLACE ";" " " CMAKE_CXX_FLAGS "${CXX_FLAGS}")

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

include_directories(${PROJECT_SOURCE_DIR})

add_subdirectory(jackson)

if(NOT CMAKE_BUILD_NO_EXAMPLES)
    add_subdirectory(example)
endif()
if (CMAKE_BUILD_TESTS)
    add_subdirectory(jackson/test)
endif()
if (CMAKE_BUILD_BENCHMARK)
    add_subdirectory(jackson/bench)
endif()

