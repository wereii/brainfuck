cmake_minimum_required(VERSION 3.10)
project(brainfuckCC C)
set(CMAKE_C_STANDARD 99)

set(CMAKE_C_FLAGS "-Wall -Wextra")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS} -Werror -g -O2")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS} -ggdb -O0")

# Check existence of ld and as programs
find_program(BINUTILS_LD NAMES ld DOC "GNU Linker")
if (${BINUTILS_LD} MATCHES "BINUTILS_LD-NOTFOUND")
    message(WARNING "Couldn't find 'ld' program, which is a runtime dependency.")
    unset(BINUTILS_LD CACHE)
endif ()

find_program(BINUTILS_AS NAMES as DOC "GNU Assembler")
if (${BINUTILS_AS} MATCHES "BINUTILS_AS-NOTFOUND")
    message(WARNING "Couldn't find 'as' program, which is a runtime dependency.")
    unset(BINUTILS_AS CACHE)
endif ()

if (NOT DEFINED BINUTILS_AS OR NOT DEFINED BINUTILS_LD)
    message(WARNING "Are you missing GNU binutils package?")
endif ()


add_executable(bfcc src/main.c src/common.c src/compiler.c)

install(TARGETS bfcc DESTINATION "${CMAKE_INSTALL_PREFIX}/bin")

option(TESTS "Generate tests" ON)
if (TESTS MATCHES ON)
    enable_testing()
    add_subdirectory(tests)
    MESSAGE(STATUS "Tests enabled")
endif ()
