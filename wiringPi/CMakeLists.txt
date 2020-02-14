# Specify the minimum version for CMake

cmake_minimum_required(VERSION 3.2)

find_library(PTHREAD_LIBRARIES pthread)
find_library(CRYPT_LIBRARIES crypt)
find_library(RT_LIBRARIES rt)
find_library(M_LIBRARIES m)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${DEBUG} ${DEFS} -Wformat=2 -Wall -Wextra -Wno-unused-function -Winline ${NWFLAGS} ${INCLUDE} -pipe -fPIC")

set(WIRINGPI_INC_DIRS "${OBC_SOURCE_DIR}/wiringPi/wiringPi")
include_directories(${WIRINGPI_INC_DIRS})

file(GLOB SRC_FILES ${WIRINGPI_INC_DIRS}/*.c)
add_library( wiringPi STATIC ${SRC_FILES} )
target_link_libraries(wiringPi ${PTHREAD_LIBRARIES}
	${CRYPT_LIBRARIES}
	${RT_LIBRARIES}
	${M_LIBRARIES})

target_include_directories (wiringPi PUBLIC ${WIRINGPI_INC_DIRS})
