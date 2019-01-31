cmake_minimum_required(VERSION 3.12 FATAL_ERROR)
project(unit_testing)

# We want C++17 without extensions
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Add conan support
include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup(KEEP_RPATHS)

# Add our library
add_subdirectory(lib)

# Add our unit tests
add_subdirectory(unittests)

