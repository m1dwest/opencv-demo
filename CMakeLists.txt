cmake_minimum_required(VERSION 3.16)

project(opencv-demo CXX)

set(CMAKE_CXX_STANDARD 23)

find_package(realsense2 CONFIG REQUIRED)
find_package(lz4 CONFIG REQUIRED)
find_package(OpenCV CONFIG REQUIRED)
find_package(glfw3 CONFIG REQUIRED)
find_package(glad CONFIG REQUIRED)
find_package(imgui CONFIG REQUIRED)
find_package(plog CONFIG REQUIRED)

file(GLOB_RECURSE APP_SOURCES CONFIGURE_DEPENDS
    "${CMAKE_CURRENT_SOURCE_DIR}/*.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
)
list(FILTER APP_SOURCES EXCLUDE REGEX "/build/")

add_executable(demo ${APP_SOURCES})
set_target_properties(demo PROPERTIES CXX_EXTENSIONS ON)

target_link_libraries(demo PRIVATE realsense2::realsense2 lz4::lz4 ${OpenCV_LIBS} imgui::imgui glfw glad::glad plog::plog)
