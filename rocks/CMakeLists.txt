cmake_minimum_required(VERSION 3.10)
project(rocks VERSION 0.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Options to control building of benchmarks and tests
option(BUILD_BENCHMARKS "Build benchmarks" OFF)
option(BUILD_TESTS "Build tests" OFF)


if(BUILD_BENCHMARKS)
    add_subdirectory(benchmarks)
endif()

if(BUILD_TESTS)
    add_subdirectory(tests)
endif()

# Include the subdirectories
add_subdirectory(src)
