project(cudpp)

set(cudpp_VERSION_MAJOR 1)
set(cudpp_VERSION_MINOR 1)
set(cudpp_VERSION_PATCH 1)

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

set(cudpp_INCLUDE_DIRS
  ${CMAKE_SOURCE_DIR}/common/inc
  ${CMAKE_SOURCE_DIR}/cudpp/include
  )
include_directories(${cudpp_INCLUDE_DIRS})

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

# Make files that store configuration to help dependent CMake files use
# these libraries.
export(
  TARGETS cutil cudpp
  FILE ${LIBRARY_OUTPUT_PATH}/cudpp-targets.cmake
  )

set(cudpp_INCLUDE_DIRS_CONFIG ${cudpp_INCLUDE_DIRS})
configure_file(
  ${CMAKE_SOURCE_DIR}/cudpp-config.cmake.in
  ${LIBRARY_OUTPUT_PATH}/cudpp-config.cmake
  @ONLY
  )

set(cudpp_INCLUDE_DIRS_CONFIG "\${_install_dir}/include")
configure_file(
  ${CMAKE_SOURCE_DIR}/cudpp-config.cmake.in
  ${LIBRARY_OUTPUT_PATH}/cudpp-config.cmake.install
  @ONLY
  )
install(FILES ${LIBRARY_OUTPUT_PATH}/cudpp-config.cmake.install
  DESTINATION lib
  RENAME cudpp-config.cmake
  )

configure_file(
  ${CMAKE_SOURCE_DIR}/cudpp-config-version.cmake.in
  ${LIBRARY_OUTPUT_PATH}/cudpp-config-version.cmake
  @ONLY
  )
install(FILES ${LIBRARY_OUTPUT_PATH}/cudpp-config-version.cmake
  DESTINATION lib
  )
