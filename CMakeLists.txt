cmake_minimum_required(VERSION 3.10)
project(brainfuckCC C)
set(CMAKE_C_STANDARD 99)

set(CMAKE_C_FLAGS "-Wall -Wextra")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS} -Werror -g -O2")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS} -ggdb -O0")

add_executable(bfcc src/main.c src/common.c src/compiler.c)

install(TARGETS bfcc DESTINATION "${CMAKE_INSTALL_PREFIX}/bin")

option(DO_TESTS "Generate tests" ON)

if (DO_TESTS)
    MESSAGE("-- Tests enabled")
    enable_testing()
    add_subdirectory(tests)
endif ()
