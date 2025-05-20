cmake_minimum_required(VERSION 3.15)
project(test_repos)

# Set C++ standard (adjust version if needed)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

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

# Include current directories
target_include_directories(test_repos PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}
)

# Uncomment if you need Windows API features
# target_link_libraries(test_repos PRIVATE WindowsAPILibrary)

# Handle NuGet packages (you'll need to manually add package references)
# message("Note: You need to manually add dependencies from packages.config")
