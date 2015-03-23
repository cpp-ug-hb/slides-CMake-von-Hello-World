cmake_minimum_required(VERSION 3.0)
project(Print)


## Build the library
add_library(
  print STATIC
  print.cpp
  print.hpp
)

target_include_directories(
  print
  PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
  PUBLIC $<INSTALL_INTERFACE:$<INSTALL_PREFIX>/include>
)


## Install it and the header
install(
  TARGETS print
  DESTINATION lib
  EXPORT Print-export
)

install(
  FILES print.hpp
  DESTINATION include
)


## Generate and install CMake config files
include(CMakePackageConfigHelpers)

configure_package_config_file(
  PrintConfig.cmake.in
  ${CMAKE_CURRENT_BINARY_DIR}/PrintConfig.cmake
  INSTALL_DESTINATION lib/Print/cmake
)

write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/PrintConfigVersion.cmake"
  VERSION 1.0
  COMPATIBILITY SameMajorVersion
)

install(
  FILES
    ${CMAKE_CURRENT_BINARY_DIR}/PrintConfig.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/PrintConfigVersion.cmake
  DESTINATION lib/Print/cmake
)

install(
  EXPORT Print-export
  DESTINATION lib/Print/cmake
)
