# Specify the minimum version for CMake

cmake_minimum_required(VERSION 2.8)

set(CMAKE_WIRINGPI_DIR "${CMAKE_SOURCE_DIR}/wiringPi/wiringPi")
set(CMAKE_WIRINGPI_LIB "${CMAKE_SOURCE_DIR}/wiringPi/wiringPi/libwiringPi.a")
IF(CMAKE_CROSSCOMPILING)
add_custom_command(
   OUTPUT ${CMAKE_WIRINGPI_LIB}
   COMMAND make CC=${CMAKE_C_COMPILER} static
   WORKING_DIRECTORY ${CMAKE_WIRINGPI_DIR}
   )
ELSE(CMAKE_CROSSCOMPILING)
add_custom_command(
   OUTPUT ${CMAKE_WIRINGPI_LIB}
   COMMAND make static
   WORKING_DIRECTORY ${CMAKE_WIRINGPI_DIR}
   )
ENDIF(CMAKE_CROSSCOMPILING)
add_custom_target(
   wiringpi
   DEPENDS ${CMAKE_WIRINGPI_LIB}
   )

add_library(wiringPi STATIC)
target_include_directories(wiringPi PUBLIC ${CMAKE_WIRINGPI_DIR})
add_dependencies(wiringPi wiringpi)