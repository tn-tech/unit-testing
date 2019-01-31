cmake_minimum_required(VERSION 3.12 FATAL_ERROR)
project(unittests)

# Add our unit tests
add_executable(${PROJECT_NAME} main.cpp ConverterTests.cpp)
target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_SOURCE_DIR}/lib)
target_include_directories(${PROJECT_NAME} SYSTEM PUBLIC ${CONAN_INCLUDE_DIRS})
target_link_directories(${PROJECT_NAME} PUBLIC ${CMAKE_BINARY_DIR}/lib)
target_link_libraries(${PROJECT_NAME} ${CONAN_LIBS})
target_link_libraries(${PROJECT_NAME} prop2json)

# Add our custom test target that will execute unit tests
add_custom_target(test COMMAND
        ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/${PROJECT_NAME} --gtest_output=xml:${CMAKE_BINARY_DIR}/test_results.xml
        DEPENDS ${PROJECT_NAME})