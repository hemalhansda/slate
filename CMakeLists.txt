cmake_minimum_required(VERSION 2.5.1)
if(COMMAND cmake_policy)
    cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)

project(slate)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -std=c99")
set(CMAKE_C_COMPILER "/usr/bin/gcc")


set(SOURCE_FILES
        source/slateui.c)
set(SOURCE_BACKEND
        source/editor.c)

add_executable(slate.out ${SOURCE_FILES})
add_executable(backend.out ${SOURCE_BACKEND})

find_package( Curses REQUIRED )
include_directories( ${CURSES_INCLUDE_DIRS} )
target_link_libraries( slate.out ${CURSES_LIBRARIES} panel )

enable_testing()

add_test( backend_run backend.out test_backend.txt )
