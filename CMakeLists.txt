cmake_minimum_required(VERSION 3.15)
project(test_repos)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find GoogleTest
find_package(GTest REQUIRED)

# Enable precompiled headers
add_library(pch_header OBJECT pch.cpp pch.h)
target_precompile_headers(pch_header PRIVATE pch.h)

# Add executable
add_executable(test_repos
    test.cpp
    pch.cpp
    pch.h
    sort.h
    stringProcessor.h
    $<TARGET_OBJECTS:pch_header>
)

# Link GoogleTest and its main function
target_link_libraries(test_repos PRIVATE 
    GTest::GTest 
    GTest::Main
)

# Include directories
target_include_directories(test_repos PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${GTEST_INCLUDE_DIRS}
)

# Linux-specific settings
if(UNIX)
    target_compile_options(test_repos PRIVATE -pthread)
    target_link_options(test_repos PRIVATE -pthread)
endif()
