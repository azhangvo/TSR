cmake_minimum_required(VERSION 3.20)
project(TSR)

set(CMAKE_CXX_STANDARD 17)

add_library(glfw3 STATIC IMPORTED)
set_target_properties(glfw3 PROPERTIES
        IMPORTED_LOCATION "${CMAKE_SOURCE_DIR}/Libraries/lib/libglfw3.a"
        INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_SOURCE_DIR}/Libraries/include"
        )

add_executable(TSR main.cpp glad.c)

include_directories(Libraries/include)

find_package(OpenGL)
find_package(X11 REQUIRED)

include_directories(${X11_INCLUDE_DIR})

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)

target_link_libraries(TSR glfw3 OpenGL ${CMAKE_DL_LIBS} ${X11_LIBRARIES} Threads::Threads)