if(NOT PICO_SDK_PATH)
  message(FATAL_ERROR "This module needs to be imported after pico_sdk_init()")
endif(NOT PICO_SDK_PATH)

cmake_minimum_required(VERSION 3.12..3.25)

project(
  can2040
  LANGUAGES C
  VERSION 1.6.0)

add_library(can2040 INTERFACE)
add_library(can2040::can2040 ALIAS can2040)

target_sources(can2040 INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/src/can2040.h
                                 ${CMAKE_CURRENT_SOURCE_DIR}/src/can2040.c)

target_link_libraries(can2040 INTERFACE pico_stdlib hardware_pio cmsis_core)

pico_generate_pio_header(can2040 ${CMAKE_CURRENT_LIST_DIR}/pio/can2040.pio)

target_include_directories(can2040 INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/src
                                             ${CMAKE_CURRENT_BINARY_DIR})
