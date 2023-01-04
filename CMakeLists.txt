cmake_minimum_required(VERSION 3.18)
project(trt_flash_attention)

find_package(CUDA REQUIRED)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_CXX_STANDARD 11)

set(FMHA_INCLUDE_DIR
    ${CMAKE_CURRENT_SOURCE_DIR}/include
    CACHE PATH "")
file(GLOB_RECURSE FMHA_FILES *.cpp)

add_library(trt_flash_attention SHARED ${FMHA_FILES})
include_directories(SYSTEM ${CUDA_INCLUDE_DIRS})
include_directories(${FMHA_INCLUDE_DIR})

include(GNUInstallDirs)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

message(STATUS ${CMAKE_INSTALL_INCLUDEDIR})

install(
  TARGETS trt_flash_attention
  EXPORT trt_flash_attention
  PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
