cmake_minimum_required(VERSION 3.6)
project(imgui-opengl-glfw-glew-cmake-demo)

set(CMAKE_CXX_STANDARD 11)

set(CMAKE_VERBOSE_MAKEFILE 1)
set(APP_VERSION_MAJOR 1)
set(APP_VERSION_MINOR 0)
set(CMAKE)

set(APP_TARGET imgui-demo.app)

include_directories(${PROJECT_SOURCE_DIR})
add_executable(${APP_TARGET} main.cpp)
target_link_libraries(${APP_TARGET} imgui)

# opengl
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

if (APPLE)
    find_package(PkgConfig REQUIRED)
endif()

# glfw
find_package(glfw3 CONFIG REQUIRED)
# include_directories(${GLFW_INCLUDE_DIRS})
# link_libraries(${GLFW_LIBRARY_DIRS})
pkg_check_modules(GLFW3 REQUIRED glfw3)
include_directories(${GLFW3_INCLUDE_DIRS})
link_libraries(${GLFW3_LIBRARIES}) 

# glew
find_package(GLEW CONFIG REQUIRED)
# include_directories(${GLEW_INCLUDE_DIRS})
pkg_check_modules(GLEW REQUIRED glew)
include_directories(${GLEW_INCLUDE_DIRS})
link_libraries(${GLEW_LIBRARIES}::glew) 

# if (APPLE)
#     find_library(COCOA_LIBRARY Cocoa)
#     find_library(OpenGL_LIBRARY OpenGL)
#     find_library(IOKIT_LIBRARY IOKit)
#     find_library(COREVIDEO_LIBRARY CoreVideo)
#     SET(EXTRA_LIBS ${COCOA_LIBRARY} ${OpenGL_LIBRARY} ${IOKIT_LIBRARY} ${COREVIDEO_LIBRARY})
# endif (APPLE)

if (WIN32)
# nothing now
endif (WIN32)

add_subdirectory(imgui)

target_link_libraries(
        ${APP_TARGET}
        # glfw
        # ${GLFW_LIBRARIES}
        ${OPENGL_LIBRARIES}
        # ${GLEW_LIBRARIES}
        # GLEW::glew
        # ${EXTRA_LIBS}
)