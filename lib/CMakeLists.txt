cmake_minimum_required(VERSION 3.12 FATAL_ERROR)
project(prop2json)

# Add our library
add_library(${PROJECT_NAME} SHARED Converter.cpp)

# Add include directories
target_include_directories(${PROJECT_NAME} SYSTEM PUBLIC ${CONAN_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} ${CONAN_LIBS})

# Check whether we need to include coverage support
if (COVERAGE)
    set_target_properties(${PROJECT_NAME} PROPERTIES COMPILE_FLAGS "--coverage")
    set_target_properties(${PROJECT_NAME} PROPERTIES LINK_FLAGS "--coverage")
endif ()
