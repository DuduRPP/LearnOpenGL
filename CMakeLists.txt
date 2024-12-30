cmake_minimum_required(VERSION 3.15)
project(LearnOpenGL LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add Dependencies Subdirectories
add_subdirectory(vendor/Glad)
add_subdirectory(vendor/GLFW)

# Include directories
include_directories(
    vendor/Glad/include    
    vendor/GLFW/include
)

# Add your executable
add_executable(${PROJECT_NAME} src/main.cpp)

# Link GLFW to your executable
target_link_libraries(${PROJECT_NAME} PRIVATE glad glfw)

# Link platform-specific libraries if needed
if(WIN32)
    target_link_libraries(${PROJECT_NAME} PRIVATE opengl32)
elseif(APPLE)
    find_library(COCOA_LIBRARY Cocoa REQUIRED)
    find_library(IOKIT_LIBRARY IOKit REQUIRED)
    find_library(COREVIDEO_LIBRARY CoreVideo REQUIRED)
    target_link_libraries(${PROJECT_NAME} PRIVATE ${COCOA_LIBRARY} ${IOKIT_LIBRARY} ${COREVIDEO_LIBRARY})
elseif(UNIX)
    target_link_libraries(${PROJECT_NAME} PRIVATE dl X11 pthread)
endif()
