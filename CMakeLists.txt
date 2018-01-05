cmake_minimum_required(VERSION 3.6)
project(Test)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")
set(CMAKE_CONFIGURATION_TYPES "Debug" CACHE STRING "" FORCE)

set(CMAKE_CXX_STANDARD 17)

if( CMAKE_BINARY_DIR STREQUAL CMAKE_SOURCE_DIR )
  message( FATAL_ERROR "In-source builds aren't allowed.\nDo `rm -f CMakeCache.txt && cd build && cmake ..` instead." )
endif()

find_package(SDL2 REQUIRED)
find_package(GLM REQUIRED)

set(SOURCE_FILES
  src/glad.c
  src/main.cpp
)

add_executable(testexec ${SOURCE_FILES})
target_link_libraries(testexec ${SDL2_LIBRARY})
target_include_directories(
  testexec
  PRIVATE
  "${CMAKE_SOURCE_DIR}/include"
  ${SDL2_INCLUDE_DIR}
  ${GLM_INCLUDE_DIR}
)
