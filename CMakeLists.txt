project(cudpp)

cmake_minimum_required(VERSION 2.8)

find_package(CUDA REQUIRED)

option(BUILD_SHARED_LIBS
  "On to build shared libraries, off for static libraries."
  OFF
  )

## Set the directory where the binaries will be stored
set(EXECUTABLE_OUTPUT_PATH
  ${PROJECT_BINARY_DIR}/bin
  CACHE PATH
  "Directory where all executable will be stored"
  )

## Set the directory where the libraries will be stored
set(LIBRARY_OUTPUT_PATH
  ${PROJECT_BINARY_DIR}/lib
  CACHE PATH
  "Directory where all the libraries will be stored"
  )

set(CMAKE_MODULE_PATH
  ${CMAKE_SOURCE_DIR}/cmake
  )

include_directories(
  ${CMAKE_SOURCE_DIR}/common/inc
  ${CMAKE_SOURCE_DIR}/cudpp/include
  )

add_subdirectory(common)
add_subdirectory(cudpp)

option(BUILD_APPLICATIONS
  "If on, builds the sample applications."
  OFF
  )

if (BUILD_APPLICATIONS)
  add_subdirectory(apps/cudpp_testrig)
  add_subdirectory(apps/simpleCUDPP)
  add_subdirectory(apps/satGL)
endif (BUILD_APPLICATIONS)
