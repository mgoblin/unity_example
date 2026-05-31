# Minimum required version of CMake
cmake_minimum_required(VERSION 3.10)

# Project name
project(unity_example)

# Set C++ standard (e.g., C++17)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Specify GCC as the compiler
set(CMAKE_C_COMPILER gcc)
set(CMAKE_CXX_COMPILER g++)

# Add executable from source files
# Assuming main source file is main.cpp (adjust if needed)
add_executable(${PROJECT_NAME} src/main.c)

# Compiler options for GCC
target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -O2)

# Enable testing
enable_testing()

add_library(unity STATIC libs/unity/unity.c)

target_include_directories(unity PUBLIC libs/unity)

# Add test executable
add_executable(test_${PROJECT_NAME} 
    # src/main.c
    tests/test_main.c
)

# Link Unity testing framework
target_link_libraries(test_${PROJECT_NAME} unity)

# Add test
add_test(NAME test_${PROJECT_NAME} COMMAND test_${PROJECT_NAME})
