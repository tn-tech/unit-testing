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
add_library(prop2json SHARED lib/Converter.cpp)
target_include_directories(prop2json SYSTEM PUBLIC ${CONAN_INCLUDE_DIRS})
target_link_libraries(prop2json ${CONAN_LIBS})

# Add our unit tests
add_executable(unittests unittests/main.cpp unittests/ConverterTests.cpp)
target_include_directories(unittests PUBLIC ${CMAKE_SOURCE_DIR}/lib)
target_include_directories(unittests SYSTEM PUBLIC ${CONAN_INCLUDE_DIRS})
target_link_directories(unittests PUBLIC ${CMAKE_BINARY_DIR}/lib)
target_link_libraries(unittests ${CONAN_LIBS})
target_link_libraries(unittests prop2json)

# Add our custom test target that will execute unit tests
add_custom_target(test COMMAND
        ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${PROJECT_NAME} --gtest_output=xml:${CMAKE_BINARY_DIR}/test_results.xml
        DEPENDS ${PROJECT_NAME})