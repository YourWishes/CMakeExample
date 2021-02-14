# Set Version Requirements
cmake_minimum_required(VERSION 3.15)
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

# Project Setup
project(CMakeExample VERSION 1.0)

# Include CMake Tools
include(FetchContent)

# Fetch GLFW
find_package(glfw3 3.3.2)
if(NOT glfw3_FOUND)
  FetchContent_Declare(
    glfw
    GIT_REPOSITORY https://github.com/glfw/glfw
    GIT_TAG 3.3.2
  )
  FetchContent_MakeAvailable(glfw)
endif()


# Add source files
file(GLOB_RECURSE SOURCE_FILES 
  ${CMAKE_SOURCE_DIR}/src/*.c
)

# Add header files
file(GLOB_RECURSE HEADER_FILES 
  ${CMAKE_SOURCE_DIR}/src/*.h
)


# Generate Executable.
add_executable(${PROJECT_NAME} ${HEADER_FILES} ${SOURCE_FILES})

# Add Libs
target_link_libraries(${PROJECT_NAME} glfw)
find_package(OpenGL REQUIRED)
target_link_libraries(${PROJECT_NAME} OpenGL::GL)