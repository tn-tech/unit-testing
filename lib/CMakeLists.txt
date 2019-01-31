cmake_minimum_required(VERSION 3.12 FATAL_ERROR)
project(prop2json)

# Add our library
add_library(${PROJECT_NAME} SHARED Converter.cpp)

# Add include directories
target_include_directories(${PROJECT_NAME} SYSTEM PUBLIC ${CONAN_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} ${CONAN_LIBS})

