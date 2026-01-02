cmake_minimum_required(VERSION 3.10 FATAL_ERROR)

project(open-simplex-noise-in-c)

option(OSN_BUILD_TEST "Build the test binary?" OFF)

add_library(open-simplex-noise-in-c
  ${CMAKE_CURRENT_SOURCE_DIR}/open-simplex-noise.c
  ${CMAKE_CURRENT_SOURCE_DIR}/open-simplex-noise.h)
target_include_directories(open-simplex-noise-in-c
  PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
if (OSN_FLOAT_TYPE)
  target_compile_definitions(open-simplex-noise-in-c
    PUBLIC OSNFLOAT=${OSN_FLOAT_TYPE})
endif()

if (OSN_BUILD_TEST)
  find_package(ZLIB REQUIRED) # PNG dependency
  find_package(PNG REQUIRED)
  
  add_executable(open-simplex-noise-in-c-test
    ${CMAKE_CURRENT_SOURCE_DIR}/open-simplex-noise-test.c)
  target_link_libraries(open-simplex-noise-in-c-test
    PRIVATE PNG::PNG open-simplex-noise-in-c)
endif()
